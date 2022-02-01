# Network Policies
Network policy with the K8S is useful to restrict and streamline the ingress and egress rules. For this we have resource type called networkpolicy

The policy supports definition by
* Namespace Selector
* Pod Selector
* IP addresses

But *one* thing to keep in mind is that the above is the AND condition, the ingress or egress will be allowed only when all the condition defined are met

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:  
  name: ingress-policy
  namespace: backend
spec:
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          backend-client: "true"
      podSelector:
        matchLabels:
          backend-client: "true"
  podSelector:
    matchLabels:
      backend-service: "true"
  policyTypes:
  - Ingress
```

In the above example, the traffic will be accepted by the POD having label as *backend-service: "true"* only when it comes from the namespace having the label *backend-client: "true"* and the pod within that namespace having the label *backend-client: "true"*