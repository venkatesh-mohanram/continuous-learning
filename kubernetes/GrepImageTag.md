# Grep Image Tags
Here is a small sequence of commands separated by pipe to get the list of the <b><i>docker image:tag</i></b> used by the microservices

```shell script
kubectl get pods -n vemohanr | awk '{print $1}' |  kubectl describe pod $1 -n vemohanr | grep Image: | grep -v istio
```
And the output will look like below
```shell script
    Image:          iad.ocir.io/frontend-service:2020.4.28
    Image:          iad.ocir.io/db-service:2020.4.28
    Image:         iad.ocir.io/kafka:5.4.1
    Image:          iad.ocir.io/elasticsearch:7.7.0
    Image:         iad.ocir.io/redis:5.0.8    
```
 