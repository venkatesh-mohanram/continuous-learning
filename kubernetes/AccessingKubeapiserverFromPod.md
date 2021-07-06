# Accessing kube-apiserver from a running pod / Doing a kubectl from a pod
Rarely we want our POD to talk to the kube-apiserver to fetch details about the other deployments, pod status etc. This is not a common usecase but the option provided by K8S can be used in a very creative way to solve problem when a running pod want to know information about the cluster

The logic is very simple, we use the ** kubectl ** command to talk to the kube-apiserver and access the cluster, the kubectl client maintains the details about the cluster in ~/.kube/config directory. And if we want to access the same from the pod then even the pod should contain all the configurations about the cluster so it can access the kube-apiserver

The good news is when kubernetes brings up the pod it mounts all the necessary folder that contains configuration, certificate etc and it will have one default [service account](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-serviceaccount-em-) attached to the pod. The default service account is authorized to access only a very limited resouce from kube-apiserver

We can create a new service account and authorize it to access additional resources by creating the following items

1. [ServiceAccount](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-serviceaccount-em-)
2. [ClusterRole](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-clusterrole-em-) / [Role](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-role-em-)
3. [ClusterRoleBinding](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-clusterrolebinding-em-) / [RoleBinding](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-rolebinding-em-)

Choosing between Role and ClusterRole depends on whether we want to access resource at own namespace only or we need access resources cluster-wide 

## Usecase: Getting the deployment details from the POD

In this usecase, we are trying to read all the deployments available in the same namespace where the POD is running 
 
### Service Account

The first step is to create the service account, it is like a user which we will bind to the role and use it in the deployment/pod

```sh
kubectl create sa apps-sa -n vemohanr --dry-run -o yaml
```

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  creationTimestamp: null
  name: apps-sa
  namespace: vemohanr
```

### Role

We can create one role mentioning about all the resources we need to access or we can create one role per resource.  

```sh
kubectl create role deployment-reader --verb=list,get --resource=deployment -n vemohanr --dry-run -o yaml
```

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  creationTimestamp: null
  name: deployment-reader
rules:
- apiGroups:
  - apps
  resources:
  - deployments
  verbs:
  - list
  - get
```

### Role Binding

Resource binding is the place where we will tie the service account with the role

```sh
kubectl create rolebinding apps-sa-deployment-reader --serviceaccount=vemohanr:apps-sa --role=deployment-reader -n vemohanr --dry-run -o yaml
```

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  creationTimestamp: null
  name: apps-sa-deployment-reader
  namespace: vemohanr
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: deployment-reader
subjects:
- kind: ServiceAccount
  name: apps-sa
  namespace: vemohanr
```

### Attach the Service Account to the POD

We need to attach the service account with the deployment so it will get granted access based on the role it is binded with

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: ubuntu
  name: ubuntu
  namespace: vemohanr
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ubuntu
  template:
    metadata:
      labels:
        app: ubuntu
    spec:
      serviceAccountName: apps-sa
      containers:
      - image: iad.ocir.io/paasdevoic/vemohanr/ubuntu:latest
        name: ubuntu
        command:
        - "sh"
        - "-c"
        - "sleep 10000"
      imagePullSecrets:
      - name: ocirsecret
```

### Quick Testing

For quick testing we can get inside this ubuntu POD and execute the curl command

```sh
$ kubectl exec -it ubuntu-5d8cc9cfdf-cxzls -n vemohanr -- sh
$ APISERVER=https://kubernetes.default.svc
$ SERVICEACCOUNT=/var/run/secrets/kubernetes.io/serviceaccount
$ NAMESPACE=$(cat ${SERVICEACCOUNT}/namespace)
$ TOKEN=$(cat ${SERVICEACCOUNT}/token)
$ CACERT=${SERVICEACCOUNT}/ca.crt
$ CACERT=${SERVICEACCOUNT}/ca.crt
$ curl --cacert ${CACERT} --header "Authorization: Bearer ${TOKEN}" -X GET ${APISERVER}/api/apis/apps/v1/deployments
```

### Client Libraries

There are client libraries available in most of the language and we can get info about it from [https://kubernetes.io/docs/reference/using-api/client-libraries/](https://kubernetes.io/docs/reference/using-api/client-libraries/) 

## Reference

[https://kubernetes.io/docs/tasks/run-application/access-api-from-pod/](https://kubernetes.io/docs/tasks/run-application/access-api-from-pod/)
[https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)



  