---
title: "Open Source"
linkTitle: "Open Source"

simple_list: true
type: docs
weight: 27
menu:
  main:
    weight: 27
---

We actively use open source solutions created and supported by enthusiasts from around the world.
We want to not only use but to return the contribution and participate in the development
of Open source products and support the community. 

Here is the instruction for the teams what to do in order to open up the project.

## Three steps to open source your code

{{< blocks/section color="white" >}}
{{% blocks/feature icon="fa-dice-one" title="Step 1" %}}
Check attribution and project originality
{{% /blocks/feature %}}

{{% blocks/feature icon="fa-dice-two" title="Step 2" %}}
Choose the license
{{% /blocks/feature %}}

{{% blocks/feature icon="fa-dice-three" title="Step 3" %}}
Check compatibility of third-party dependencies
{{% /blocks/feature %}}
{{< /blocks/section >}}

### Step 1. Check attribution and project originality.
The project should have a list of members for the project. Each member should have:

* Identity – Pavel Griboedov
* Company — LLC «Leroy Merlin Vostok»
* Contact email – pavel.griboedov@leroymerlin.ru

#### Setting correct information in `git`
It is required to send proper meta information in all commits. 
This information used to determine an author of the code.

```
git config --global user.name "Pavel Griboedov"
git config --global user.email "pavel.griboedov@leroymerlin.ru"
```

Involving trainee or temp workers in the open sourcing internal projects or 
in contributing to third-party projects is strictly prohibited.

When an external company writes code for us then this fact should be mentioned and we should have a proper contract. 

#### Checking originality
Originality is an important legal concept. We can enforce legal rights only if the code is *original*. 
In practice, originality stems from the ability to identify *design decisions* in the source code.

{{< alert color="success" title="Design Decision" >}}
Personal intellectual contribution of the developer demonstrating that another developer would have solved
the technical issue in a different manner.

![Design Decision Example](/images/design_decision.jpg)
{{< /alert >}}

{{< alert color="danger" title="Not a Design Decision" >}}
Automatically generated code or the code which can only be written in a single manner.

![Not A Design Decision Example](/images/not_design_decision.jpg)
{{< /alert >}}

### Step 2. Choose the license
The hardest and the most important part is to choose the correct license for your code.
Some third-party libraries used in your project can force you to use a specific license — 
more details in [step 3](#step-3-check-compatibility-of-third-party-dependencies).

##### Copyleft licenses
This type of license in most of the cases requires to use the same open source
license when distributing the code together with yours.

The most popular license here is [GNU GPLv3](https://choosealicense.com/licenses/gpl-3.0/). 
It lets people do almost anything they want with your project, except distributing closed source versions.

##### Copyright licenses
This type of license allows everyone to distribute the code together with your code in the closed proprietary products.

* BSD — there is two general editions.
The [original](https://opensource.org/licenses/BSD-3-Clause) license requires advertisement of the initial project on all products uses the code with the line like
«This product includes software developed by the `organization`».
[Modified](https://opensource.org/licenses/bsd-license.php) version not includes this requirement. 
All versions are going under the same name and to avoid collision **we do not recommend** to use this licenses.
This license ignores patent rights, described further.

* [MIT](https://opensource.org/licenses/MIT) - short license in several paragraphs.
The license beloved by developers because of simplicity and it works well for small projects.
The MIT license was drafted before software patents were common. Therefore, they completely ignore the topic.

{{< alert color="primary" title="Difference between Copyright and Patent" >}}
There are two, completely independent, forms of intellectual property rights
that can be used to protect software against unwanted copying/modification:

* Copyright
* Patents

Copyright protects the "expression of an idea" and applies to the source code that gets written.
Copyright protection is granted automatically at the moment that the code is written.
Copyright protection means that only the author is allowed to make copies of or changes in the code,
unless the author explicitly gives this right also to others by means of a copyright license.

Patents protect inventions and need to be explicitly requested. When a patent has been granted to you,
you have the exclusive right to make use of that invention or to give a patent license to others.
Patents can be broader that copyrights, because if someone else makes the same invention that you have a patent on,
then you can force them to stop using the invention or to buy a patent license from you. With copyright, however,
it is possible that multiple people independently write very similar code and each has their own copyright protection.

[source](https://opensource.stackexchange.com/questions/6302/what-does-express-grant-of-patent-rights-from-contributors-to-users-mean)
{{< /alert >}}

* [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt) —
one of the most popular open source license used by [CNCF](https://www.cncf.io/) and [Apache Foundation](https://www.apache.org/licenses/).
Longer than MIT, but covers also patent rights.

#### Recommended license for common cases
By default we offer you to use a 
<abbr data-toggle="tooltip" title="It means everybody can distribute your code with the closed proprietary products.">non copyleft</abbr>
 open source license – [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt).

{{< alert color="primary" title="Apache License 2.0" >}}
A permissive license whose main conditions require preservation of copyright and license notices.
Contributors provide an express grant of patent rights. 
Licensed works, modifications, and larger works may be distributed under different terms and without source code.

![Apache License](/images/apache_license.jpg)

[source](https://choosealicense.com/licenses/apache-2.0/)
{{< /alert >}}

#### Placing the license information
* Each code file should have copyright notice on the top.

```
/*
 * Copyright 2020 LLC Leroy Merlin Vostok.
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      https://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

package ru.leroymerlin.delivery.tariff.convert;
```

* `README.md` should mention the license used.

```
## License

This repository is released under version 2.0 of the 
[Apache License](https://www.apache.org/licenses/LICENSE-2.0).
```

* `LICENSE` file in the root should have [complete text](https://www.apache.org/licenses/LICENSE-2.0.txt) of the license.


### Step 3. Check compatibility of third-party dependencies.

Third-party component licenses may force to use a particular license for the whole project.
It is mandatory to check license compatibility between components and between component and project license.

| Third Party License Type                                                         | Examples             | Actions Required                                                            |
|----------------------------------------------------------------------------------|----------------------|-----------------------------------------------------------------------------|
| **Permissive**                                                                   | `Apache` `BSD` `MIT` | None                                                                        |
| **Copyleft**                                                                     | `GPL` `LGPL` `AGPL`  | <abbr data-toggle="tooltip" title="Ensure that its intial license allows its redistribution under the licence selected by the project or alongside the other third-party components governed by a possibly different license.">Check compatibility</abbr>|
| **Unidentified**                                                                 |                      | Delete or replace component                                                 |
| **Proprietary**                                                                  | `Commercial`         | Delete or replace component                                                 |
| **Requires accepting another agreement**<br /> alongside the open source license | `CLA` `CAA`          | Accept the agreement <br />or delete or replace component |


## All Steps Have Been Passed
Congratulations! You may open source the project. <i class="fa fa-glass-cheers"></i>

For doing that you need to announce your willing at the CI/CD slack channel 
and let your colleagues add the repository to the allowlist of `prevent-public-repos` script.

After that, you can make repository public in the settings of the repository.
