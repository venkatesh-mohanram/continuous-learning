# Container logs
It is natural to look for logs logged by the container to debug whether the requests are serviced correctly or where the failure is etc

And Kubernetes provides command to get the log from the container

## Getting from a single POD

The below command will help to get the log from a particular POD 

```
$ kubectl logs -f <pod_name> -n <namespace>
```

If we have multiple replicas and we want to see the logs from all the replicas then we can use the label argument in the above command

```
kubectl logs -f -l <app=ic-api-home> --all-containers -n <namespace>
```

## Useful links
* Kubernetes cheat sheet : [https://kubernetes.io/docs/reference/kubectl/cheatsheet/#interacting-with-running-pods](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#interacting-with-running-pods)
* There is another opensource tool called stern which does a great job [https://github.com/wercker/stern](https://github.com/wercker/stern)