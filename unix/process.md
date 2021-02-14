# ps
The ps or process status command is a very frequently used command but still it has lots of option which we will forget 

## To list all the process including the daemon
This command basically lists the process started by the terminal tty and started as a daemon

```
ps -x
```
Along with that we can use grep command to filter out the PID of a particular process

```
ps -x | grep kubelet
```