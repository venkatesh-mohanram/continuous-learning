# Horizontal Pod Autoscaling
Below is the definition file where both metrics on cpu and memory are defined

```yaml
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: api-intg-hpa
  namespace: vemohanr
spec:
  maxReplicas: 5
  minReplicas: 1
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: api-intg
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

## Reference
[https://cloud.google.com/kubernetes-engine/docs/how-to/horizontal-pod-autoscaling#multiple-metrics](https://cloud.google.com/kubernetes-engine/docs/how-to/horizontal-pod-autoscaling#multiple-metrics)