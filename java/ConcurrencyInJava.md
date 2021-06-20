* Each thread shares the process wide resources like memory and file handles
* Each thread has its own program counter, stack, local variables
* Synchronous IO - 
     * Java Servlet hides how it manages the requests and allocates a thread for each request, thus if one thread is blocked, the other thread can execute
     * The problem with Synchronus IO is that there are limitations of the Operating System on how many number of threads can be created per process
* Non Blocking IO - 

* Thread Safety
     * Stateless class - No fields only operations and every state is via local variable only
     * Atomicity - Needs to be taken care in two situations
          1. Check-then-act(if obj null, initialize)
          2. Read-Modify-Write (Incrementing a counter) 
     * Intrinsic Locks - Using a lock object in Synchronized block - mutex
     * Reentrant - The thread which is holding the lock can reenter another critical section that uses the same lock      