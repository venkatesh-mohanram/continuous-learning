# Grep Image Tags
Here is a small sequence of commands separated by pipe to get the list of the <b><i>docker image:tag</i></b> used by the microservices

```shell script
$ kubectl get pods -n vemohanr | awk '{print $1}' |  kubectl describe pod $1 -n vemohanr | grep Image: | grep -v istio
```
And the output will look like below

```shell script
    Image:          iad.ocir.io/frontend-service:2020.4.28
    Image:          iad.ocir.io/db-service:2020.4.28
    Image:         iad.ocir.io/kafka:5.4.1
    Image:          iad.ocir.io/elasticsearch:7.7.0
    Image:         iad.ocir.io/redis:5.0.8    
```

Recently learned one more trick with wide output which can give the image tag for the deployments

```
$ kubecel get deployment --output wide
```
and the output contains the below

```
NAME             READY   UP-TO-DATE   AVAILABLE   AGE    CONTAINERS       IMAGES                                                      SELECTOR
frontend-service   1/1     1            1           106m   frontend-service   iad.ocir.io/frontend-service:2020.4.28   app=frontend-service
db-service         1/1     1            1           106m   db-service    iad.ocir.io/db-service:2020.4.28              app=db-service
kafka              1/1     1            1           106m   kafka         iad.ocir.io/kafka:5.4.1                       app=kafka
elasticsearch      1/1     1            1           106m   elasticsearch iad.ocir.io/elasticsearch:7.7.0              app=elasticsearch
redis              1/1     1            1           106m   redis         iad.ocir.io/redis:5.0.8                       app=redis
```
 