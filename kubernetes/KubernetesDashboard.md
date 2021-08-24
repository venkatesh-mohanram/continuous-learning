# Kubernetes Dashboard
We can perform all actions to the kubernetes cluster using the *kubectl* command but sometime using the graphical interface will be helpful

1 One line execution to install dashboard into the kubernetes cluster

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.3.1/aio/deploy/recommended.yaml 
```
2 If the cluster is not having permission to pull image from the docker.io registry then we need to pull the following image and push it to the organization docker registry

```basg
docker pull kubernetesui/metrics-scraper:v1.0.6
docker pull kubernetesui/dashboard:v2.3.1
```
3 Create service account, cluster role binding

```bash
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
EOF
```

4 Create Secret

```bash
kubectl -n kubernetes-dashboard get secret $(kubectl -n kubernetes-dashboard get sa/admin-user -o jsonpath="{.secrets[0].name}") -o go-template="{{.data.token | base64decode}}"
```

5 Launch the dashboard

```bash
kubectl proxy
```
6 Open the URL in the browser

```bash
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
```

### References
[https://github.com/kubernetes/dashboard](https://github.com/kubernetes/dashboard)