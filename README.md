# Single ELK Docker Instance

THIS REPO IS A WORK IN PROGRESS SOME FEATURES MAY NOT QUITE WORK YET.
KNOWN ISSUE IS WITH ELASTALERTS.


This repository is aimed at developers who need an ELK 'stack' on a local machine for testing purposes. It contains the following technology:

**ElasticSearch** is full-text, distributed NoSQL Database and an open-source search engine library. Built by the [Elastic Company](https://github.com/elastic/elasticsearch), and derived from [Apache Lucene](https://lucene.apache.org/). It's the place where your data will be stored, searched and analayzed from.

**Logstash**, is an open-source, server side data processing pipeline built by the [Elastic Company](https://github.com/elastic/logstash). It's intended to recieve data from multiple sources, apply data filtering, mutation, transformation, or enrichment and send it to an ElasticSearch database.

**Kibana** is an open-source data visualization & dashboard engine for ElasticSearch. Built by the [Elastic Company](https://github.com/elastic/kibana).

**Beats**, are lightweight data shippers. We will be using **Filebeat** which is specifically aimed at structured or unstructured log files. Built by the [Elastic Company](https://github.com/elastic/beats).

**Elastalert**, is a third-party alerting & monitoring plug-in for ElasticSearch. Originally developed by[yelp](https://github.com/Yelp/elastalert) and modified by [BitSensor](https://github.com/bitsensor/elastalert).

## Dependencies
* Python3
* PIP3
* [docker-compose]https://pypi.org/project/docker-compose/
* [Docker](https://www.docker.com/products/docker-desktop) Engine 19.03.0 or greater
* [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) 2.9 or greater

## Getting Started

From your terminal or console, clone this repository. 
```console
git clone https://github.com/injectedfusion/single-elk-docker-instance.git
```
Take a moment to familarize yourself with the project directory.

```
.
├── LICENSE
├── README.md
├── config
│   ├── config-hisoric-data-example.json
│   ├── config-local-elastalert-installation.json
│   ├── config.json
│   ├── elastalert-test.yaml
│   ├── elastalert.yaml
│   └── elastalert.yml
├── docker-compose.yml
├── elastalert-server-config.json
├── elastalert-test.yaml
├── elastalert.yml
├── elasticsearch.yml
├── filebeat.yml
├── hosts
├── kibana.yml
├── log
│   └── apache_logs.log
├── logstashsettings
│   ├── log4j2.properties
│   └── logstash.yml
├── pipeline
│   └── logstash.conf
├── project_build.yml
├── rule_templates
│   ├── detection_template.yaml
│   ├── error_jira_template.yaml
│   ├── integration_started_template.yaml
│   ├── no_data_template.yaml
│   ├── relevant_attack_template.yaml
│   ├── spike_template.yml
│   ├── successful_attack_template.yaml
│   ├── threshold_template.yml
│   └── volumetric_alert_template.yaml
└── rules
    └── test-query-rule.yml
```

For your convienence a `log` directory has been created for you, where you can simply drop any log data you wish to ingest.

> Note: file extensions dropped in the log directory must end in `.log`

## Usage:

Verify we have pulled down the correct docker images.

```
docker images
```
The images we wish to validate are:

``` console
REPOSITORY             TAG                 IMAGE ID            CREATED             SIZE
logstash               7.7.0               30dcca1db5e9        5 days ago          740MB
kibana                 7.7.0               eadc7b3d59dd        5 days ago          1.15GB
elasticsearch          7.7.0               7ec4f35ab452        6 days ago          757MB
elastic/filebeat       7.7.0               96cc9145e919        6 days ago          408MB
bitsensor/elastalert   latest              f18338c0610a        12 months ago       247MB
```

