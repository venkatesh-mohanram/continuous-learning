# Accessing kube-apiserver from a running POD
Rarely we want our POD to talk to the kube-apiserver to fetch details about the other deployments, pod status etc. This is not a common usecase but the option provided by K8S can be used in a very creative way to solve problem when a running pod want to know information about the cluster

The logic is very simple, we use the * kubectl * command to talk to the kube-apiserver and access the cluster  