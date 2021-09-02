# Getting into the running container
Sometimes we want to get into the running container to see some files inside it like some configuration settings or to modify something. And it is easy with kubeneteres *exec* command

```shell script
kubectl exec -it frontend-service sh
```
The last argument can be any executables that are available in the container's $PATH variable, more often we want to use the *sh* or *bash*

```shell script
sh-4.2#       
```
Inside the shell script we can type in any command the container supports, cat the file content etc.,

If we want to run the command as it is without getting inside the container then we can do the following

```sh
[slc10vhh-~] bash$ kubectl exec -it frontend-service -- bash -c "cat /sys/fs/cgroup/memory/memory.stat | grep rss"
rss 2062966784
rss_huge 1910505472
total_rss 2062966784
total_rss_huge 1910505472
```
 