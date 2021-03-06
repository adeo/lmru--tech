---
title: "Technology"
weight: 30
type: docs
description: Сonstantly challenging selection of tools.
---

### 1. All codebase are compliant with [InnerSource requirements](https://adeo.github.io/innersource/).

* Codebase accessible for each collaborators and stored in GitHub.
* Non compliant repositories declared as a technical debt and fixed.
* Code review is mandatory.

#### Practices & rituals: 
{{< glossary title="30% rule" >}}
Each engineer may spend some part of his working time on R&D tasks, technical debt reduction or education. 
The percentage it is approximate number and should be determined by technical leader together with the product team.
{{< /glossary >}}
{{< glossary title="The Boy Scout Rule" source="https://deviq.com/boy-scout-rule/" >}}
True Boy Scouts have a rule regarding camping, that they should leave the campground cleaner than they found it.

Our version is: **leave your code better than you found it.**
As [Uncle Bob said](https://www.oreilly.com/library/view/97-things-every/9780596809515/ch08.html), *the act of leaving a mess in the code should be as socially unacceptable as littering.*
{{< /glossary >}}
{{< glossary title="Contribution conventions" source="https://adeo.github.io/innersource" >}}
The project uses a consistent convention to handle contributions from it’s own team but also for external teams, I.E: pull requests, code-review and branch permissions
{{< /glossary >}}

{{< alert color="warning" title="Antipattern" >}}Closed repository without readme and maintainers working in production.{{< /alert >}}

---

### 2. We automate everything as much as possible.

* We prefer automated tests rather than manual testing.
* Build & Deploy done by CI tool.

#### Practices & rituals: 
{{< glossary title="DevOps" >}}
A friendship between developers and operations :) If seriously, I would recommend to read [this book](https://www.amazon.com/Phoenix-Project-DevOps-Helping-Business/dp/0988262592) to understand what is it.

We practice DevOps worship as the main approach of product building.
{{< /glossary >}}
{{< glossary title="IaC" >}}
Infrastructure as a Code. We prefer to have automated configuration files rather than manual UI clicks. The configuration file contains a script on how to prepare infrastructure, build, and deploy applications.
{{< /glossary >}}

{{< alert color="warning" title="Antipattern" >}}It is scary to make release because of plenty of manual work and rare occasion.{{< /alert >}}

---

### 3. Choice of technology aligned with [Technology Table]({{< ref "/stack" >}}).

* Table is kept up-to-date by technology committee.
* All movements in the table are  logged in decision records table.
* We support iniciatives to try new technology or approach after notice of technology committee.

#### Practices & rituals: 
{{< glossary title="Technology Committee" >}}
The committee is a community of enterprise architects, technical architects and technical leaders of development teams and IT infrastructure. The main goal of the committee is the selection and recommendations on the use of technologies in Leroy Merlin Russia and increasing the efficiency of use of company resources. Technologies are understood as programming languages, frameworks and libraries, software tools and approaches in the context of specific usage scenarios.

Meetings are held at least once a month. Leader — CTO.
{{< /glossary >}}

{{< alert color="warning" title="Antipattern" >}}Manager orders an external company to write a non-maintainable black-box application on 1C.{{< /alert >}}

---

### 4. Front applications follow [Design System](https://fronton.leroymerlin.ru/).

<i class="fa fa-lock mr-1"></i> <i>Design system currently accessible only from internal network</i>

* All business settings configurable through UI.

{{< glossary title="Design System" source="https://uxdesign.cc/what-the-heck-is-a-design-system-c89a8ea73b0d">}}
Design System – the system of rules and tools for visual and technical design. Reflects the philosophy of the product. Design System continuously evolving.
{{< /glossary >}}

{{< alert color="warning" title="Antipattern" >}}Built in store application uses Comic Sans.{{< /alert >}}

---

### 5. We build robust applications and infrastructure.

* We know about production issues before end-users.
* We prefer develop stateless applications and run them inside containers using container orchestrator.
* Applications handle partial outages.
* Applications and databases are replicated and can be sharded.
* Applications responses accurately and correctly handle wrong inputs.
* Services provides <abbr data-toggle="tooltip" title="Service Level Objective is a goal that service provider wants to reach.">SLO</abbr> and controls them.
* Infrastructure for key systems allows to have master-master replication.

#### Practices & rituals: 
{{< glossary title="VALET" source="https://landing.google.com/sre/workbook/chapters/slo-engineering-case-studies/" >}}
A way how to track SLO. 

* Volume (traffic) — how much business volume can my service handle?
* Availability — is the service up when I need it?
* Latency — does the service respond fast when I use it?
* Errors — does the service throw an error when I use it?
* Tickets — does the service require manual intervention to complete my request?
{{< /glossary >}}
{{< glossary title="Feature Toggling">}}
An approach where new functionality should be added as a pluggable module and can be turned off at any time.
{{< /glossary >}}
{{< glossary title="Distributed Tracing" >}}
Each request on the entrance receives a unique tracing ID and pushes this ID with all consequence calls.
{{< /glossary >}}
{{< glossary title="Telemetry" >}}
Applications expose endpoints with health metrics for analysis and monitoring.
{{< /glossary >}}

{{< alert color="warning" title="Antipattern" >}}Client can't order because email system is broken.{{< /alert >}}

---

### 6. Software testing has the same importance as software development.

* Testing process start on designing product/feature requirements stage.
* Every product team has at least one QA-engineer.
* Source code is covered by tests immediately. Tests created while code is being crafted, and not postpone to the backlog.

#### Practices & rituals: 
{{< glossary title="Dynamic test environments" >}}
Software testing is conducted in dynamic test environment. Such environment should include all required for testing dependencies (it is recommended to mock out external services). Testing environment is isolated from external processes and systems to prevent them from affecting test results. Test environment is removed when testing is finished.
{{< /glossary >}}
{{< glossary title="Mocking" >}}
It is important to be independent of external systems (unstable behavior, restricted or prohibited control of test data) during software testing. For that case use mocking of such systems.
Mock is a system emulator that duplicates system behavior in limited manner but does not reproduce its inner logic.
{{< /glossary >}}
{{< glossary title="Performance testing" >}}
Type of software testing which involve testing of system’s performance but not its logic.

Backend performance is measured by following metrics:
* requests per second
* response time, ms
* percentage of failures, %
* system resources usage, %

Frontend performance is measured with Google Lighthouse and its metrics.
For backend tests recommended use the Gatling.
{{< /glossary >}}
{{< glossary title="Canary deployment" >}}
Canary deployment helps to reduce negative impact of new feature deployment in case it contains bugs. This strategy is that the first deploy the change to a small subset of servers, test it, and then roll the change out to the rest of the servers. [Learn more](https://octopus.com/docs/deployment-patterns/canary-deployments#:~:text=Canary%20deployments%20are%20a%20pattern,the%20rest%20of%20the%20servers.)
{{< /glossary >}}

{{< alert color="warning" title="Antipattern" >}}Functional testing in production environment creates real incidents and worsens real users’ experience{{< /alert >}}
