## ResourceQuota
Kubernetes provides a configuration which restrict CPU share per namespace

### Get the quota
```shell script
kubectl get resourcequota --namespace=vemohanr --output=yaml
``` 
This will return what the current quota and how much is utilized with hard and soft limits
```shell script
vemohanr@VEMOHANR-IN:~$ kubectl get resourcequota --namespace=vemohanr --output=yaml
apiVersion: v1
items:
- apiVersion: v1
  kind: ResourceQuota
  metadata:
    creationTimestamp: "2020-04-15T16:27:22Z"
    name: resource-quota
    namespace: vemohanr
    resourceVersion: "16704897"
    selfLink: /api/v1/namespaces/vemohanr/resourcequotas/resource-quota
    uid: 0ec9c08c-f1d3-4056-a495-42d12d218835
  spec:
    hard:
      requests.cpu: "2"
  status:
    hard:
      requests.cpu: "2"
    used:
      requests.cpu: "2"
kind: List
metadata:
  resourceVersion: ""
  selfLink: ""
```
### Editing the quota
```shell script
kubectl edit ResourceQuota/resource-quota --namespace=vemohanr
```
This will open the yaml file in a editor and we can edit and save the file.

In general we can edit any kubernetes resource using the <b><i>kubectl edit</i></b> command like below

```shell script
kubectl edit <ResourceType/ResourceName>
``` 

## References
https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#edit
