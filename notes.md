## Chapter 3
### Practice Exercise 
#### 3.1-3.7
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/3.pdf
#### 3.8
https://www.tutorialspoint.com/actions-taken-by-a-kernel-to-context-switch-between-processes
#### 3.11
https://stackoverflow.com/questions/20028026/os-how-many-process-are-created-by-the-program
#### 3.12
https://stackoverflow.com/questions/19804016/child-and-relation-with-fork
#### 3.13
https://stackoverflow.com/questions/32773545/process-ids-and-fork
#### 3.14
* Ordinary pipes: communication between parent and child process with less overhead.
* Named pipes: communication between different machine via TCP/IP, or between processes without specific relationship.
#### 3.15
If an RPC mechanism cannot support either at most once or at least once semantics then the RPC can fail or be duplicated and executed more than once as a result of common network errors. So the RPC server cannot guarantee that a remote procedure will be invoked correctly and executed only once. This two semantics is not required for simple querying static data without involving time-sensitive or altering data.
#### 3.16
CHILD: 0 CHILD: -1 CHILD: -4 CHILD: -9 CHILD: -16 PARENT: 0 PARENT: 1 PARENT: 2 PARENT: 3 PARENT: 4
> stack and heap are copied for newly created process)
#### 3.17
https://www.coursehero.com/file/p64lasoq/What-are-the-benefits-and-the-disadvantages-of-each-of-the-following-Consider/
##### a. Synchronous and asynchronous communication
For system level, synchronous communication allows a rendezvous between the sender and receiver and is more efficient because it will block until the message is available, the disadvantage will be blocking the process if the message is fail. Asynchronous is nonblocking communication that is easier to code for programmer level, but less efficient.
##### b. Automatic and explicit buffering
automatic buffer does not limit the size of the message queue, so for the programmer sender will not be blocked because to code but might be not memory efficient for system. Explicit buffering is complxer to code but can safe more space for the system.
##### c. Send by copy and send by reference
send by copy is suitable for short message or simple parameters and won't affect other process's data. send by reference can safe the effort of copying data but should careful of multiple process changing the same data causing wrong result. Send by reference allow the receiver to alter the state of parameter so it allows programmer to write a distributed version of centralized application. Java’sRMI provides both; however, passing a parameter by reference requires declaring the parameter as a remote object as well.
##### d. Fixed-sized and variable-sized messages
The number of Fixed-sized message in a queue is known, and fixed sized message is easier for parsing and for remote communication, variable-sized message is less efficient for communication so it can be send by shared memory for large sized message.
### Programming Problems
#### 3.18
https://www.geeksforgeeks.org/zombie-and-orphan-processes-in-c/
> the child finishes its execution using `exit()` system call while the parent sleeps for 50 seconds, hence doesn’t call `wait()` and the child process’s entry still exists in the process table.
#### 3.20
https://stackoverflow.com/questions/29285913/api-for-obtaining-and-releasing-a-pid
#### 3.21-3.22
https://zhuanlan.zhihu.com/p/80883605
#### 3.24
https://brainly.com/question/15461989
#### 3.25
https://github.com/stemmlerjs/os-design-assign-2/blob/master/Part%201/Server/src/assignment2/EchoServer.java
#### 3.26
https://www.geeksforgeeks.org/c-program-demonstrate-fork-and-pipe/
#### 3.27
https://github.com/manojkmeena/OS-Project/blob/master/Question%2026%20-%20Design%20a%20file-copying%20program%20named%20filecopy%20using%20ordinary%20pipes.%20This%20program%20will%20be%20passed%20two%20parameters:%20the%20name%20of%20the%20file%20to%20be%20copied%20and%20the%20name%20of%20the%20copied%20file.%20The%20program%20will%20then%20create%20an%20ordinary%20pipe%20and%20write%20the%20contents%20of%20the%20file%20to%20be%20copied%20to%20the%20pipe.%20The%20child%20process%20will%20read%20this%20file%20from%20the%20pipe%20and%20write%20it%20to%20the%20destination%20file.%20For%20example%2C%20if%20we%20invoke%20the%20program%20as%20follows:%20filecopy%20input.txt%20copy.txt%20The%20file%20input.txt%20will%20be%20written%20to%20the%20pipe.%20The%20child%20process%20will%20read%20the%20contents%20of%20this%20file%20and%20write%20it%20to%20the%20destination%20file%20copy.txt.
## Chapter 4
### Practice Exercise
#### 4.1-4.7 
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/4.pdf
#### 4.8 For sequencial or trivial process, or embedded process which sigle core, the extra work needed by multithreading such as swapping context would cost more resource hence slower than single thread.
#### 4.9
When there are multiple task that can run independently and not need to wait for each other, or switching available core to prevent the process blocked by some task, multithreaded solution using multiple kernel threads provide better performance than a single-threaded solution on a single-processor system. Exmaple including web server dealing with many user requests, and processes that can be done with recursive devide-and-conquer like manipulating files, matrix calculations.
#### 4.10 Heap memory is shared across threads, global variables depends on operating system.
A thread is a basic unit of CPU utilization; it comprises a thread ID , a program counter (PC ), a register set, and a stack. It shares with other threads belonging to the same process its code section, data section, and other operating-system resources, such as open files and signals.
For POSIX and Windows threading, any data declared globally—that is, declared outside of any function—are shared among all threads belonging to
the same process. Because Java has no equivalent notion of global data, access to shared data must be explicitly arranged between threads.
#### 4.11 
When a OS use many-to-one model, the entire process will block if a thread makes a blocking system call, hence unable to take advantage of multiple processing cores. With one-to-one or many-to-many mapping model, in the multithreading solution works better scenario, a multithreaded solution using multiple user-level threads achieve better performance on a multiprocessor system than on a single-processor system.
#### 4.12-4-14, 4.18, 4,19, 4.21
https://github.com/Criviere/os/blob/master/Chapter4.md
#### 4.15
Determine if the following problems exhibit task or data parallelism:
> Data parallelism distributes subsets of the same data across different computing cores and performs the same operation on each core. Task paral-
lelism distributes not data but tasks across multiple cores. Each task is running a unique operation
* Using a separate thread to generate a thumbnail for each photo in a collection - data parallelism
* Transposing a matrix in parallel - data parallelism
* A networked application where one thread reads from the network and another writes to the network - task parallelism
* The fork-join array summation application described in Section 4.5.2 - data parallelism
* The Grand Central Dispatch system - task parallelism
#### 4.16 - 4.17
http://mjgeiger.github.io/OS/prev/sp17/homework/OSsp17_hw2_soln.pdf
#### 4.20
https://blog.xuite.net/pero.pero1/pero/4771524#
### Programming Problems
#### 4.22
https://github.com/SeanStaz/statisticsCalculator_Multithreaded.c/blob/master/pthreads.c
#### 4.23
https://github.com/UnJaw/Programming_HW0/blob/master/Prime.java
#### 4.24
https://github.com/SeanStaz/monteCarloMethod.c/blob/master/A3.c
#### 4.25
https://codereview.stackexchange.com/questions/256274/calculating-pi-with-monte-carlo-using-openmp
#### 4.26
https://www.geeksforgeeks.org/introducing-threads-socket-programming-java/
#### 4.28
create a thread[100], each thread[i] create a thread called `allocating_pid()` and than `sleep()`, finally call `release_pid()`, and `join()` thread[i] in the for loop.
#### 4.29
https://stackoverflow.com/questions/66996996/how-do-i-get-my-multithreaded-server-client-chat-program-to-echo-messages-to-all
## Chpater 5
### Practice Exercises
#### 5.1-5.10 https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/5.pdf
#### 5.12
* CPU utilization and response time: CPU utilization is increased if the overheads associated with context switching is minimized. The context switching overheads could be lowered by performing context switches infrequently. This could, however, result in increasing the response time for processes.
* Average turnaround time and maximum waiting time: Average turnaround time is minimized by executing the SJF. Such a scheduling policy could, however, starve long-running tasks and thereby increase their waiting time.
* I/O device utilization and CPU utilization: CPU utilization is maximized by running long-running CPU-bound tasks without performing context switches. I/O device utilization is maximized by scheduling I/O-bound jobs as soon as they become ready to run, thereby incurring the overheads of context switches.
#### 5.13
By assigning more lottery tickets to higher-priority processes.
#### 5.14
The primary advantage of each processing core having its own run queue is that there is no contention over a single run queue when the scheduler is running concurrently on 2 or more processors. When a scheduling decision must be made for a processing core, the scheduler only need to look no further than its private run queue. A disadvantage of a single run queue is that it must be protected with locks to prevent a race condition and a processing core may be available to run a thread, yet it must first acquire the lock to retrieve the thread from the single queue. However, load balancing would likely not be an
issue with a single run queue, whereas when each processing core has its own run queue, there must be some sort of load balancing between the different run queues.
#### 5.15
When α = 0 and τ0 = 100 milliseconds, the formula always makes a prediction of 100 milliseconds for the next CPU burst. When α = 0.99 and τ0 = 10 milliseconds, the most recent behavior of the process is given much higher weight than the past history associated with the process. Consequently, the scheduling algorithm is almost memoryless, and simply predicts the length of the previous burst for the next quantum of CPU execution.
#### 5.16
This scheduler would favor CPU-bound processes as they are rewarded with a longer time quantum as well as priority boost whenever they consume an entire time quantum. This scheduler does not penalize I/O-bound processes as they are likely to block for I/O before consuming their entire time quantum, but their priority remains the same.
#### 5.17
* Gantt charts

FCFS | p1 t = 5| p2 t = 8| p3 t = 9 | p4 t = 16 | p5 t = 20 |
--- | --- | --- | --- |--- |---

SJF | p3 t = 1 | p2 t = 4 | p5 t = 8 | p1 t = 13 | p4 t = 20 |
--- | --- | --- | --- |--- |---

non-preemptive priority | p1 t = 5 | p5 t = 9 | p3 t = 10 | p4 t = 17 | p2 t = 20 |
--- | --- | --- | --- |--- |---

RR | p1 t = 2 | p2 t = 4 | p3 t = 5 | p4 t = 7 | p5 t = 9 | p1 t = 11 | p2 t = 12 | p4 t = 14 | p5 t = 16 | p1 t = 17 | p4 t = 20|
--- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---
* turnaround time

--- | FCFS | SJF | non-preemptive priority | RR |
---|---|---|---|---
p1 | 5 | 13| 5 | 17|
p2 | 8 | 4 | 20| 12|
p3 | 9 | 1 | 10| 5 |
p4 | 16| 20| 17| 20|
p5 | 20| 8 | 9 | 16|
* waiting time

--- | FCFS | SJF | non-preemptive priority | RR |
---|---|---|---|---
p1 | 0 | 8 | 0 | 12|
p2 | 5 | 1 | 17| 9 |
p3 | 8 | 0 | 9 | 4 |
p4 | 9 | 13| 10| 11|
p5 | 16| 4 | 5 | 12|
* SJF
#### 5.18
* Gantt chart

p1 t = 15 | p2 t = 20 | p3 t = 30 | p4 t = 40 | p3 t = 45 | p5 t = 50 | p3 t = 55 | p6 t = 70 | p4 t = 80 | p2 t = 95
---|---|---|---|---|---|---|---|---|---
* turnaround time: p1 = 15, p2 = 95, p3 = 35, p4 = 55, p5 = 5, p6 = 15
* waiting time: p1 = 0, p2 = 75, p3 = 20, p4 = 35, p5 = 0
#### 5.19
Nice values < 0 are assigned a higher relative priority and such systems may not allow non-root processes to assign themselves higher priorities.
#### 5.20
Shortest job first and Priority algorithm could result in starvation.
#### 5.21
* (a) The process with two pointers will run twice more often than other process.
* (b) Advantages: 1. allowing user prioritize process while preventing starvation. 2. the algorithm need not change. Disadvantage: 1. Context switching will now have a larger effect than it did before. 2. Removing processes from the running queue is now significantly harder, as you would have to search through the whole list.
* (c) Allow the quantum time each process gets to be changed on a per process basis.
#### 5.22
(a) The time quantum is 1 millisecond: Irrespective of which process is scheduled, the scheduler incurs a 0.1 millisecond context-switching cost for every context-switch. This results in a CPU utilization of 1/1.1 * 100 = 91%.
(b) The time quantum is 10 milliseconds: The I/O-bound tasks incur a context switch after using up only 1 millisecond of the time quantum. The time required to cycle through all the processes is therefore 10 * 1.1 + 10.1 (as each I/O-bound task executes for 1 millisecond and then incur the context
switch task, whereas the CPU-bound task executes for 10 milliseconds before incurring a context switch). The CPU utilization is therefore 20/21.1 * 100 = 94%.
#### 5.23
The program could maximize the CPU time allocated to it by not fully utilizing its time quantums. It could use a large fraction of its assigned quantum, but relinquish the CPU before the end of the quantum, thereby increasing the priority associated with the process.
#### 5.24
* β > α > 0: FCFS
* α < β < 0: LIFO
#### 5.25
* a. FCFS — discriminates against short jobs since any short jobs arriving after long jobs will have a longer waiting time.
* b. RR — treats all jobs equally (giving them equal bursts of CPU time) so short jobs will be able to leave the system faster since they will finish first.
* c.Multilevel feedback queues work similar to the RR algorithm.
#### 5.26
A shared ready queue in an symmetric multiprocessing(SMP) environment has to lack frequently to make sure one job is assign to only one processor at a time. So queue accessing becomes bottle neck of the dispatching step.
#### 5.27
Similar to multilevel queue scheduling, the high-priority queue can be given 80 percent of the CPU time for RR scheduling among its processes, while the low-priority queue receives 20 percent of the CPU to give to its processes on an FCFS basis.
#### 5.28
* a. processor affinity has the benefit of keeping a thread running on the same processor that the thread can take advantage of its data being in that processor’s cache memory
* b. load balancing by moving child process to another processor can help reducing process waiting time but requires longer memory access times.
#### 5.29
An architecture featuring non-uniform memory access(NUMA) has two physical processor chips each with their own CPU and local memory. If the operating
system’s CPU scheduler and memory-placement algorithms are NUMA-aware and work together, then a thread that has been scheduled onto a particular CPU
can be allocated memory closest to where the CPU resides, thus providing the thread the fastest possible memory access.
#### 5.30
* a. A thread in the REALTIME PRIORITY CLASS with a relative priority of NORMAL: 24
* b. A thread in the ABOVE NORMAL PRIORITY CLASS with a relative priority of HIGHEST: 12
* c. A thread in the BELOW NORMAL PRIORITY CLASS with a relative priority of ABOVE NORMAL: 7
#### 5.31
HIGH priority class and HIGHEST priority within that class. (numeric priority of 15)
#### 5.32
* a. What is the time quantum (in milliseconds) for a thread with priority 15? 160. With priority 40? 40.
* b. Assume that a thread with priority 50 has used its entire time quantum without blocking. What new priority will the scheduler assign this thread? 50 (keep the same priority)
* c. Assume that a thread with priority 20 blocks for I/O before its time quantum has expired. What new priority will the scheduler assign this thread? 52 (new priority of return from sleep)
#### 5.33
vruntime is less for (1) higher priority and (2) for I/O-bound than CPU-bound.
* Both A and B are CPU-bound: prority A > B. `vruntime` A < B. (due to nice value)
* A is I/O-bound, and B is CPU-bound: prority A > B. `vruntime` A < B. (due to nice value and also I/O bound)
* A is CPU-bound, and B is I/O-bound: unclear. The system may reduce vruntime of B more than original nice value difference(which is 10).
#### 5.34
Consider two processes P1 and P2 where period p1 = 50, cpu burst t1 = 25 and p2 = 80, t2 = 35. If P1 were assigned a higher priority than P2, then the following scheduling events happen under rate-monotonic scheduling. P1 is scheduled at t = 0, P2 is scheduled at t = 25, P1 is scheduled at t = 50, and P2 is preempted and again scheduled at t = 75. P2 is not scheduled early enough to meet its deadline(figure 5.23). The earliest deadline schedule performs the following scheduling events: P1 is scheduled at t = 0, P2 is scheduled at t = 25, P1 is scheduled at t = 60, and so on(figure 5.24). This schedule actually meets the deadlines and therefore earliest-deadline-first scheduling is more effective than the rate-monotonic scheduler.
Rate-monotonic has a limitation: CPU utilization is bounded, and it is not always possible to maximize CPU resources fully. Scheduling cannot guarantee that processes can be scheduled so that they meet their deadlines. In contrast, Earliest-deadline-firs (EDF) scheduling does not require that processes be periodic, nor must a process require a constant amount of CPU time per burst. The only requirement is that a process announce its deadline to the scheduler when it becomes runnable, so scheduling assigns priorities dynamically according to deadline. The appeal of EDF scheduling is that it is theoretically optimal—theoretically, it can schedule processes so that each process can meet its deadline requirements and CPU utilization will be 100 percent. In practice, however, it is impossible to achieve this level of CPU utilization due to the cost of context switching between processes and interrupt handling.
#### 5.35 
rate-monotonic scheduling | p1 t = 25 | p2 t = 50 | p1 t = 75 | p2 t = 80 | p2 t = 100 | p1 t = 125 | p2 t = 135 | idle t = 150
--- | --- | --- | --- |--- |--- | --- | --- | ---

P2 is not scheduled early enough to meet its deadline.

earliest-deadline-first(EDF) scheduling | p1 t = 25 | p2 t = 55 | p1 t = 80 | p2 t = 100 | p1 t = 125 | p2 t = 135 | idle t = 150
--- | --- | --- | --- |--- |--- |--- |---
#### 5.36
Latency must be bound to ensure that real-time tasks receive immediate attention. Furthermore, sometimes interrupts are disabled when kernel data structures are being modified, so the interrupt does not get serviced immediately. For hard real-time systems, the time-period for which interrupts are disabled must be bounded in order to guarantee the desired quality of service.
#### 5.37
mobile operating systems use heterogeneous multiprocessing to better manage power consumption by assigning tasks to certain cores based upon the specific demands of the task. By combining a number of slower cores with faster ones, a CPU scheduler can assign tasks that do not require high performance, but may need to run for longer periods, (such as background tasks) to little cores, thereby helping to preserve a battery charge. Similarly, interactive applications which require more processing power, but may run for shorter durations, can be assigned to big cores. Additionally, if the mobile device is in a power-saving mode, energy-intensive big cores can be disabled and the system can rely solely on energy-efficient little cores.
## Chapter 6
### Practice Exercises
#### 6.1-6.6
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/6.pdf
#### 6.7
* a. the data `top` has race condition if it is changed by`push()` and `pop()` simutaneously.
* b. add `acquare()` before changing the value of `top` and `release()` after changing.
#### 6.8
If there are two process called `bid()` simutaneously, the data `highestBid` has race condition. Add `acquire()` before the if statement and `release()` before exiting the function to get mutual exclusiveness.
#### 6.9
array `v[k]` has race condition because all thread can access its value.
#### 6.10
yes. CAS checks no other thread changes the target data and has a lower overhead than lock. https://tigercosmos.xyz/post/2020/10/system/cas-lock-free/


