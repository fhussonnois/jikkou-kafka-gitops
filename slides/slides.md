---
theme: seriph
# title of your slide, will auto infer from the first header if not specified
title: Jikkou
description: "Jikkou"
author: fhussonnois
# enable presenter mode, can be boolean, 'dev' or 'build'
presenter: true
# enabled pdf downloading in SPA build, can also be a custom url
download: false
# filename of the export file
exportFilename: 'GitOps-for-Apache-Kafka-With-Jikkou-v1.0.0.pdf'
# export options
# use export CLI options in camelCase format
# Learn more: https://sli.dev/guide/exporting.html
export:
  format: pdf
  timeout: 30000
  dark: false
  withClicks: false
  withToc: false
  perSlide: true
background: /assets/cover100.jpeg
themeConfig:
  primary: '#16262f'
class: text-left
highlighter: shikiji
lineNumbers: false
info: false
drawings:
  persist: false
transition: slide-left
mdc: true
---

<style>
.slidev-layout.cover h1 {
  color: #ffffff!important;
}
.slidev-layout h1 {
  color: #3b5467!important;
  font-size: 1em;
}
.text-light {
  color: #6C757D!important;
}
.text-dark {
  color: #343a40!important;
}
.text-small {
  font-size: 0.8em;
}
.float-right {
  float: right
}
ul {
  list-style: circle!important;
}
.logo-center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
</style>

#  GitOps for Apache Kafka®<br/>At scale and with ease using Jikkou!

<br />
The Opensource Resource as Code Framework for Apache Kafka®

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/streamthoughts/jikkou" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
  <a href="https://medium.com/@{{ $slidev.configs.author }}" target="_blank" alt="Medium" title="Open in Medium"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
     <carbon-logo-medium />
  </a>
    <a href="https://twitter.com/{{ $slidev.configs.author }}" target="_blank" alt="Twitter" title="Open in Twitter"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
     <carbon-logo-twitter /> @{{ $slidev.configs.author }}
  </a>
</div>

---
layout: 'intro'
---

# Florian Hussonnois

<div class="leading-8 opacity-80">
Lead Software Engineer <strong>@Kestra</strong>.<br><br>
</div>

* Worked for 12 years as Consultant & Trainer
* 10+ years of experience with Apache Kafka (version 0.7)
* Open-source projects such as [Kafka Connect File Pulse](https://streamthoughts.github.io/kafka-connect-file-pulse/), [Jikkou](https://www.jikkou.io/)
* [Confluent Community Catalyst](https://developer.confluent.io/catalysts/) since 2019

<div class="pt-6">
  <a href="https://github.com/streamthoughts/jikkou" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
  <a href="https://medium.com/@{{ $slidev.configs.author }}" target="_blank" alt="Medium" title="Open in Medium"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
     <carbon-logo-medium />
  </a>
    <a href="https://twitter.com/{{ $slidev.configs.author }}" target="_blank" alt="Twitter" title="Open in Twitter"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
     <carbon-logo-twitter /> @{{ $slidev.configs.author }}
  </a>
</div>

<img src="/static/avatar.png" class="rounded-full w-50 abs-tr mt-50 mr-25"/>

---
layout: image-right
image: /assets/img-gen-101.jpeg
left: true
equal: false
---

# The True Story Behind Every Kafka Resources!

<style>
.slidev-layout blockquote {
    font-size: 0.60em !important;
    color: #555555 !important;
    border-left-width: 0px !important;
    border-radius: 0rem !important;
}
</style>

It all starts with Kafka's CLI.

```bash
#!/bin/bash
kafka-topics --bootstrap-server localhost:9092 \
  --create --topic my_topic \
  --partitions 6 \
  --replication-factor 1

# (output)
# Created topic my-topic.
```

> <i>in a galaxy far, far away....</i>
> <br /> <br />
> <strong>Padawan</strong>: "Can you please create a new topic for my team?" <br/>
> <strong>Jedi</strong>: "Yes, of course! How many partitions do you need?" <br/>
> <strong>Padawan</strong>: "...<i>(silence)</i>" <br/>

---
layout: image-left
image: /assets/img-gen-102.jpeg
---
#  What About Configuration ?

Yet another story!

<style>
.slidev-layout blockquote {
    font-size: 0.60em !important;
    color: #555555 !important;
    border-left-width: 0px !important;
    border-radius: 0rem !important;
}
</style>

```bash
#!/bin/bash
# Update to new value
kafka-configs --bootstrap-server localhost:9092 \
  --entity-type topics --entity-name my_topic \
  --alter --add-config retention.ms=17280000
```

```bash
#!/bin/bash
# Reset to default value
kafka-configs --bootstrap-server localhost:9092 \
  --entity-type topics --entity-name my_topic  \
  --alter --delete-config retention.ms
```

> <i>in a galaxy far, far away....</i>
> <br /> <br />
> <strong>Amiral</strong>: "Could you update the config of this topic?" <br/>
> <strong>Stormtrooper</strong>: "Yes, give me a second, please." <br/>
> <strong>Amiral</strong>: "Why did we lose all our data?" <br/>
> <strong>Stormtrooper</strong>: "Oops, we forgot a zero in rentention.ms." <br/>

---
layout: image-right
image: /assets/img-gen-103.jpeg
---

# What's the problem ?

With Manual Configuration Management

**No versioning** 
  * <span class="text-light">How to keep track of changes over time?</span>

**Non-repeatable** 
  *  <span class="text-light">How to reproduce modifications on multiple environments ?</span>

**No traceability** 
  * <span class="text-light">Who did what and when ?</span>

**No human fault-tolerance**
* <span class="text-light">One typo, and boom!</span>

---
layout: default
class: "text-left"
---

# Hard to Scale! 

Centralized team can quickly become a bottleneck

<img class="logo-center" src="/static/kafka-centralized-team.svg" style="width:80%;height:auto;">

* Creating new topics or requesting access takes hours instead of minutes.

---
layout: two-cols-header
class: "text-left"
---

# The GitOps and IaC Approach

Everything As Code!

::left::

**Synchronize** the desired states (_plan_) of our resources
and configurations with the actual state of our infrastructure from Git.

* Enables a decentralized approach - multiple repositories for each team.
* Shifts responsibilities to development teams.
* Higher autonomy

::right::

<img class="logo-center" src="/static/gitops.svg" style="width:80%;height:auto;">

---
layout: image-right
class: "text-left"
image: /assets/img-gen-106.jpeg
---

# Existing IaC Solutions

Why they don't fit ?

* **[Terraform](https://www.terraform.io/)** <span class="text-light">(or [OpenTofu](https://opentofu.org/))</span>
  * Often preferred by <strong>DevOps</strong> teams, but not as commonly used by development teams.
  * Have to learn HCL - Multiple providers for Kafka
  
* **[Strimzi](https://strimzi.io/)** (Kubernetes Operators) - [Helm](https://helm.sh/)
  * Not everyone runs on Kubernetes, or has the ability to deploy an operator.

Not specialized solutions: no control over the pushed configurations.

---
layout: center
class: text-center
---

# Introducing Jikkou

The Opensource Resource as Code Framework for Apache Kafka®

<img class="logo-center" src="/static/logo-jikkou-title.svg" alt="Jikkou Logo" style="width:25%;height:auto;">

---
layout: two-cols-header
class: "text-left"
---

# What is Jikkou ?

<span class="text-light">Jikkou is a flexible framework enabling developers and Devops teams to efficiently manage, automate and provision all the resources required for their projects.</span> 

::left::

<br />

* Open Source - **Apache License, Version 2.0**.
* Written in Java.
* Declarative (YAML) - Resource as Code.
* Can be easily integrated into a GitOps workflow 
  * [Jikkou GitHub Action](https://github.com/streamthoughts/setup-jikkou)
* Extensible - Developed for **Apache Kafka®**, 
  * but designed for anything!

::right::

<img class="logo-center" src="/static/logo-jikkou-title.svg" alt="Jikkou Logo" style="width:60%;height:auto;">

<div class="quote text-light text-center">Jikkou (jikkō/実行), means "execution (e.g. of a plan), carrying out, (putting into) practice in Japanese.</div>

<style>
.quote {
  font-style: italic;
  font-size: 0.8em;
  margin-top: 1rem;
  margin-bottom: 1rem;
}
</style>

---
layout: center
class: text-center
---

# Jikkou original goal
A modern and intuitive command line client for Apache Kafka.

Jikkou was initially developed as a simple **Command Line Interface (CLI)** to efficiently _**C**reate_, _**R**ead_, 
_**U**pdate_ , _**D**elete_, and version resources such as Topics, ACLs, and Quotas.


```bash
# Installing Jikkou CLI using SDKMAN!
$ sdk install jikkou
```

Available as a **native image** (built with GraalVM) or **Java Binary distribution**.

---
layout: two-cols-header
class: "text-left"
---

# Configuration

HOCON

::left::

```json
# ./application.conf
jikkou {
    extension.providers {
      default.enabled: true
    }

    kafka {
        client {
            bootstrap.servers = "localhost:9092"
            bootstrap.servers = ${?KAFKA_BOOTSTRAP_SERVERS}
        }
    }
}
```

<br />
<br />

<span class="text-light text-small">See: https://github.com/lightbend/config</span>

::right::

**Configure context**

```bash
$ jikkou config set-context localhost \ 
  --config-file "`pwd`/application.conf
```

**Use context**

```bash
$ jikkou config use-context localhost
```

**Display current configuration**

```bash
$ jikkou config view
```

---
layout: image-right
image: /assets/img-gen-107.jpeg
---

# Everything As A Resource

Express the desired state of resources using YAML descriptor files.

```yaml {monaco}
---
# ./my-topic.yaml 
apiVersion: "kafka.jikkou.io/v1beta2"
kind: KafkaTopic
metadata:
  name: 'my-topic'
spec:
  partitions: 3
  replicas: 1
  configs:
    min.insync.replicas: 1
    cleanup.policy: 'delete'
```

<div class="text-small text-light">

* Same resource model as Kubernetes to describe the entities to manage.

</div>

---
layout: two-cols-header
class: text-left
---


# Reconcile

Apply resource changes

::left::

**Multiple reconciliation modes:**

* **`CREATE`**: Create new resource.
* **`UPDATE`**: Create or update existing resources.
* **`DELETE`**: Delete existing resource.
* **`FULL`**: Apply any changes.

<br />
<br />

<div class="text-small text-light">

NOTE: Jikkou supports a `dry-run` mode.

</div>

::right::

**To only display state changes**
```bash
jikkou diff \
--files ./my-topic.yaml \
--selector "metadata.labels.environment IN (demo)"
--output YAML
```

**To only create new resources**
```bash
jikkou create \
--files ./my-topic.yaml \
--selector "metadata.labels.environment IN (demo)"
--output YAML
```

---
layout: default
---

# Apply
Resource State Changes

**(output)**
```yaml
---
kind: "ApiChangeResultList"
apiVersion: "core.jikkou.io/v1"
metadata:
  labels: {}
  annotations:
    jikkou.io/changes-count: 1
dryRun: false
results:
- end: "2023-12-20T00:00:00.000000Z"
  status: "CHANGED"
  description: "Create topic 'my-topic' (partitions=3, replicas=1, configs=[cleanup.policy=delete,min.insync.replicas=1])"
  changed: true
  failed: false
  change:
    apiVersion: "kafka.jikkou.io/v1beta2"
    kind: "KafkaTopicChange"
    metadata:
      name: "my-topic"
      labels:
        environment: "dev"
      annotations:
        jikkou.io/managed-by-location: "./my-topic.yaml"
    spec:
      changes:
      - name: "partitions"
        op: "CREATE"
        after: 3
      - name: "replicas"
        op: "CREATE"
        after: 1
      - name: "config.cleanup.policy"
        op: "CREATE"
        after: "delete"
      - name: "config.min.insync.replicas"
        op: "CREATE"
        after: 1
      op: "CREATE"
      data: {}
```

<style>
pre {
  max-height: 350px;
}
</style>

---
layout: default
class: "text-left"
---

# How It Works ?

Leverage your system as the Source of Truth!

<img class="logo-center" src="/static/jikkou-workflow.svg" style="width:70%;height:auto;">

Jikkou adopts a stateless approach and does not store any state internally.

* Seamless integration with other solutions.


---
layout: two-cols-header
class: "text-left"
---

# Templating

Jikkou provides a simple templating mechanism based-on [Jinjava](https://github.com/HubSpot/jinjava), a [Jinja](https://jinja.palletsprojects.com/en/3.1.x/templates/#base-template) template engine for Java.

::left::

**Template Resource File**
```yaml
# ./kafka-topics.tpl
---
apiVersion: 'kafka.jikkou.io/v1beta2'
kind: 'KafkaTopicList'
items:
{% for country in values.countryCodes %}
- metadata:
    name: "{{ values.topicPrefix}}-iot-events-{{ country }}"
  spec:
    partitions: {{ values.topicConfigs.partitions }}
    replicas: {{ values.topicConfigs.replicas }}
    config:
      retention.ms: 3600000
      max.message.bytes: 20971520
{% endfor %}
```

::right::

**Data Values File**

```yaml
# ./values.yaml
---
topicConfigs:
  partitions: 4
  replicas: 1
topicPrefix: "{{ system.env.TOPIC_PREFIX | default('test', true) }}"
countryCodes:
  - fr
  - uk
  - it
```

**Command**

```bash
#!/bin/bash
jikkou prepare \
--files kafka-topics-template.tpl \
--values-files kafka-topics-values.yaml
```

---
layout: default
class: "text-left"
---

# Validate
Ensure that inbound resources conform to specific rules or constraints.


**Example**: Validate that topic names match a specific regex.

```json
# ./application.conf
jikkou {
  validations = [
    {
      name = "topicMustHaveValidName"
      type = io.streamthoughts.jikkou.kafka.validation.TopicNameRegexValidation
      priority = 100
      config = {
        topicNameRegex = "[a-zA-Z0-9\\._\\-]+"
      }
    }
}
```  
 
---
layout: default
class: "text-left"
---

# Transform
Transform, enrich, or filter inbound resources


**Example:** Enforce a minimum value for the replication factor of kafka topics.

```json
# ./application.conf
jikkou {
  transformations: [
    {
      type = io.streamthoughts.jikkou.kafka.transform.KafkaTopicMinReplicasTransformation
      priority = 100
      config = {
        minReplicationFactor = 3
      }
    }
  ]
}
```

---
layout: default
class: text-left
---

# Actions

Allow a user to execute a specific and one-shot operation on resources.

**Using Jikkou CLI:**

```bash
$ jikkou action <ACTION_NAME> execute [<options>]
```

**Built-in actions:**

* `KafkaConsumerGroupsResetOffsets`
  *  <span class="text-light">Reset offsets of consumer group to earliest, lastest, a specific offset or from datetime.</span>
* `KafkaConnectRestartConnectors` 
  *  <span class="text-light">Restarts all or just the failed Connector and Task instances for one or multiple named connectors.</span>

---
layout: quote
---

# "Ok, it's very cool! But... 
How to use Jikkou if you don't have a direct public access to the your Kafka cluster?"

---
layout: center
class: text-left
---


# Jikkou API Server

A REST interface that makes it easy to manage and automate all your data platform resources.

```bash
$ docker run -it --net host streamthoughts/jikkou-api-server:latest
```

---
layout: center
class: text-left
---


# Jikkou API Server

Usage


![](/static/jikkou-api-server.svg)

---
layout: image-right
image: /assets/img-gen-108.jpeg
---


# Jikkou API Server

Key Benefits

* **Improved Security** :
  * <span class="text-small text-light">Can sit behind your API management platform.</span>
  * <span class="text-small text-light">Provides additional security and auditing capabilities.</span>

* **Centralized Governance** : 
  * <span class="text-small text-light">Acts as a gateway to your data platform.</span>
  * <span class="text-small text-light">Allows to centralize validation/transformation rules to manage resources.</span>

* **Can be extended** : 
  * <span class="text-small text-light">Supports custom resources and extensions.</span>

---
layout: default
class: text-left
---

# REST APIs

Jikkou API Server is built with Micronaut Framework

**Listing resources.**

`GET /apis/{group}/{version}/{plural}`

**Creating resources.**

`POST /apis/{group}/{version}/{plural}/reconcile/mode/{mode}{?dry-run}`

# Security 

* Micronaut Framework supports multiple authentication mechanisms. 
* Jikkou API Server with Basic Authentication, JWT, X.509 Certificate, OAuth2, etc.

---
layout: image-left
image: /assets/img-gen-109.jpeg
---

# Jikkou CLI / Proxy Mode

Do not change your developer experience

```json
jikkou {
  # Proxy Configuration
  proxy {
    # Specify whether proxy mode is enabled (default: false).
    enabled = true
    # URL of the API Server
    url = "http://localhost:28082"
  }
}
```
---
layout: center
image: /assets/img-gen-110.jpeg
---

# DEMO

---
layout: center
class: text-center
---

# Learn More

[Documentations](https://www.jikkou.io/docs/) 
· <carbon-logo-github /> [GitHub](https://github.com/streamthoughts/jikkou) 
· <carbon-logo-medium /> [Blog Posts](https://medium.com/search?q=jikkou+kafka)

---
layout: end
---

# Thank You 

Questions ?

⭐ Star the project on GitHub: https://github.com/streamthoughts/jikkou

<img class="logo-center" src="/static/logo-jikkou-title.svg" alt="Jikkou Logo" style="width:10%;height:auto;">
