# DirectByteBuffer memory leak
Till I read the below articles I do not know that java uses some memory out of the heap memory. Some points
* The JVM does use off-heap memory which is outside of the allocated heap memory space
* But this off-heap usage became more after the introduction of java.nio for supporting the non-blocking IO operation.
* Each thread gets its piece of off-heap memory and will be collected when the corresponding java object is GCd from Heap
* There are many implementation of EventLoop/Event-driven framework ([Grizzly](https://javaee.github.io/grizzly/), [Netty](https://netty.io/) etc) which uses the java.nio non-blocking APIs like Buffers, Channels, Selectors  etc
* This leak will not be detected from HeapDump, this memory limit is at the OS level and the OS will kill process if the off-heap memory consumption is beyond the limit

## Debugging the memory

### Capturing the RSS (Resident State Set) memory

The memory.stat file will contain all the information on the physical memory utilization

```bash
bash$ watch -n 5 'cat /sys/fs/cgroup/memory/memory.stat | grep rss'
```

### Capturing Heap dump

```sh
bash$ jcmd <jpid> GC.heap_dump /tmp/dump.hprof
```
```sh
kubectl exec -it ic-api-intg-dt-8d9db667-6g2sr -c ic-api-intg-dt -n vemohanr -- bash -c "while(true); do jcmd 6 GC.heap_info && date && echo ------------- && sleep 2; done" | tee /scratch/vemohanr/deleteme/heap-info-210903-2.txt
```
```sh
kubectl exec -it ic-api-intg-dt-8d9db667-6g2sr -c ic-api-intg-dt -n vemohanr -- bash -c "while(true); do cat /sys/fs/cgroup/memory/memory.stat | grep rss && date && echo ------------- && sleep 2; done" | tee /scratch/vemohanr/deleteme/rss-210903-2.txt
```

For getting the jpid, try one of the following

```sh
bash$ jps
bash$ ps -aux
```
## Interesting articles which explains it
[https://dzone.com/articles/troubleshooting-problems-with-native-off-heap-memo](https://dzone.com/articles/troubleshooting-problems-with-native-off-heap-memo)

[https://www.evanjones.ca/java-bytebuffer-leak.html](https://www.evanjones.ca/java-bytebuffer-leak.html)