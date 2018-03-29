# Curator

This is a dockerized version of the Elasticsearch Curator tool, to be used to
manage indicies.

For further details see:

https://github.com/elastic/curator


## Usage Examples

### Kubernetes

An example setup which creates a Kubernetes job to run daily and delete 
`filebeat-` and `logstash-` indices older than 14 days is included in
`examples/kubernetes`.

Modify the example `config.yaml` with your configuration options.

Create a ConfigMap to hold the configuration and action files

```
kubectl create configmap curator --from-file=delete-indices=./examples/kubernetes/delete-indices --from-file=config.yaml=./examples/kubernetes/config.yaml
```

Then create the job which will use this ConfigMap

```
kubectl apply -f ./examples/kubernetes/curator-job.yaml
```