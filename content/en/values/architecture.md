---
title: "Architecture"
weight: 20
type: docs
description: Building long-term systems and fighting with technical debt.
---

### 1. We care about API cleanness.

* We expose services to other teams through APIs on the Developer Portal. *[<i class="fa fa-lock"></i> internal ](https://devportal-apim.apps.lmru.tech/)*
* We are following [API Design Principles]({{< ref "/api" >}}). Non compliant APIs should declared as a technical debt and modified.
* <abbr data-toggle="tooltip" title="Service is an application, but not all applications are services. For example, a frontend is not a service.">Services</abbr> do not provide a client library. The API and its data model are expressed as REST and JSON <abbr  data-toggle="tooltip" title="Shared internal dependencies lead to a large-scale complexity over time.">[?]</abbr>.

#### Practices & rituals: 
{{< glossary title="30% rule" >}}
Each engineer may spend some part of his working time on R&D tasks, technical debt reduction or education. 
The percentage it is approximate number and should be determined by technical leader together with the product team.
{{< /glossary >}}

{{< alert color="warning" title="Antipattern" >}}GraphQL or GRPC endpoint exposed for external usage. <sup>[[See Technology Value]]({{< ref "technology/#3-choice-of-technology-aligned-with-technology-tablehahahugoshortcode-s6-hbhb" >}})</sup>{{< /alert >}}

---

### 2. We use modular architecture and avoid tight coupling between products.

* <abbr data-toggle="tooltip" title="When we are talking about “Modular” or “Microservices” architecture it means set of architecture patterns.">Modules</abbr> are isolated and loosely coupled.
* Modules have single responsibility. 
* We can throw away existing, add on new or change sequence of modules execution safely without impact on other functionality.
* We periodically review important architecture and technical debt issues. 

#### Practices & rituals: 
{{< glossary title="Architecture Committee" >}}
Enterprise & Solution architects meeting. Held by demand. Leader – CTO.

Main tasks: 
* solution architecture problem solving
* escalation place for architecture gaps / technical debt grow
* unblocking issues with technical debt
* solution architecture consulting
{{< /glossary >}}
{{< glossary title="High Cohesion" source="https://stackoverflow.com/questions/10830135/what-is-high-cohesion-and-how-to-use-it-make-it" >}}
High cohesion is when you have a class (or module) that does a well defined job. Low cohesion is when a class does a lot of jobs that don't have much in common.
{{< /glossary >}}
{{< glossary title="External Configuration" >}}
A changeable configuration of applications should be stored in the environment.
{{< /glossary >}}
{{< glossary title="Orchestration / Choreography" >}}
Microservices pattern for building of sequenses of execution (SAGAs). Short explanation [here](https://medium.com/ingeniouslysimple/choreography-vs-orchestration-a6f21cfaccae). Detailed [here](https://microservices.io/patterns/data/saga.html).
{{< /glossary >}}

{{< alert color="warning" title="Antipattern" >}}Microservices with hardcoded steps and multiple entries.{{< /alert >}}

---

### 3. We develop only economically sustainable products.

* We avoid duplication of systems functionality.
* Every system have single mantainer team.

#### Practices & rituals: 
{{< glossary title="Revenue / Expenses Ratio" >}}
An estimated amount of money earned by product or feature divided on spends on it should be calculated before work run.
{{< /glossary >}}
{{< glossary title="KISS" >}}
Keep It Stupid Simple. Like Occam said, «[entities should not be multiplied without necessity](https://en.wikipedia.org/wiki/Occam%27s_razor)». Adding new levels of abstraction must have a strong reason. Adding new data entities or solution components also must have strong reason. Simplification is a King and we welcome the approach to describe it as an architecture debt and rework the complex areas to make it simple.
{{< /glossary >}}
{{< glossary title="DRY" >}}
Do Not Repeat Yorself. Differently said, we are not develop multilple systems/modules/microservices/components with the same purpose.
{{< /glossary >}}

{{< alert color="warning" title="Antipattern" >}}Unprofitable product continues to develop for a long time because it is scary to admit a mistake. <sup>[[See People Value]]({{< ref "people/#2-we-accept-mistakes-and-learn-from-them" >}})</sup>{{< /alert >}}
