# Service Account verification using REST API
Service Account in K8S is used to invoke all the k8s admin server APIs within the POD provided the service account is granted with necessary RBAC permissions via role-binding or cluster-role-binding

The recommended way to invoke the K8S API from the POD is to use the official client libraries. However if we want to make a quick testing of service account configuration then we can use the K8S REST APIs to invoke and check whether the POD is having sufficient privilage to access the resources or not.

Before going to steps of invoking the REST API, few lines about how the POD gets that privilage. When a deployment/pod is binded with a service account, the POD will get the *certficate*, *token* and *namespace* in the location <code>/var/run/secrets/kubernetes.io/serviceaccount</code>

```shell
$ kubectl exec backend-api-b874f697f-fgqk7 -c backend-api -n vemohanr -- cat /var/run/secrets/kubernetes.io/serviceaccount/token
```

On executing the above command we would get the token I we can use to invoke the REST API, and now we can use the above token and form the curl command

```shell
$ kubectl exec backend-api-b874f697f-fgqk7 -c backend-api -n vemohanr -- curl -k -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6Ikd6VFI0R3g2RW9tckNwbnhMOE5oWDlLc2ZEMVRUZU1qVExXbktkVlh2YW8ifQ.eyJhdWQiOlsiYXBpIl0sImV4cCI6MTY5NDU2MjE3MiwiaWF0IjoxNjYzMDI2MTcyLCJpc3MiOiJodHRwczovL2t1YmVybmV0ZXMuZGVmYXVsdC5zdmMuY2x1c3Rlci5sb2NhbCIsImt1YmVybmV0ZXMuaW8iOnsibmFtZXNwYWNlIjoidmVtb2hhbnIiLCJwb2QiOnsibmFtZSI6ImljLWFwaS1pbnRnLWR0LWI4NzRmNjk3Zi1mZ3FrNyIsInVpZCI6ImI4OWE4MGJlLWYwZGUtNGFlZi1iODBiLWRlYWQ3ZDc2YzVhMSJ9LCJzZXJ2aWNlYWNjb3VudCI6eyJuYW1lIjoiYXBwcy1zYSIsInVpZCI6ImFmZjRiNGU5LTY4ZTEtNDY0ZS1iZGJhLTQxMTYzOTIxMWM1NyJ9LCJ3YXJuYWZ0ZXIiOjE2NjMwMjk3Nzl9LCJuYmYiOjE2NjMwMjYxNzIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDp2ZW1vaGFucjphcHBzLXNhIn0.Lp_FOzcCz19KLwTm4qU_VHOjqpM9M6wSpPAfGWZQQyjFz276xLBEYU22dwaFcuHkOXw83S1xy0rWAAhgvkaWFmpLwuC9GxlMh583XJo1b1GC-BIei_EgzdTrD3TFOtQ9CCTC4Jf0FWmmY5Uz5ng5xglLbw7220YsRIG9NIj1PkfBfVJCVrezE-wXyNb4jkr86wlNz3uKhYw8FdIffUuOyXpNfTt1IyOkGnQGtow_E3F5asqO7ZlaB6DjUJBZhwgP90SqAmpVyu10hTELNLchV-NeTtyQJEHIbLqZj64wJb3SrBqenHft_g_2SRivoMzDoDQUFtk_N3HHNdpHDfEC7A" https://147.154.106.173:6443/apis/apps/v1/namespaces/vemohanr/cronjobs
```

If want to know what is the K8S admin API server IP etc, execute the below command to get it

```shell
$ kubectl cluster-info
Kubernetes master is running at https://147.154.106.173:6443
CoreDNS is running at https://147.154.106.173:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
kubedashboard-kubernetes-dashboard is running at https://147.154.106.173:6443/api/v1/namespaces/kube-system/services/https:kubedashboard-kubernetes-dashboard:https/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

## References
[https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.25/#-strong-api-overview-strong-](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.25/#-strong-api-overview-strong-)
[https://www.ibm.com/docs/en/cloud-paks/cp-management/2.0.0?topic=kubectl-using-service-account-tokens-connect-api-server](https://www.ibm.com/docs/en/cloud-paks/cp-management/2.0.0?topic=kubectl-using-service-account-tokens-connect-api-server)
[Acc](AccessingKubeapiserverFromPod.md)