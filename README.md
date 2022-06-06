# Mailu-Logging (Kubernetes)
## Background
We will use [filbeat](https://www.elastic.co/beats/filebeat) to push mailu logs to [logstash](https://www.elastic.co/logstash/), which then in turn will push those logs to [Elasticsearch](https://www.elastic.co/elasticsearch/).

What you wish to do with those logs is upto you, but they can be pulled into Kibana or Grafana

## Grafana
Is the whole goal of this, to operate a Mailu Kubernetes deployment with a Grafana dashboard ([11293](https://grafana.com/grafana/dashboards/11293)) 

## Acknowledgements
The bulk of the logstash is from [Bhozar](https://github.com/bhozar) and original work is in this [Github repository](https://github.com/bhozar/grafana-dashboards/tree/master/postfixsmtpemail_opendkim)

## Pre-Requisites
 - Working Elasticsearch deployment (ours is in a monitoring namespace)
 - Working Mailu deployment (ours is in a mailu-mailserver namespace)
 - Mailu deployment can access the hostpath with the logs

## Installation
Within the mailu namespace add the configmaps into Kubernetes, these cover the core setup of filebeat and logstash, with logstash running all the pattern matching for Bhozars work.

The deployment uses volume maps for the configmap mounts and also mounts hostpaths for the Kubernetes logs, so that filebeat can monitor and push them to logstash.

You will need to alter
logstash.conf - Pointing to your Elasticsearch deployment

