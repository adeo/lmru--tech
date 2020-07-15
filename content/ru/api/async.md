---
title: "Принципы построения асинхронного API"
weight: 30
type: docs
---

В компании используются две технологии для межпродуктового асинхронного взаимодействия.

<div class="row mb-2 mt-4">
	<div class="offset-4 col-4 text-center">
    <img src="../kafka.png" alt="Kafka logo" style="height: 100px;"/>
    <h3 class="h3 mt-3">Kafka</h4>
  </div>
  <div class="col-4 text-center">
    <img src="../rabbitmq.png" alt="RabbitMQ logo" style="height: 100px;"/>
    <h3 class="h3 mt-3">RabbitMQ</h4>
  </div>
</div>

<div class="row mb-4 mt-2">
	<div class="col-4 text-right">
    <p><b class="text-nowrap">Комфортная скорость</b></p>
    <p><b class="text-nowrap">Acknowledgment</b></p>   
    <p><b class="text-nowrap">Многоразовое чтение</b></p>
    <p><b class="text-nowrap">Продвинутый роутинг</b></p>
    <p><b class="text-nowrap">Приоритет сообщений</b></p>
    <p><b class="text-nowrap">Модель</b></p>
    <p><b class="text-nowrap">Скалирование брокера</b></p>
    <p><b class="text-nowrap">Скалирование клиента</b></p>
  </div>
  <div class="col-4 text-center">
    <p>100 rps</p>
    <p><i class="fa fa-check"></i></p>
    <p><i class="fa fa-check"></i></p>
    <p><i class="fa fa-minus"></i></p>
    <p><i class="fa fa-minus"></i></p>
    <p><abbr data-toggle="tooltip" title="Потребители запрашивают батчи сообщений начиная с определённого оффсета.">Пулл</abbr></p>
    <p>Горизонтальное</p>
    <p>Скалирование количества партиций топика</p>
  </div>
  <div class="col-4 text-center">
    <p>20 rps</p>
    <p><i class="fa fa-check"></i></p>
    <p><i class="fa fa-minus"></i></p>
    <p><i class="fa fa-check"></i></p>
    <p><i class="fa fa-check"></i></p>
    <p><abbr data-toggle="tooltip" title="Сообщения доставляются от Реббита к потребителю.">Пуш</abbr></p>
    <p>Вертикальное <sup><abbr data-toggle="tooltip" title="Да, все наши кластеры Реббита проскалированы горизонтально. Однако, Реббит потребляет много ресурсов для координации и гораздо эффективнее скалировать его через увеличение мощности нод.">как так?</abbr></sup></p>
    <p>Скалирование количества потребителей</p>
  </div>
</div>

<div class="row mb-4 mt-2">
	<div class="col-4 text-right">
    <p><b class="text-nowrap">Кейсы использования</b></p>
  </div>
  <div class="col-4">
    <ul>
      <li>Анализ данных: трекинг, поглощение данных, логгирование, аудит безопасности.</li>
      <li>Процессинг реального времени: множество продюссеров с небольшим количеством консьюмеров.</li>
      <li>Event Sourcing: моделирование изменения состояния системы через поледовательность событий.</li>
    </ul>
  </div>
  <div class="col-4">
    <ul>
      <li>Сложный роутинг до потребителей.</li>
      <li>Меж-микросервисная коммуникация.</li>
      <li>Приложение поддериживает только легаси протоколы (STOMP, MQTT и другие).</li>
    </ul>
  </div>
</div>

## Общие правила

Каждый продукт имеет свой собственный экземпляр брокера сообщений. 
Система, публикующая данные, ответственна за этот экземпляр.

Всякая информация, обладающая ценностью одновременно для нескольких систем, передаётся через <abbr data-toggle="tooltip" title="Независимое от бизнес процесса и способа потребления, а также минималичичное API, созданное для нескольких потребителей.">канонические</abbr> топики или эксчейнджи. Все каноничные топики, эксчейнджи и очереди привязаны к домену через указание <abbr data-toggle="tooltip" title="products, services, stocks, prices, offers, orders, customers, partners, company, locations, finance или technical">канонического домена</abbr> в названии.

Запрещается отправка напрямую в RabbitMQ очередь: вместо этого используй эксчейндж.

## Соглашение о названиях

Используй *camelCase* для всех полей.

### Kafka Топик

```
[app]-[type]-[int/ext]-[domain]-[object]-[version]
```

* `app` название публикующего приложения
* `type`
  * `system` топик для использования только внутри продуктовой команды или приложения
  * `init` топик для полного извлечения данных, не используемый для постоянной интеграции <sup><abbr data-toggle="tooltip" title="Загрузить информацию в новое приложение или восстановить исторические данные после падения.">примеры</abbr></sup>
  * `canonical` топик для публикации <abbr data-toggle="tooltip" title="Независимое от бизнес процесса и способа потребления, а также минималичичное API, созданное для нескольких потребителей.">канонической</abbr> информации
* `int/ext` *int* топик используется внутри, *ext* топик опубликован в Интернет
* `domain` <abbr data-toggle="tooltip" title="products, services, stocks, prices, offers, orders, customers, partners, company, locations, finance или technical">канонический домен</abbr>
* `object` данные, отправляемые через это топик <sup><abbr data-toggle="tooltip" title="fulfillmentTask, shipment, paymentTask">примеры</abbr></sup>
* `version` версия топика

{{% alert color="success" title="Пример" %}}
`crm-canonical-int-customers-organization-v9`
{{% /alert %}}

### RabbitMQ Эксчейндж

```
[app]-[type]-x-[domain]-[object]-[version]
```

* `app` название публикующего приложения
* `type`
  * `tx` topic exchange.
  * `fx` fanout exchange.
  * `dx` direct exchange.
  * `hx` headers exchange
* `x` exchange 
* `domain` <abbr data-toggle="tooltip" title="products, services, stocks, prices, offers, orders, customers, partners, company, locations, finance или technical">канонический домен</abbr>
* `object` данные, передаваемые через эксчейндж <sup><abbr data-toggle="tooltip" title="fulfillmentTask, shipment, paymentTask">примеры</abbr></sup>
* `version` версия эксчейнджа

{{% alert color="success" title="Пример" %}}
`paymentGateway-tx-x-orders-paymentTask-v1`
{{% /alert %}}

### RabbitMQ Очередь

```
[app]-[type]-q-[domain]-[object]-[filter]-[version]
```

* `app` название подписавшегося приложения
* `type`
  * `tx` topic эксчейндж.
  * `fx` fanout эксчейндж.
  * `dx` direct эксчейндж.
  * `hx` headers эксчейндж
* `q` очередь 
* `domain` <abbr data-toggle="tooltip" title="products, services, stocks, prices, offers, orders, customers, partners, company, locations, finance или technical">канонический домен</abbr>
* `object` данные, передаваемые через очередь <sup><abbr data-toggle="tooltip" title="fulfillmentTask, shipment, paymentTask">примеры</abbr></sup>
* `filter` описания фильтров для типов: `tx`, `dx`, `hx` <sup><abbr data-toggle="tooltip" title="created, updatedStatus, updatedStatusPaid">примеры</abbr></sup>
* `version` версия очереди

{{% alert color="success" title="Пример" %}}
`solution-tx-q-orders-paymentTask-created-v2`
{{% /alert %}}