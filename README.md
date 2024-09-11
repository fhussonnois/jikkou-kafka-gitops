# Kafka GitOps : Jikkou & Kestra

## Introduction

**[Jikkou](https://github.com/streamthoughts/jikkou)** (jikkō / 実行) is an open-source tool to help you automate the
management of the configurations that live on your [Apache Kafka]https://kafka.apache.org/documentation/ clusters.

## Prerequisites

* Java
* Docker & Docker Compose
* [yq](https://github.com/mikefarah/yq)
* [jq](https://stedolan.github.io/jq/)

## Getting Started

## Install Jikkou

**First, let's install latest Jikkou release**

```bash
# using SDKMan!
sdk install jikkou
```

````bash
export JIKKOUCONFIG=.jikkou/config.json
source <(jikkou generate-completion)
jikkou --version
````

## Create a Confluent Cloud Cluster

https://login.confluent.io/login

## Export Cluster API key and API Secret

**Create a local `.env` file:**

```bash
#.env
CLUSTER_API_KEY=...
CLUSTER_API_SECRET=...
CLUSTER_BOOTSTRAP_SERVER=...

# add 'KESTRA_' prefix to expose those variables into Kestra
KESTRA_CLUSTER_API_KEY=${CLUSTER_API_KEY}
KESTRA_CLUSTER_API_SECRET=${CLUSTER_API_SECRET}
KESTRA_CLUSTER_BOOTSTRAP_SERVER=${CLUSTER_BOOTSTRAP_SERVER}
```

and

 

```bash
export $(xargs < .env) 
```

## Set configuration context for localhost

```bash
jikkou config set-context confluent --config-file=`pwd`/application.conf
jikkou config use-context confluent
```

```bash
jikkou config view --name confluent
```

## Check if cluster is accessible

```bash
jikkou health get kafka  | yq
```

## Describe Kafka Broker

```bash
jikkou get kafkabrokers | yq
```

## Working with Kafka Topics 

### Create Some Topics

**Display Resource Definition**

```bash
cat ./getstarted/initial-topics.yaml | yq
```

**Create Kafka Topics**

```bash
jikkou apply --files ./getstarted/initial-topics.yaml --selector "metadata.name MATCHES (jikkou-demo-.*)"
```

NOTE: Run the command above a second time to see the behavior of Jikkou

### Delete Topics

**Display Resource Definition**

```bash
cat ./getstarted/remove-topics.yaml | yq
```

**Delete Kafka Topics**

```bash
jikkou apply \
  --files ./getstarted/remove-topics.yaml \
  --selector "metadata.name MATCHES (jikkou-demo-.*)"
```

WARN: When working on a production environment, we highly recommend to always run the apply or delete command with the `--selector` options to make sure to not remove any topics by accident. Furthermore, always run your command in `--dry-run` mode to check for changes that will be executed by Jikkou before proceeding.

### Exploring the use of ConfigMap

**Display Resource Definition**

```bash
cat ./getstarted/topics-configmap.yaml | yq
```

**Validate Resource Definition**

```bash
jikkou validate \
--files ./getstarted/topics-configmap.yaml | yq
```

**Apply Resource Definition**
```bash
jikkou apply \
  --files ./getstarted/topics-configmap.yaml \
 --selector "metadata.name MATCHES (jikkou-demo-.*)"
```

### Exploring the use of Templating

**Display Resource Definition**
```bash
cat ./getstarted/topics-template.tpl
```

**Display Values**
```bash
cat ./getstarted/topics-values.yaml | yq
```

**Validate Resource Definition**
```bash
jikkou validate \
  --files ./getstarted/topics-template.tpl \
  --values-files ./getstarted/topics-values.yaml | yq
```

**Apply Resource Definition**

```bash
export TOPIC_PREFIX=demo 
jikkou apply \
  --files ./getstarted/topics-template.tpl \
  --values-files ./getstarted/topics-values.yaml
```

## Demo #2 - Automate Jikkou with Kestra


```bash
docker compose -f ./docker-compose.yaml up
```



**Update the application.conf**