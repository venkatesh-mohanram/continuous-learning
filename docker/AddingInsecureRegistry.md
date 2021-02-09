# Insecure registry
For some reason if we cannot talk to the docker registry using a secured SSL/TLS channel then we can follow the approach to talk to a docker registry in insecured manner. 

Most of the times, the usecases might be like
1. We want to push images to a docker registry hosted by a colleague who is also in same network
2. Wanted to use the docker registry hosted by the company and wanted to bypass SSL connection and the need of certificate etc

## Steps 

1. Create a file /etc/docker/daemon.json
	This file contains system independent configuration details except for the HTTP Proxy details
2. Add below entry into it

```
{  
  "insecure-registries": ["host:5000"]
}

```
3. Ensure the directory exists
4. Restart the docker daemon

```
[root@slc10vhh vemohanr]# systemctl daemon-reload
[root@slc10vhh vemohanr]# systemctl restart docker
```

Reference: [https://docs.docker.com/registry/insecure/](https://docs.docker.com/registry/insecure/)