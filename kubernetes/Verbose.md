# Debugging kubectl command
If we want to debug what's going behind the kubectl command execution then we can add the additional verbose level along with other arguments in the command

This will help in cases when there is error returned and the error is very abstract. It also prints which .kube/config file it is referring to.

<i>Example</i>

```
kubectl get namespaces --v=8

```
and below will be the output

```
[slc10vhh-~] bash$ kubectl get namespaces --v=8
I0121 03:36:12.698234   20490 loader.go:375] Config loaded from file:  /home/vemohanr/.kube/config
I0121 03:36:12.703299   20490 round_trippers.go:420] GET https://:6443/api?timeout=32s
I0121 03:36:12.703530   20490 round_trippers.go:427] Request Headers:
I0121 03:36:12.703696   20490 round_trippers.go:431]     Accept: application/json, */*
I0121 03:36:12.703869   20490 round_trippers.go:431]     User-Agent: kubectl/v1.17.4 (linux/amd64) kubernetes/8d8aa39
W0121 03:36:44.703531   20490 transport.go:243] Unable to cancel request for *exec.roundTripper
I0121 03:36:44.706330   20490 round_trippers.go:446] Response Status:  in 32002 milliseconds
I0121 03:36:44.706388   20490 round_trippers.go:449] Response Headers:
I0121 03:36:44.706444   20490 cached_discovery.go:121] skipped caching discovery info due to Get https://:6443/api?timeout=32s: context deadline exceeded (Client.Timeout exceeded while awaiting headers)
```

There are also multiple different verbose level we can set and more information in [https://kubernetes.io/docs/reference/kubectl/cheatsheet/#kubectl-output-verbosity-and-debugging](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#kubectl-output-verbosity-and-debugging) 
