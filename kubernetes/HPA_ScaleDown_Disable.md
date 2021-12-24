# HPA Scale Down disable
If we want to disable the scale down then we can do the below behavior configuration. Common reason to disable the scale down is the microservice is storing the session information, in an ideal world the microservice should be stateless though!

```sh
$ kubectl edit hpa.v2beta2.autoscaling api-backend-hpa
```

```yaml
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: api-backend-hpa
  namespace: vemohanr
spec:
  behavior:
    scaleDown:
      policies:
      - periodSeconds: 15
        type: Percent
        value: 100
      selectPolicy: Disabled
    scaleUp:
      policies:
      - periodSeconds: 15
        type: Pods
        value: 4
      - periodSeconds: 15
        type: Percent
        value: 100
      selectPolicy: Max
      stabilizationWindowSeconds: 0  
  maxReplicas: 7
  minReplicas: 2
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: api-backend
  metrics:
  - type: Resource
    resource:
      name: memory
      target:
        type: AverageValue
        averageValue: 2000Mi
  - type: Resource
    resource:
      name: cpu
      target:
        type: AverageValue
        averageValue: 850m

```
