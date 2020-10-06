# Storage directory
The default storage directory for images, containers etc used by the docker daemon is '/var/lib/docker/tmp/'. Sometimes the storage within the system may not be enough and we prefer to change it to some other mounts

1. Create a file /etc/docker/daemon.json
	This file contains system independent configuration details except for the HTTP Proxy details
2. Add below entry into it

```
{
  "data-root" : "/mnt/vemohanr/soft/docker-data",
  "storage-driver" : "overlay2"
}
```
3. Ensure the directory exists
4. Restart the docker daemon

```
[root@slc10vhh vemohanr]# systemctl daemon-reload
[root@slc10vhh vemohanr]# systemctl restart docker
```

Reference: [https://docs.docker.com/config/daemon/systemd/#runtime-directory-and-storage-driver](https://docs.docker.com/config/daemon/systemd/#runtime-directory-and-storage-driver)