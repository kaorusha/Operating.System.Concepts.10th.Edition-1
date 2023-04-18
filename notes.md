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
#### 4.27
https://stackoverflow.com/questions/719677/printing-fibonacci-with-fork
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
yes. [CAS](https://tigercosmos.xyz/post/2020/10/system/cas-lock-free/) checks no other thread changes the target data and has a lower overhead than lock.
#### 6.11
"compare and compare-and-swap" idiom work appropriately. Suppose thread 1 is in the function, lock=1;Thread 2 also enters the function when the environment changes. At this time, lock=0. When thread 2 enters compare_and_swap(), set the lock to 1, and then return 0, and then thread 2 exits the loop. When the control is switched back to thread 1, when it enters compare_and swap(), it will return 1 and continue to spin.
#### 6.12
https://brainly.com/question/15244517
#### 6.13-6.15, 6.17
https://personal.cis.strath.ac.uk/sotirios.terzis/classes/CS.304/Remaining%20Contemplation%20Questions.pdf
#### 6.16, 6,19
see [5.15](http://dtucker.cs.edinboro.edu/CSCI380/Spring2017/Chapter5Answers.html) and 5.17
#### 6.18
Semaphore is nothing but is a special integer variable that can be accessed by only two system calls which are atomic in nature, known as p() and v() or wait() and signal(). It is a signaling mechanism that if a semaphore value is negative, its magnitude is the number of processes waiting on that semaphore. The busy waiting is not completely but moved from the entry section to the critical sections of application programs. Furthermore, we have limited busy waiting to the critical sections of the wait() and signal() operations, and these sections are short (if properly coded, they should be no more than about ten instructions).
#### 6.20
Given that waiting on a lock requires two context switches— a context switch to move the thread to the waiting state and a second context switch to restore the waiting thread once the lock becomes available — the general rule is to use a spinlock if the lock will be held for a duration of less than two context switches(2 * T, T = context switch time).
#### 6.21
https://enya.day/computers_and_technology/question-5212688.html
#### 6.22
http://mjgeiger.github.io/OS/prev/sp17/homework/OSsp17_hw2_soln.pdf
#### 6.23
The counting semaphore is initialized to the number of resources available (here it is maximum number of allowed connections). When the count for the semaphore goes to 0, all resources are being used. After that, processes that wish to use a resource will block until the count becomes greater than 0.
#### 6.24
n this case, the process will permanently block on the second call to wait(), as the semaphore is now unavailable. So system can't satisfy to ensure
that processes make progress during their execution life cycle.
#### 6.25, 6.26, 6.30
https://www.studocu.com/en-us/document/jacksonville-state-university/fundamentals-of-computer-operating-systems/cs350-chapter-6/41843522
#### 6.25
https://www.geeksforgeeks.org/monitor-vs-semaphore/
#### 6.26
https://www.quora.com/How-does-the-signal-operation-associated-with-monitors-differ-from-the-corresponding-operation-defined-for-semaphores
#### 6.27
http://web.cs.wpi.edu/~cs502/f98/Waltham/hw2soln.html
#### 6.28
```c
type resource = monitor
var P: array[0..2] of boolean;
X: condition;
procedure acquire (id: integer, printer-id: integer);
begin
if P[0] and P[1] and P[2] then X.wait(id)
if not P[0] then printer-id := 0;
else if not P[1] then printer-id := 1;
else printer-id := 2;
P[printer-id]:=true;
end
procedure release (printer-id: integer)
begin
P[printer-id]:=false;
X.signal;
end

begin
P[0] := P[1] := P[2] := false;
end
```
#### 6.29
```c
int sumid=0; /* Shared var that contains the sum of the process ids currently accessing the file */
int waiting=0; /* Number of process waiting on the semaphore OkToAccess */
semaphore mutex=1; /* Our good old Semaphore variable ;) */
semaphore OKToAccess=0; /* The synchronization semaphore */

get_access(int id)
{
  sem_wait(mutex);
  while(sumid+id > n) {
    waiting++;
    sem_signal(mutex);
    sem_wait(OKToAccess);
    sem_wait(mutex);
  }
  sumid += id;
  sem_signal(mutex);
}

release_access(int id)
{
  int i;
  sem_wait(mutex);
  sumid -= id;
  for (i=0; i < waiting;++i) {
    sem_signal(OKToAccess);
  }
  waiting = 0;
  sem_signal(mutex);
}

main()
{
  get_access(id);
  do_stuff();
  release_access(id);
}
```
Some points to note about the solution:

Release_access wakes up all waiting processes. It is NOT ok to wake up the first waiting process in this problem --- that process may have too large a value of id. Also, more than one process may be eligible to go in (if those processes have small ids) when one process releases access.

Woken up processes try to see if they can get in. If not, they go back to sleep.

Waiting is set to 0 in release_access after the for loop. That avoids unnecessary signals from subsequent release_accesses. Those signals would not make the solution wrong, just less efficient as processes will be woken up unnecessarily.
#### 6.31
see [3](https://www3.cs.stonybrook.edu/~kifer/Courses/cse306/homeworks/hw2.pdf)
#### 6.32
see [5.20](https://silo.tips/download/chapter-5-exercises-51-answer-52-answer-53-lottery-scheduling)
## Chapter 7
### Practice Exercises
#### 7.1-7.6
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/7.pdf
#### 7.7
Some kernel data structures include a process id (pid) management system, kernel process table, and scheduling queues.With a pid management system, it is possible two processes may be created at the same time and there is a race condition assigning each process a unique pid. The same type of race condition can occur in the kernel process table: two processes are created at the same time and there is a race assigning them a location in the kernel process table. With scheduling queues, it is possible one process has been waiting for IO which is now available. Another process is being context-switched out. These two processes are being moved to the Runnable queue at the same time. Hence there is a race condition in the Runnable queue.
#### 7.8
You cannot hold a spin lock while you acquire a semaphore, because you might have to sleep while waiting for the semaphore, and you cannot sleep while holding a spin lock (from "Linux Kernel Development" by Robert Love).
https://stackoverflow.com/questions/4752031/why-cant-you-sleep-while-holding-spinlock
#### 7.9
see [6.32](http://hscc.cs.nthu.edu.tw/~sheujp/homework/os09/HW6_ref.pdf)
#### 7.10
* a. If the portions are large, then adding and removing data to the shared pool requires a considerable amount of time. Since the producer and consumer cannot execute in the monitor concurrently, parallelism is lost.
* b. This problem could be alleviated by storing pointers to buffer regions within the monitor instead of storing the buffer regions themselves. Consequently, one could modify the code to simply copy the pointer to the buffer region into and out of the monitor state. This operation should be relatively inexpensive and therefore the period of time that the monitor is being held will be much shorter, thereby increasing the throughput of the monitor.
#### 7.11
* a. Throughput in the readers-writers problem is increased by favouring multiple readers as opposed to allowing a single writer to exclusively access the shared values. On the other hand, favouring readers could result in starvation for writers.
* b. The starvation in the readers-writers problem could be avoided by keeping timestamps associated with waiting processes. When a writer is finished with its task, it would wakeup the process that has been waiting for the longest duration. When a reader arrives and notices that another reader is accessing the database, then it would enter the critical section only if there are no waiting writers. These restrictions would guarantee fairness.
#### 7.12
we do not place the call to lock() within the try clause, as lock() does not throw any checked exceptions. Consider what happens if we place lock() within the try clause and an unchecked exception occurs when lock() is invoked (such as OutofMemoryError): The finally clause triggers the call to unlock(), which then throws the unchecked IllegalMonitorStateException, as the lock was never acquired. Unlock statement is always called in the finally block to ensure that the lock is released even if an exception is thrown in the method body(try block).
#### 7.13
**Software transactional memory (STM)** works by inserting instrumentation code inside transaction blocks. The code is inserted by a compiler and manages each transaction by examining where statements may run concurrently and where specific low-level locking is required. **Hardware transactional memory (HTM)** uses hardware cache hierarchies and cache coherency protocols to manage and resolve conflicts involving shared data residing in separate processors’ caches. HTM requires no special code instrumentation and thus has less overhead than STM.
### Programming Problems
#### 7.14
https://github.com/pronaypeddiraju/OS-Project/blob/master/P159_part1.cpp
#### 7.16
A mutex is created with the pthread mutex init() function. The first parameter is a pointer to the mutex. By passing NULL as a second parameter, we initialize the mutex to its default attributes.The mutex is acquired and released with the pthread mutex lock() and pthread mutex unlock() functions. [stack-ptr.c](https://www.chegg.com/homework-help/questions-and-answers/program-stack-ptrc-implements-stack-using-linked-list-however-contains-race-condition-appr-q95139381)
#### 7.17
https://github.com/github-bishwajeet/OS-Assignment/blob/master/OS_Assignment.cpp
#### 7.19
https://github.com/nikhilkrdwivedi/OS-Assignment/blob/master/Barrier.c
## Chapter 8
### Practice Exercises
#### 8.1-8.11
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/8.pdf
#### 8.12
* a. The four necessary conditions for a deadlock are (1) mutual exclusion; (2) hold-and-wait; (3) no preemption; and (4) circular wait. The mutual exclusion condition holds since only one car can occupy a space in the roadway. Hold-and-wait occurs where a car holds onto its place in the roadway while it waits to advance in the roadway. A car cannot be removed (i.e. preempted) from its position in the roadway. Lastly, there is indeed a circular wait as each car is waiting for a subsequent car to advance. The circular wait conditi on is also easily observed from the graphic.
* b. A simple rule that would avoid this traffic deadlock is that a car may not advance into an intersection if it is clear it will not be able immediately to clear the intersection.
#### 8.15
YES. (1)Mutual exclusion is maintained, as they cannot be shared if there is a writer. (2)Hold-and-wait is possible, as a thread can hold one reader—writer lock while waiting to acquire another. (3) You cannot take a lock away, so no preemeption is upheld. (4) A circular wait among all threads is possible.
#### 8.16
If thread_one is scheduled before thread_two and thread_one is able to acquire both mutex locks before thread_two is scheduled, deadlock will not occur. Deadlock can only occur if either thread_one or thread_two is able to acquire only one lock before the other thread acquires the second lock.
#### 8.17
* a. **containment** add a lock for acquiring all other locks.
```c
void transaction(Account from, Account to, double amount)
{
  Semaphore lock1, lock2, lock3;
  wait(lock3);
  lock1 = getLock(from);
  lock2 = getLock(to);
  wait(lock1);
    wait(lock2);
      withdraw(from, amount);
      deposit(to, amount);
    signal(lock3);
    signal(lock2);
  signal(lock1);
}
```
* b. use `pthread_mutex_trylock()` and if livelock happens, sleep for a random period before retrying.
#### 8.18
(a) T2-->T3-->T1 or T2-->T1-->T3 (b) deadlock T1-->R3-->T3-->R1-->T1 (c) T2-->T3-->T1 or T3-->T2-->T1 (d) deadlock R1-->T1-->R2-->T3-->R1 and R1-->T2-->R2-->T4-->R1 (e) T2-->T1(or T3)-->T3(or T1)-->T4 (f) T4(or T2)-->T2(or T4)-->T1-->T3
#### 8.19
* a. Runtime overhead - A deadlock-avoidance scheme tends to increase the runtime overheads than the circular-wait scheme due to the cost of keep track of the current resource allocation.
* b. System throughput - However, a deadlock-avoidance scheme allows for more concurrent use of resources than schemes that statically prevent the formation of deadlock. In that sense, a deadlock-avoidance scheme could increase system throughput.
#### 8.20
a, d, e, f
#### 8.21
Need = Max - Allocation = \[\[4,2,2,1], \[2,1,0,2], \[4,3,0,2], \[3,1,1,1], \[4,2,3,1]]
#### 8.22
There is no circular-waiting happens. Suppose the system is deadlocked. This implies that each process is holding one resource and is waiting for 
one more. Since there are three processes and four resources, one process must be able to obtain two resources. This process requires no more resources and, therefore it will return its resources when done.
#### 8.23
* a. The maximum need of each thread is between one resource and m resources.--> $1 <= Max_i <= m$
* b. The sum of all maximum needs is less than $m + n$. -->
$$\sum_{i=1}^n Max_i = \sum_{i=1}^n Allocation_i + Need_i < m + n$$
If there exists a deadlock state then:
$$\sum_{i=1}^n Allocation_i = m$$
So condition b comes to
$$\sum_{i=1}^n Need_i < n$$ 
This implies that there exists a process $P_i$ such that $Need_i = 0$. Since from condition a $Max_i >= 1$ it follows that $P_i$ has at least one resource that it can release. Hence the system cannot be in a deadlock state.
#### 8.24
The following rule prevents deadlock: when a philosopher makes a request for the first chopstick, do not grant the request if there is no other philosopher with two chopsticks and if there is only one chopstick remaining.
#### 8.25
When a philosopher makes a request for a chopstick, allocate the request if: 1) the philosopher has two chopsticks and there is at least one chopstick remaining, 2) the philosopher has one chopstick and there are at least two chopsticks remaining, 3) there is at least one chopstick remaining, and there is at least one philosopher with three chopsticks, 4) the philosopher has no chopsticks, there are two chopsticks remaining, and there is at least one other philosopher with two chopsticks assigned.
#### 8.26
see [7.11](https://docplayer.net/64549995-Chapter-7-exercises-7-1-answer-7-2-answer-7-3-answer-7-4-answer.html). If we use single-resource-type scheme and for each type which seems safe for need may contradict with other resource type. Banker's scheme simuteneously consider all resource type. 
#### 8.27
(a) T4-->T0-->remains arbitrarily (b) T2(or T4)-->T4(or T2)-->T1(or T3)-->remains arbitrarily (c) unsafe, non of tread need is satisfied (d) T3-->remains arbitrarily
#### 8.28
(a) T2 or T3 first, than T0 and T1 can be finished, than remains can be finished. (b) No. If granted, $Need_4 = \[1,2,3,0]$ and $Available = \[0,0,0,0]$, which is unsafe state. (c) Yes. If granted, $Need_2 = \[0,0,1,0]$ and $Available = \[2,1,1,4]$, T2 can be finished, and keeps in safe state. (d) Yes. If granted, $Need_3 = \[0,0,1,0]$ and $Available = \[0,0,1,2]$, T3 can be finished, and keeps in safe state.
#### 8.29
The optimistic assumption is that there will not be any form of circular wait in terms of resources allocated and processes making requests for them. This assumption could be violated if a circular wait does indeed occur in practice.
> section 8.7.2 we take an optimistic attitude and assume that Ti will require no more resources to complete its task; it will thus soon return all currently allocated resources to the system. If our assumption is incorrect, a deadlock may occur later. That deadlock will be detected the next time the deadlock-detection algorithm is invoked.
#### 8.30-8.31
see [7.15-7.16](https://docplayer.net/64549995-Chapter-7-exercises-7-1-answer-7-2-answer-7-3-answer-7-4-answer.html)
## Chapter 9
### Practice Exercises
#### 9.1-9.10
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/9.pdf
#### 9.11
https://www.geeksforgeeks.org/difference-between-internal-and-external-fragmentation/
#### 9.12
The linker has to replace unresolved symbolic addresses with the actual addresses associated with the variables in the final program binary. In order to perform this, the modules should keep track of instructions that refer to unresolved symbols. During linking, each module is assigned a sequence of addresses in the overall program binary and when this has been performed, unresolved references to symbols exported by this binary could be patched in other modules since every other module would contain the list of instructions that need to be patched.
#### 9.13
* first-fit

process| 100 MB | 170 MB | 40 MB | 205 MB | 300 MB | 185 MB
-------|--------|--------|-------|------|--------|-------
200 MB | 100 MB | 170 MB | 40 MB | 5 MB | 300 MB | 185 MB
 15 MB | 85 MB  | 170 MB | 40 MB | 5 MB | 300 MB | 185 MB
185 MB | 85 MB  | 170 MB | 40 MB | 5 MB | 115 MB | 185 MB
 75 MB | 10 MB  | 170 MB | 40 MB | 5 MB | 115 MB | 185 MB
175 MB | 10 MB  | 170 MB | 40 MB | 5 MB | 115 MB |  10 MB
 80 MB | 10 MB  |  90 MB | 40 MB | 5 MB | 115 MB |  10 MB
* best-fit

process| 100 MB | 170 MB | 40 MB | 205 MB | 300 MB | 185 MB
-------|--------|--------|-------|------|--------|-------
200 MB | 100 MB | 170 MB | 40 MB | 5 MB | 300 MB | 185 MB
 15 MB | 85 MB  | 170 MB | 25 MB | 5 MB | 300 MB | 185 MB
185 MB | 85 MB  | 170 MB | 25 MB | 5 MB | 300 MB |   0 MB
 75 MB | 10 MB  | 170 MB | 25 MB | 5 MB | 300 MB |   0 MB
175 MB | 10 MB  | 170 MB | 25 MB | 5 MB | 125 MB |   0 MB
 80 MB | 10 MB  | 170 MB | 25 MB | 5 MB |  45 MB |   0 MB
* worst-fit

process| 100 MB | 170 MB | 40 MB | 205 MB | 300 MB | 185 MB
-------|--------|--------|-------|--------|--------|-------
200 MB | 100 MB | 170 MB | 40 MB | 205 MB | 100 MB | 185 MB
 15 MB | 100 MB | 170 MB | 40 MB | 190 MB | 100 MB | 185 MB
185 MB | 100 MB | 170 MB | 40 MB |   5 MB | 100 MB | 185 MB
 75 MB | 100 MB | 170 MB | 40 MB |   5 MB | 100 MB | 110 MB
175 MB | 100 MB | 170 MB | 40 MB |   5 MB | 100 MB | 110 MB
 80 MB | 100 MB |  90 MB | 40 MB |   5 MB | 100 MB | 110 MB

process with 175 MB must wait in worst-fit, and first-fit left more space than best-fit. 
#### 9.14
* a. contiguous-memory allocation: might require relocation of the entire program since there is not enough space for the program to grow its allocated memory space.
* b. paging: incremental allocation of new pages is possible in this scheme without requiring relocation of the program’s address space.
#### 9.15
Issues | contiguous memory allocation scheme | paging
-------|-------------------------------------|--------
a. External fragmentation | holes develop as old processes die and new processes are initiated.| |
b. Internal fragmentation | |Processes are allocated in page granularity and results in a corresponding wastage of space.
c. Ability to share code across processes | not allowed, since a process’s virtual memory segment is not broken into noncontiguous fine grained segments. | allowed
#### 9.16
An address on a paging system is a logical page number and an offset. The physical page is found by searching a table based on the logical page number to produce a physical page number. Because the operating system controls the contents of this table, it can limit a process to accessing only those physical pages allocated to the process. There is no way for a process to refer to a page it does not own because the page will not be in the page table. To allow such access, an operating system simply needs to allow entries for non-process memory to be added to the process’s page table. This is useful when two or more processes need to exchange data they just read and write to the same physical addresses (which may be at varying logical addresses). This makes for
very efficient interprocess communication.
#### 9.17
Mobile devices generally use flash memory rather than more spacious hard disks for nonvolatile storage. The resulting space constraint is one reason why mobile operating-system designers avoid swapping. Other reasons include the limited number of writes that flash memory can tolerate before it becomes unreliable and the poor throughput between main memory and flash memory in these devices.
#### 9.18
The boot disk has limited storage capacity.
#### 9.19
When the TLB attempts to resolve virtual page numbers, it ensures that the ASID for the currently running process matches the ASID associated with the virtual page. If the ASIDs do not match, the attempt is treated as a TLB miss. If the TLB does not support separate ASIDs, then every time a new page table is selected (for instance, with each context switch), the TLB must be flushe (or erased) to ensure that the next executing process does not use the wrong translation information. Otherwise, the TLB could include old entries that contain valid virtual addresses but have incorrect or invalid physical addresses left over from the previous process.
#### 9.20
* a. Contiguous-memory allocation requires the operating system to allocate the entire extent of the virtual address space to the program when it starts executing. This could be much larger than the actual memory requirements of the process.
* b. Paging does not require the operating system to allocate the maximum extent of the virtual address space to a process at startup time, but it still requires the operating system to allocate a large page table spanning all of the program’s virtual address space. When a program needs to extend the stack or the heap, it needs to allocate a new page but the corresponding page table entry is preallocated.
#### 9.21
address references | page numbers(1-KB page size) | offset
-------------------|--------------|-------
21205              |     20       |  725
164250             |    160       |  410
121357             |    118       |  525
16479315           |  16093       |   83
27253187           |  26614       |  451
#### 9.22
* a. A conventional, single-level page table has $2^{12}$ entries. (virtual address / page size)
* b. An inverted page table has $2^8$ entries. (physical address / page size)
maximum amount of physical memory is $2^{20}$(or $2^{10}$ KB).
#### 9.23
Consider a logical address space of 2,048 pages with a 4-KB page size, mapped onto a physical memory of 512 frames.
* a. 11 + 13 bits are required in the logical address
* b. 9 + 11 bits are required in the physical address
#### 9.24
Consider a computer system with a 32-bit logical address and 8-KB page size. The system supports up to 1 GB of physical memory.
* a. A conventional, single-level page table has $2^{14}$ entries.
* b. An inverted page table has $2^{12}$ entries.
#### 9.25
Consider a paging system with the page table stored in memory.
* a. If a memory reference takes 50 nanoseconds, how long does a paged memory reference take?<br/>
we must first access memory for the page table and frame number (50 nanoseconds) and then access the desired byte in memory (50 nanoseconds), for a total of 100 nanoseconds.
* b. If we add TLBs, and if 75 percent of all page-table references are found in the TLBs, what is the effective memory reference time? (Assume that finding a page-table entry in the TLBs takes 2 nanoseconds, if the entry is present.)<br/>
effective memory-access time = 0.75 x (2 + 50) + 0.25 x 100 = 64 nanoseconds$
#### 9.26
In certain situations the page tables could become large enough that by paging the page tables, one could simplify the memory allocation problem (by ensuring that everything is allocated as fixed-size pages as opposed to variable-sized chunks) and also enable the swapping of portions of page table that are not currently used.
#### 9.27
* a. Describe all the steps taken by the IA-32 in translating a logical address into a physical address.<br/>
The IA-32 address translation is shown in more detail in Figure 9.23. The 10 high-order bits reference an entry in the outermost page table, which IA-32 terms the page directory. (The CR3 register points to the page directory for the current process.) The page directory entry points to an inner page table that is indexed by the contents of the innermost 10 bits in the linear address. Finally, the low-order bits 0–11 refer to the offset in the 4-KB
page pointed to in the page table.<br/>
One entry in the page directory is the Page Size flag, which—if set—indicates that the size of the page frame is 4 MB and not the standard 4 KB. If this flag is set, the page directory points directly to the 4-MB page frame, bypassing the inner page table; and the 22 low-order bits in the linear address
refer to the offset in the 4-MB page frame.
* b. What are the advantages to the operating system of hardware that provides such complicated memory translation?<br/>
The advantage is that the OS can provide protection both through segmentation and paging.
* c. Are there any disadvantages to this address-translation system? If so, what are they? If not, why is this scheme not used by every manufacturer?<br/>
The complexity makes it slow and inflexible - OS's can't choose a page table format or handle TLB misses. The OS had to be more complex to manage both segments and page tables.
## Chapter 10
### Practice Exercise
#### 10.1-10.14
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/10.pdf
#### 10.4 [explain](https://gateoverflow.in/71580/ugc-net-cse-august-2016-part-3-question-51)
#### 10.15 [9.14][1]
#### 10.16 [9.15][2]
#### 10.17 [9.16][1]
#### 10.18
The virtual addresses is 12-bit so 0 to 7 bit is 256-byte page size represents the offset and 8 to 11 bit represents virtual page number.
* 0x2A1 --> 0xAA1
* 0x4E6 --> 0x9E6
* 0x94A --> 0x14A
* 0x316 --> 0xF16
#### 10.19 [9.19][1]
#### 10.20 [10.3](https://courses.cs.washington.edu/courses/cse451/04au/homework/hw4sol..htm)
#### 10.21 [9.21][2]
#### 10.22
* a. Convert the following virtual addresses (in hexadecimal) to the equivalent physical addresses.
  * 0x621C --> 0x821C
  * 0xF0A3 --> 0x20A3
  * 0xBC1A --> 0x4C1A
  * 0x5BAA --> 0xDBAA
  * 0x0BA1 --> 0x9BA1
* b. The logical address (in hexadecimal) that results in a page fault is the page numbers in the table with a dash for a page frame indicates that the page is not in memory, which is 1, 9, and E(14).
* c. From what set of page frames will the LRU page-replacement algorithm choose in resolving a page fault? Any page table entries that have a reference bit of zero.
#### 10.23 [9.7][3]
#### 10.24
page-reference strings | 2 | 6 | 9 | 2 | 4 | 2 | 1 | 7 | 3 | 0 | 5 | 2 | 1 | 2 | 9 | 5 | 7 | 3 | 8 | 5   
-----------------------|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---
| (1) FIFO             | 2 | 2 | 2 |   | 4 | 4 | 4 | 7 | 7 | 7 | 5 | 5 | 5 |   | 9 | 9 | 9 | 3 | 3 | 3 
|     page faults = 18 |   | 6 | 6 |   | 6 | 2 | 2 | 2 | 3 | 3 | 3 | 2 | 2 |   | 2 | 5 | 5 | 5 | 8 | 8 
|                      |   |   | 9 |   | 9 | 9 | 1 | 1 | 1 | 0 | 0 | 0 | 1 |   | 1 | 1 | 7 | 7 | 7 | 5 
| (2) LRU              | 2 | 2 | 2 |   | 2 |   | 2 | 2 | 3 | 3 | 3 | 2 | 2 |   | 2 | 2 | 7 | 7 | 7 | 5 
|     page faults = 17 |   | 6 | 6 |   | 4 |   | 4 | 7 | 7 | 7 | 5 | 5 | 5 |   | 9 | 9 | 9 | 3 | 3 | 3 
|                      |   |   | 9 |   | 9 |   | 1 | 1 | 1 | 0 | 0 | 0 | 1 |   | 1 | 5 | 5 | 5 | 8 | 8 
| (3) Optimal (OPT)    | 2 | 2 | 2 |   | 2 |   | 2 | 2 | 2 | 2 | 2 |   |   |   | 9 |   | 9 | 3 | 3 |   
|     page faults = 13 |   | 6 | 6 |   | 4 |   | 1 | 1 | 1 | 1 | 1 |   |   |   | 1 |   | 7 | 7 | 8 |   
|                      |   |   | 9 |   | 9 |   | 9 | 7 | 3 | 0 | 5 |   |   |   | 5 |   | 5 | 5 | 5 |   

page-reference strings | 0 | 6 | 3 | 0 | 2 | 6 | 3 | 5 | 2 | 4 | 1 | 3 | 0 | 6 | 1 | 4 | 2 | 3 | 5 | 7  
-----------------------|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---
| (1) FIFO             | 0 | 0 | 0 |   | 2 |   |   | 2 |   | 2 | 1 | 1 | 1 | 6 | 6 | 6 | 2 | 2 | 2 | 7 
|     page faults = 16 |   | 6 | 6 |   | 6 |   |   | 5 |   | 5 | 5 | 3 | 3 | 3 | 1 | 1 | 1 | 3 | 3 | 3 
|                      |   |   | 3 |   | 3 |   |   | 3 |   | 4 | 4 | 4 | 0 | 0 | 0 | 4 | 4 | 4 | 5 | 5 
| (2) LRU              | 0 | 0 | 0 |   | 0 | 0 | 3 | 3 | 3 | 4 | 4 | 4 | 0 | 0 | 0 | 4 | 4 | 4 | 5 | 5 
|     page faults = 19 |   | 6 | 6 |   | 2 | 2 | 2 | 5 | 5 | 5 | 1 | 1 | 1 | 6 | 6 | 6 | 2 | 2 | 2 | 7 
|                      |   |   | 3 |   | 3 | 6 | 6 | 6 | 2 | 2 | 2 | 3 | 3 | 3 | 1 | 1 | 1 | 3 | 3 | 3 
| (3) Optimal (OPT)    | 0 | 0 | 0 |   | 2 |   |   | 2 |   | 2 | 1 |   | 1 | 1 |   |   | 2 | 2 | 2 | 7 
|     page faults = 13 |   | 6 | 6 |   | 6 |   |   | 5 |   | 4 | 4 |   | 4 | 4 |   |   | 4 | 3 | 3 | 3 
|                      |   |   | 3 |   | 3 |   |   | 3 |   | 3 | 3 |   | 0 | 6 |   |   | 6 | 6 | 5 | 5 

page-reference strings | 3 | 1 | 4 | 2 | 5 | 4 | 1 | 3 | 5 | 2 | 0 | 1 | 1 | 0 | 2 | 3 | 4 | 5 | 0 | 1  
-----------------------|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---
| (1) FIFO             | 3 | 3 | 3 | 2 | 2 |   | 2 | 3 |   | 3 | 3 | 1 |   |   |   | 1 | 1 | 5 | 5 | 5 
|     page faults = 15 |   | 1 | 1 | 1 | 5 |   | 5 | 5 |   | 2 | 2 | 2 |   |   |   | 3 | 3 | 3 | 0 | 0 
|                      |   |   | 4 | 4 | 4 |   | 1 | 1 |   | 1 | 0 | 0 |   |   |   | 0 | 4 | 4 | 4 | 1 
| (2) LRU              | 3 | 3 | 3 | 2 | 2 |   | 1 | 1 | 1 | 2 | 2 | 2 |   |   |   | 2 | 2 | 5 | 5 | 5 
|     page faults = 16 |   | 1 | 1 | 1 | 5 |   | 5 | 3 | 3 | 3 | 0 | 0 |   |   |   | 3 | 3 | 3 | 0 | 0 
|                      |   |   | 4 | 4 | 4 |   | 4 | 4 | 5 | 5 | 5 | 1 |   |   |   | 1 | 4 | 4 | 4 | 1 
| (3) Optimal (OPT)    | 3 | 3 | 3 | 2 | 5 |   |   | 5 |   | 2 | 2 |   |   |   |   | 3 | 4 | 5 |   |   
|     page faults = 11 |   | 1 | 1 | 1 | 1 |   |   | 1 |   | 1 | 1 |   |   |   |   | 1 | 1 | 1 |   |   
|                      |   |   | 4 | 4 | 4 |   |   | 3 |   | 3 | 0 |   |   |   |   | 0 | 0 | 0 |   |   

page-reference strings | 4 | 2 | 1 | 7 | 9 | 8 | 3 | 5 | 2 | 6 | 8 | 1 | 0 | 7 | 2 | 4 | 1 | 3 | 5 | 8  
-----------------------|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---
| (1) FIFO             | 4 | 4 | 4 | 7 | 7 | 7 | 3 | 3 | 3 | 6 | 6 | 6 | 0 | 0 | 0 | 4 | 4 | 4 | 5 | 5 
|     page faults = 20 |   | 2 | 2 | 2 | 9 | 9 | 9 | 5 | 5 | 5 | 8 | 8 | 8 | 7 | 7 | 7 | 1 | 1 | 1 | 8 
|                      |   |   | 1 | 1 | 1 | 8 | 8 | 8 | 2 | 2 | 2 | 1 | 1 | 1 | 2 | 2 | 2 | 3 | 3 | 3 
| (2) LRU              | 4 | 4 | 4 | 7 | 7 | 7 | 3 | 3 | 3 | 6 | 6 | 6 | 0 | 0 | 0 | 4 | 4 | 4 | 5 | 5 
|     page faults = 20 |   | 2 | 2 | 2 | 9 | 9 | 9 | 5 | 5 | 5 | 8 | 8 | 8 | 7 | 7 | 7 | 1 | 1 | 1 | 8 
|                      |   |   | 1 | 1 | 1 | 8 | 8 | 8 | 2 | 2 | 2 | 1 | 1 | 1 | 2 | 2 | 2 | 3 | 3 | 3 
| (3) Optimal (OPT)    | 4 | 4 | 4 | 7 | 9 | 8 | 8 | 8 |   | 8 |   | 8 | 0 | 7 |   | 4 |   | 4 | 5 | 5  
|     page faults = 16 |   | 2 | 2 | 2 | 2 | 2 | 2 | 2 |   | 2 |   | 2 | 2 | 2 |   | 2 |   | 3 | 3 | 3 
|                      |   |   | 1 | 1 | 1 | 1 | 3 | 5 |   | 6 |   | 1 | 1 | 1 |   | 1 |   | 1 | 1 | 8 

page-reference strings | 0 | 1 | 2 | 3 | 4 | 4 | 3 | 2 | 1 | 0 | 0 | 1 | 2 | 3 | 4 | 4 | 3 | 2 | 1 | 0  
-----------------------|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---
| (1) FIFO             | 0 | 0 | 0 | 3 | 3 |   |   |   | 3 | 0 |   |   | 0 | 0 | 4 |   |   |   | 4 | 4 
|     page faults = 12 |   | 1 | 1 | 1 | 4 |   |   |   | 4 | 4 |   |   | 2 | 2 | 2 |   |   |   | 1 | 1 
|                      |   |   | 2 | 2 | 2 |   |   |   | 1 | 1 |   |   | 1 | 3 | 3 |   |   |   | 3 | 0 
| (2) LRU              | 0 | 0 | 0 | 3 | 3 |   |   |   | 3 | 0 |   |   |   | 3 | 3 |   |   |   | 3 | 0 
|     page faults = 11 |   | 1 | 1 | 1 | 4 |   |   |   | 1 | 1 |   |   |   | 1 | 4 |   |   |   | 1 | 1 
|                      |   |   | 2 | 2 | 2 |   |   |   | 2 | 2 |   |   |   | 2 | 2 |   |   |   | 2 | 2 
| (3) Optimal (OPT)    | 0 | 0 | 0 | 3 | 3 |   |   |   | 3 | 0 |   |   |   | 3 | 3 |   |   |   | 3 | 0 
|     page faults = 11 |   | 1 | 1 | 1 | 4 |   |   |   | 1 | 1 |   |   |   | 1 | 4 |   |   |   | 1 | 1 
|                      |   |   | 2 | 2 | 2 |   |   |   | 2 | 2 |   |   |   | 2 | 2 |   |   |   | 2 | 2 
#### 10.25 [9.10][3]
#### 10.26 [9.25][1]
#### 10.27 [9.11][3]
#### 10.28 [9.13][3]
#### 10.29 [9.28][1]
#### 10.30
A major page fault occurs when a page is referenced and the page is not in memory. Servicing a major page fault requires reading the desired page from the backing store into a free frame and updating the page table. Minor page faults occur when a process does not have a logical mapping to a page, yet that page is in memory. To deal with minor page fault, it is only necessary to update the page table (for shared library), or remove needed frame from the free-frame list and move to resident page in order to reassigned to the process.
#### 10.31
Mobile systems generally do not support either standard swapping or swapping pages. Thus, memory compression is an integral part of the memory-management strategy for most mobile operating systems.
#### 10.32 [9.15][3]
#### 10.33
Page 18~26, page 31, 33
#### 10.34 [9.16][3]
#### 10.35 [9.17][3]
page-reference strings | 1 | 2 | 3 | 4 | 5 | 3 | 4 | 1 | 6 | 7 | 8 | 7 | 8 | 9 | 7 | 8 | 9 | 5 | 4 | 5 | 4 | 2 
-----------------------|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---
| (b) LFU              | 1 | 1 | 1 | 1 | 5 |   |   | 5 | 6 | 6 | 8 |   |   | 8 |   |   |   | 8 | 8 | 8 |   | 8 
|     page faults = 14 |   | 2 | 2 | 2 | 2 |   |   | 1 | 1 | 7 | 7 |   |   | 7 |   |   |   | 7 | 7 | 7 |   | 7 
|                      |   |   | 3 | 3 | 3 |   |   | 3 | 3 | 3 | 3 |   |   | 9 |   |   |   | 9 | 9 | 5 |   | 2 
|                      |   |   |   | 4 | 4 |   |   | 4 | 4 | 4 | 4 |   |   | 4 |   |   |   | 5 | 4 | 4 |   | 4 
| (c) optimal          | 1 | 1 | 1 | 1 | 1 |   |   |   | 6 | 6 | 8 |   |   | 8 |   |   |   |   | 8 |   |   | 2 
|     page faults = 11 |   | 2 | 2 | 2 | 5 |   |   |   | 5 | 5 | 5 |   |   | 5 |   |   |   |   | 5 |   |   | 5 
|                      |   |   | 3 | 3 | 3 |   |   |   | 3 | 7 | 7 |   |   | 7 |   |   |   |   | 4 |   |   | 4 
|                      |   |   |   | 4 | 4 |   |   |   | 4 | 4 | 4 |   |   | 9 |   |   |   |   | 9 |   |   | 9
#### 10.36 [9.14][4]
#### 10.37 [9.19][3]
#### 10.38 [9.20][3]
#### 10.39 [9.21][3]
#### 10.40
      request           1024                   release    1024
                         /\                                /\
                      512  512                          512  512
                      /\                                /\
                   256  256(135)                     256  256(135)
                   /\
                128  128
                /\
              64  64
              /\
            32  32
           /\    /\
         16 16  16(14)16(12)
         /\     
        8  8(5)
       /\
      4  4(3)
#### 10.41 [9.23][3]
#### 10.42 [9.24][3]
#### 10.43 [9.25][3]
[1]: https://ininet.org/9-14-assume-a-program-has-just-referenced-an-address-in-virtua.html
[2]: http://www.jade-cheng.com/uh/coursework/ics-412/homework-6.pdf
[3]: https://docplayer.net/25406625-Chapter-9-exercises-9-1-answer-9-2-ready-running-blocked-answer-9-3.html
[4]: https://sites.cs.ucsb.edu/~tyang/class/170.w06/solutions/solution3.html
## Chapter 11
### Practice Exercises
#### 11.1-11.10
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/11.pdf
#### 11.11 [12.18][5]
#### 11.12 
Due to the lack of moving parts in NVM devices, performance is unaffected by problems like seek time and rotational delay. Therefore, a straightforward FCFS policy will do.
#### 11.13
cylinder request         | 0 | 356 | 544 | 1212 | 1523 | 1618 | 2069 | 2150 | 2296 | 2800 | 3681 | 4695 | 4999 
-------------------------|---|-----|-----|------|------|------|------|------|------|------|------|------|-------
| (a) FCFS               |   |     |     |      |      |      |      |a,b,c |      |      |      |      |  
|     distance = 13011   |   |     |     |      |      |      |  a   |      | b,c  |      |      |      |
|                        |   |     |     |  a   |      |      |      |      |      | b,c  |      |      |
|                        |   |     |     |      |      |      |      |      |  a   |      | b,c  |      |
| (b) SCAN               |   |     |     |      |      |      |      |      |      |   a  |      |  b,c |
|     distance = 7492    |   |     |  a  |      |      |      |      |      |      |      |      |      |  b,c
|                        | c |     |     |      |      |  a   |  b   |      |      |      |      |      |
|                        |   | a,c |     |      |      |  b   |      |      |      |      |      |      |
| (c) C-SCAN             |   |     |  c  |      |  a,b |      |      |      |      |      |      |      |
|     distance = 9917    |   |     |     | b,c  |      |      |      |      |      |      |      |  a   |
|                        |   |     |  b  |      |  c   |      |      |      |      |      |   a  |      |
|                        |   |  b  |     |      |      |   c  |      |      |      |      |      |      |
| [other algorithm](https://www.geeksforgeeks.org/disk-scheduling-algorithms/)                       |   |     |     |      |      |      |   c  |      |      |      |      |      |
#### 11.14
* a. rewrite $d = \frac{1}{2}at^2$ and get $t = \sqrt{\frac{2d}{a}}$
* b. solve the simultaneous equations $t = x + y\sqrt{L}$ that result from (t = 1, L = 1) and (t = 18, L = 4999) to obtain $t = 0.7561 + 0.2439\sqrt{L}$
* c. total seek time is 29ms(FCFS), 22ms(SCAN), 25ms(C-SCAN). SCAN is the fatest.
* d. percentage speedup = 6 / 29 = 20.7%
#### 11.15
* a. At 7200 RPM, the rotational latency is at worst 1/7200 minute (8.33 milliseconds) and on the average it is half that (4.17 ms).
* b. Solving $t = 0.7561 + 0.2439\sqrt{L}$ for t = 4.167 gives L = 195.58, so we can seek over 195 tracks (about 4% of the disk) during an average rotational latency.
#### 11.16
HDDs and NVM devices [compare](https://www.promax.com/blog/explaining-difference-between-the-hdd-and-nvme-drive) and [best applications](https://www.ibm.com/cloud/blog/hard-disk-drive-vs-solid-state-drive)
#### 11.17
NVM devices as a caching tier has faster access time and provides more efficiency than HDD. On the other hand, limited read-write times and data leaks makes it not suitable for sparing or long-time storage device than HDDs.
#### 11.18 [2][7] and additional note [11.14][8]
#### 11.19 [4][7]
#### 11.20 [11.15][8]
#### 11.21 [12.28][5]
#### 11.22
RAID Level 5 organization will be faster than RAID Level 1 organization when writing multiple blocks of data. This is because multiple blocks are split between disks meaning that RAID Level 5 can write concurrently on more than one disk. [compare other aspect](https://www.diffen.com/difference/RAID-1-vs-RAID-5)
#### 11.23 [11.16][8]
#### 11.24 [11.17][8]
#### 11.25 [11.25][6]
#### 11.26 [11.26][6]
[5]: http://hscc.cs.nthu.edu.tw/~sheujp/homework/os09/HW12_ref.pdf
[6]: https://www.studocu.com/en-us/document/jacksonville-state-university/fundamentals-of-computer-operating-systems/cs350-chapter-11/41845684
[7]: https://efreidoc.fr/L3/Operating%20System/Exercises/2012-13/2012-13.exercises.week10.answers.op.pdf4
[8]: https://blog.csdn.net/apple_72111807/article/details/128245197
## Chapter 12
### Practice Exercises
#### 12.1-12.7
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/12.pdf
#### 12.8 [12.8][9]
#### 12.9 [12.9][9]
#### 12.10 [13.3][10]
#### 12.11 [12.11][9]
#### 12.12 [10][11]
#### 12.13 [13.6][10]
#### 12.14 [13.14][12]
#### 12.15 
Direct virtual memory access (DVMA), using virtual addresses that undergo translation to physical addresses. DVMA can perform a transfer between two memory-mapped devices without the intervention of the CPU or the use of main memory. Platforms that support DVMA provide the device with a virtual address rather than a physical address. With this memory access method, the platform translates device accesses to the provided virtual address into the proper physical addresses using a type of Memory Management Unit (MMU). The device transfers data to and from a contiguous virtual image that can be mapped to dis-contiguous physical pages. Devices that operate on these platforms do not require Scatter/Gather DMA capability. [9.1.3 Performing DMA on SPARC](https://www.jungo.com/st/support/documentation/windriver/901/wdpci_man_mhtml/node48.html)
#### 12.16 [13.7][13]
#### 12.18
In a reliable transfer of data, the modules are required to check whether space is available on the target module. It is also required to block the sending module if space is not available. This process requires extra coordination between the modules, but overhead enables the system to provide stronger abstraction than one which does not guarantee the reliable transfer, this abstraction reduces the complexity of the code.

[9]: https://www.studocu.com/en-us/document/jacksonville-state-university/fundamentals-of-computer-operating-systems/cs350-chapter-12/41845698
[10]: https://sites.cs.ucsb.edu/~tyang/class/170.w06/solutions/solution3.html
[11]: https://nanopdf.com/download/exe-c07-io_pdf
[12]: https://framist.github.io/2021/10/08/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F%E4%BD%9C%E4%B8%9A%E5%8D%81%E4%B8%89/
[13]: http://alumni.cs.ucr.edu/~choua/school/cs153/Solution%20Manual.pdf
## Chapter 13
### Practice Exercises
#### 13.1-13.8
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/13.pdf
#### 13.9 [11.1][13]
#### 13.10 [11.10][14]
#### 13.11 [11.11][14]
#### 13.12 [11.12][14]
#### 13.13 [11.8][13]
#### 13.14
When a block is accessed, the file system could prefetch the subsequent blocks in anticipation of future requests to these blocks. This prefetching optimization would reduce the waiting time experienced by the process for future requests.
#### 13.15
A database. A file in the database will be searched for the file by a file pointer; if the file is found, it's contents will be fetched.
#### 13.16 [11.10][13]
[14]: https://framist.github.io/2021/10/08/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F%E4%BD%9C%E4%B8%9A%E5%8D%81%E4%B8%80/
## Chapter 14
### Practice Exercises
#### 14.1-14.6
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/14.pdf
#### 14.1 [explain see 4](https://hackmd.io/@25077667/os-hw5#4-Consider-a-file-currently-consisting-of-100-blocks-Assume-that-the-file-control-block-and-the-index-block-in-the-case-of-indexed-allocation-is-already-in-memory-Calculate-how-many-disk-IO-operations-are-required-for-contiguous-linked-and-indexed-single-level-allocation-strategies-if-for-one-block-the-following-conditions-hold-In-the-contiguous-allocation-case-assume-that-there-is-no-room-to-grow-in-the-beginning-but-there-is-room-to-grow-in-the-end-Assume-that-the-block-information-to-be-added-is-stored-in-memory)
#### 14.7 [11.2][15]
#### 14.8 [12.10][16]
#### 14.9 [12.11][16]
#### 14.10
* a, c [12.2][13]
* b. 4 disk operations.  
  * 1- Reading in the disk block containing the root directory  
  * 2- disk block containing the directories b 
  * 3- disk block containing the directories c 
  * 4- reading in the disk block containing the file
#### 14.11 [11.3][15]
#### 14.12 [14.12](https://www.studocu.com/en-us/document/jacksonville-state-university/fundamentals-of-computer-operating-systems/cs350-chapter-14/41845702)
#### 14.13 
* Advantages
  * There might be more disk space on the other mount point.
  * More transparency because the user doesn’t need to be aware of mount points and create links in all scenarios.
* Disadvantages
  * This is generally finished with symbolic connections, which has the disadvantage that renaming the record won't have the impact you expect or while making a document with a comparable name in a similar area, the document will be made on the first file system. Likewise, renaming documents over the distinctive mount focuses may fail. 
  * Failure to provide transparent access to the file when the file system containing the link might be mounted while the file system containing the target file might not be. In this case, the error condition will show that the particular link is a dead link and that the link does indeed cross filesystem boundaries
#### 14.14 [12.6][13]
#### 14.15 [12.16][16]
#### 14.16 [12.8][13]
#### 14.17 [12.19][16]
#### 14.18 [12.14][13]
#### 14.19 
The advantage is that the application can deal with the failure condition in a more intelligent manner if it realizes that it incurred an error while accessing a file stored in a remote file system. For instance, a file open operation could simply fail instead of hanging when accessing a remote file on a failed server and the application could deal with the failure in the best possible manner; if the operation were simply to hang, then the entire application hangs, which is not desirable. The disadvantage however is the lack of uniformity in failure semantics and the resulting complexity in application code.
#### 14.20
UNIX consistency semantics requires updates to a file to be immediately available to other processes. Supporting such a semantics for shared files on remote file systems could result in the following inefficiencies: all updates by a client have to be immediately reported to the file server instead of being batched (or even ignored if the updates are to a temporary file), and updates have to be communicated by the file server to clients caching the data immediately, again resulting in more communication.

[15]: http://hscc.cs.nthu.edu.tw/~sheujp/homework/os09/HW11_ref.pdf
[16]: https://framist.github.io/2021/06/26/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F%E4%BD%9C%E4%B8%9A%E5%8D%81%E4%BA%8C/
## Chapter 15
### Practice Exercises
#### 15.1-15.5
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/15.pdf
#### 15.6
One issue is the maintenance of the consistency of the name cache. In case the cache entry becomes inconsistent, then either it should be updated or its inconsistency should be detected when it is used for the next time. In case of the inconsistency being detected later, there must be a fallback mechanism to determine the new translation for the name.
#### 15.7 Given a mounted file system with write operations underway, and a system crash or power loss, what must be done before the file system is remounted if: (a) The file system is not log-structured? (b) The file system is log-structured?
* (a) Some NVM storage devices contain a battery or supercapacitor to provide enough power, even during a power loss, to write data from device buffers to the storage media so the data are not lost. But even those precautions do not protect against corruption due to a crash.
* (b) If the system crashes, the log file will contain zero or more transactions. Any transactions it contains were not completed to the file system, even though they were committed by the operating system, so they must now be completed. The transactions can be executed from the pointer until the work is complete so that the file-system structures remain consistent. The only problem occurs when a transaction was aborted—that is, was not committed before the system crashed. Any changes from such a transaction that were applied to the file system must be undone, again preserving the consistency of the file system. This recovery is all that is needed after a crash, eliminating any problems with consistency checking.
#### 15.8 Why do operating systems mount the root file system automatically at boot time?
The root partition selected by the boot loader, which contains the operating-system kernel.
#### 15.9 Why do operating systems require file systems other than root to be mounted?
An operating system has a static mounting preconfiguration that is established at boot time, which enables the operating system to traverse its directory
structure, switching seamlessly among file systems of varying types.
## Chapter 16
### Practice Exercise
#### 16.1 Buffer-overflow attacks can be avoided by adopting a better program-ming methodology or by using special hardware support. Discuss these solutions.
Preventing the execution of code that is found in the stack segment of a process's location space is one sort of hardware support that makes sure that a buffer overflow attack doesn't take place.
#### 16.2 [19.1][13]
#### 16.3 What is the purpose of using a “salt” along with a user-provided pass-word? Where should the salt be stored, and how should it be used?
The salt value is added to the password to ensure that if two plaintext passwords are the same, they result in different hash values. In addition, the salt value makes hashing a dictionary ineffective, because each dictionary term would need to be combined with each salt value for comparison to the stored passwords. Newer versions of UNIX also store the hashed password entries in a file readable only by the superuser. The programs that compare the hash to the stored value run setuid to root, so they can read this file, but other users cannot.
#### 16.4 [19.2][13]
#### 16.5 An experimental addition to UNIX allows a user to connect a watchdog program to a file. The watchdog is invoked whenever a program requests access to the file. The watchdog then either grants or denies access to the file. Discuss two pros and two cons of using watchdogs for security.
The watchdog program becomes the primary security mechanism for file access. Because of this we find its primary benefits and detractions. A benefit of this approach is that you have a centralized mechanism for controlling access to a file—the watchdog program. By ensuring the watchdog program has sufficient security techniques, you are assured of having secure access to the file. However, this is also the primary negative of this approach as well—the watchdog program becomes the bottleneck. If the watchdog program is not properly implemented (that is, it has a security hole), there are no other backup mechanisms for file protection.
#### 16.6 [19.5][13]
#### 16.7 [19.7][13]
#### 16.8 [19.8][13]
#### 16.9 What commonly used computer programs are prone to man-in-the-middle attacks? Discuss solutions for preventing this form of attack. 
Any protocol that requires a sender and a receiver to agree on a session key before they start communicating is prone to the man-in-the-middle attack. Transport Layer Security (TLS) is a cryptographic protocol, which is a complex protocol with many options that enables two computers to communicate securely in which asymmetric cryptography is used so that a client and a server can establish a secure session key that can be used for symmetric encryption of the session between the two—all of this while avoid-ing man-in-the-middle and replay attacks. For added cryptographic strength, the session keys are forgotten once a session is completed. Another communication between the two will require generation of new session keys.
#### 16.10 Compare symmetric and asymmetric encryption schemes, and discuss the circumstances under which a distributed system would use one or the other.
Both encryption methods use keys to encrypt and decrypt data. The main difference is that symmetric encryption uses the same key to encrypt and decrypt data. In contrast, asymmetric encryption uses a pair of keys – a public key to encrypt data and a private key to decrypt information. Symmetric cryptography usually simpler transformations that are not computationally intensive, but less secure. Asymmetric much more computationally intensive, but
very secure (based on cryptographic hardness property of finding prime factors of a number). Asymmetric typically used for authentication, key distribution, small amounts of confidential infomation while symmetric encryption for bulk data encryption.
#### 16.11 Why doesn’t $D_{kd,N}(E_{ke,N}(m))$ provide authentication of the sender? To what uses can such an encryption be put?
$D_{kd,N}(E_{ke,N}(m))$ implies that the message is encrypted using the public key and afterward decoded kd,N ke,N utilizing the private key. The public key crypto systems does not provide the necessary authentication to the receiver. This scheme isn't adequate to ensure validation since any entity can acquire the public keys and accordingly might have created the message. The only entity that can decrypt the message is the entity that owns the private key and provides sufficient security to guarantee authentication.
#### 16.12 Discuss how the asymmetric encryption algorithm can be used to achieve the following goals. <br/>    a. Authentication: the receiver knows that only the sender could have generated the message. <br/>    b. Secrecy: only the receiver can decrypt the message. <br/>    c. Authentication and secrecy: only the receiver can decrypt the message, and the receiver knows that only the sender could have generated the message.
* a. Constraining the set of potential senders of a message by paring public and private key.
* b. The private key (or “secret key”) must be zealously guarded, and can't be derived from public key.
* c. Making sure that the sender uses the right public key, so the message won't be decrypted by man-in-the-middle.
#### 16.13 Consider a system that generates 10 million audit records per day. Assume that, on average, there are 10 attacks per day on this system and each attack is reflected in 20 records. If the intrusion-detection system has a true-alarm rate of 0.6 and a false-alarm rate of 0.0005, what percentage of alarms generated by the system corresponds to real intrusions?
$$\frac{10(intrusion/day) \cdot 20(records/intrusion)}{10^7(records/day)} = 0.00002$$

$$Bayes' theorem: P(I|A) = \frac{P(I) \cdot P(A|I)}{P(I) \cdot P(A|I)+P(\neg I) \cdot P(A|\neg I)} = \frac{0.00002 \cdot 0.6}{0.00002 \cdot 0.6 + 0.99998 \cdot 0.0005} \approx 0.023 = 2.3 \\% $$
#### 16.14 Mobile operating systems such as iOS and Android place the user data and the system files into two separate partitions. Aside from security, what is an advantage of that separation?
The system partition is mounted read-only, whereas the data partition is read–write. This approach has numerous advantages, not the least of which is greater security: the system partition files cannot easily be tampered with, bolstering system integrity. Secondly, it allows for easier maintenance like reinstall, restore and updates of the operating system while remaining user data. Thirdly, user are easier to manage thier data and free up space.
## Chapter 17
### Practice Exercise
#### 17.1-17.6
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/17.pdf
#### 17.11
Yes, this approach is equivalent to including the access privileges of domain B in those of domain A as long as the switch privileges associated with domain B are also copied over to domain A.
#### 17.12
Set up a dynamic protection structure that changes the set of resources available with respect to the time allotted to the three categories of users. As time changes, so does the domain of users eligible to play the computer games. When the time comes that a user’s eligibility is over, a revocation process must occur. Revocation could be immediate, selective (since the computer staff may access it at any hour), total, and temporary (since rights to access will be given back later in the day). 
#### 17.13
An hardware feature that is required for proficient capability manipulation is permitting a capability object to be distinguished as either a capability of accessing object. Typically, several bits are important to recognize the various kinds of capability objects. This couldn't be utilized for routine memory protection since they offer little protection apart from a binary value demonstrating whether they are a capability object or something else.
#### 17.14 [2.a][17]
#### 17.15 [2.b][17]
#### [17.16](https://brainly.com/question/29854236)
#### 17.17
The need-to-know principle: A process can only access these resources it has been authorized and are required to complete its task. Sticking to this rule can limit the damage a process can do to the system.
#### 17.18
* a. The MULTICS ring-protection scheme : The ring protection scheme in MULTICS does not really implement the need-to-know rule. For instance, if an object must be accessible in a domain at ring level j however not available in a domain at ring level i, at that point we should have j<i.j<i. This requirement means that each item available in level i should be open in level j.
* b. JVM’s stack-inspection scheme allow module designers to enforce the need-to-know principle.
#### 17.19
If a Java program could directly alter annotations of its stack frame then it could perform operations it does not have permission. By permitting a Java program to legitimately adjust the annotations of a stack outline, a program might play out an activity for which it doesn't have the essential consents, in this manner abusing the security model of Java.
#### [17.20](https://brainly.in/question/9544375)
#### 17.21
The principle of least privilege: Minimizes the attack surface, diminishing avenues a malicious actor can use to access sensitive data or carry out an attack by protecting superuser and administrator privileges. Reduces malware propagation by not allowing users to install unauthorized applications.
#### 17.22
The guideline of least privilege just restricts the damage but doesn't forestall the abuse of access privilege related to a module if the module were to be undermined. For example, if a system code is given access privileges to manage the errand of managing tertiary storage, a security loophole in the code would not cause any damage to different parts of the system, however, it could even now cause protection failures in getting to the tertiary storage.

[17]: http://www.cs.cornell.edu/courses/cs414/2007sp/homework/hw6_soln.pdf
## Chapter 18
### Practice Exercise
#### 18.1 Describe the three types of traditional hypervisors.
* Type 0 hypervisors are implemented in the hardware and require modifications to the operating system to ensure proper operation. Some type 0 hypervisors offer an example of paravirtualization, in which the operating system is aware of virtualization and assists in its execution.
* Type 1 hypervisors provide the environment and features needed to create, run, and manage guest virtual machines. Each guest includes all of the software typically associated with a full native system, including the operating system, device drivers, applications, user accounts, and so on.
* Type 2 hypervisors are simply applications that run on other operating systems, which do not know that virtualization is taking place. These hypervisors do not have hardware or host support so must perform all virtualization activities in the context of a process.
#### 18.2 Describe four virtualization-like execution environments, and explain how they differ from “true” virtualization.
* Paravirtualization: the guest must be modified to run on the paravirtualized virtual hardware. The gain for this extra work is more efficient use of resources and a smaller virtualization layer.
* Programming-environment virtualization is part of the design of a programming language. The language specifies a containing application in which programs run, and this application provides services to the programs.
* Emulation is used when a host system has one architecture and the guest was compiled for a **different architecture**. Every instruction the guest wants to execute must be translated from its instruction set to that of the native hardware. Although this method involves some performance penalty, it is balanced by the usefulness of being able to run old programs on newer, incompatible hardware or run games designed for old consoles on modern hardware.
* Application containment create a virtual layer between the operating system and the applications. In this system, only one kernel is installed, and the hardware is not virtualized. Rather, the operating system and its devices are virtualized, providing processes within a zone with the impression that they are the only processes on the system. Containers use fewer system resources and are faster to instantiate and destroy, more similar to processes than virtual machines.
#### 18.3 Describe four benefits of virtualization.
* The host system is protected from the virtual machines, just as the virtual machines are protected from each other.
* The ability to freeze, or **suspend**, a running virtual machine and allow copies and **snapshots** to be made of the guest. The copy can be used to create a new VM or to move a VM from one machine to another with its current state intact. The guest can then **resume** where it was, as if on its original machine, creating a **clone**.
* System programmers are given their own virtual machine, and system development is done on the virtual machine instead of on a physical machine. Rapid porting and testing of programs in varying environments. In addition, multiple versions of a program can run, each in its own isolated operating system, within one system. Similarly, quality-assurance engineers can test their applications in multiple environments.
* It Improves not only resource utilization but also resource management. Virtual machines in production data-center use provides system **consolidation**. Such physical-to-virtual conversions result in resource optimization, since many lightly used systems can be combined to create one more heavily used system. **Templating**, in which one standard virtual machine image, including an installed and configured guest operating system and applications, is saved and used as a source for multiple running VMs. Other features include managing the patching of all guests, backing up and restoring the guests, and monitoring their resource use. A **live migration** feature that moves a running guest from one physical server to another without interrupting its opera-
tion or active network connections. If a server is overloaded, live migration can thus free resources on the source host while not disrupting the guest. Similarly, when host hardware must be repaired or upgraded, guests can be migrated to other servers.
#### 18.4 Why are VMMs unable to implement trap-and-emulate-based virtual-ization on some CPUs? Lacking the ability to trap and emulate, what method can a VMM use to implement virtualization?
Some CPUs do not have a clean separation of privileged and nonprivileged instructions. Unfortunately for virtualization implementers, the Intel x86 CPU
line is one of them, which has maintained backwards compatibility and accordingly similar issues with virtualization. If the CPU is in user mode, then only
some flags are replaced, and others are ignored. Because no trap is generated if these *special instructions* is executed in user mode, the trap-and-emulate procedure is rendered useless. This problem was solved with **binary translation** technique. If the guest VCPU is in kernel mode, Instructions other than special instructions are run natively. Special instructions are translated into a new set of instructions that perform the equivalent task. It is implemented by translation code within the VMM. The code reads native binary instructions dynamically from the guest, on demand, and generates native binary code that executes in place of the original code.
#### 18.5 What hardware assistance for virtualization can be provided by modern CPUs?
* Guest VCPU state data structures to load and save guest CPU state automatically during guest context switches. In addition, **virtual machine control structures (VMCSs)** are provided to manage guest and host state, as well as various guest execution controls, exit controls, and
information about why guests exit back to the host.
* Nested page tables in hardware to allow the VMM to fully control paging while the CPUs accelerate the translation from virtual to physical addresses. The NPTs add a new layer, one representing the guest’s view of logical-to-physical address translation. The CPU page-table walking function (traversing the data structure to find the desired data) includes this new layer as necessary, walking through the guest table to the VMM table to find the physical address desired.
* Hardware-assisted DMA. First, the VMM sets up protection domains to tell the CPU which physical memory belongs to each guest. Next, it assigns the I/O devices to the protection domains, allowing them direct access to those memory regions and only those regions. In this manner, DMA transfers are passed through between a guest and a device without VMM interference.
* Interrupt remapping feature automatically deliver an interrupt destined for a guest to a core that is currently running a thread of that guest. That way, the guest receives interrupts without any need for the VMM to intercede in their delivery. Without interrupt remapping, malicious guests could generate interrupts that could be used to gain control of the host system.
#### 18.6 Why is live migration possible in virtual environments but much less possible for a native operating system?
Without virtualization: we must warn users, shut down the processes, possibly move the binaries, and restart the processes on the new system. Only then can users access the services again. With live migration, we can decrease the load on an overloaded system or make hardware or system changes with no discernable disruption for users.
## Chapter 19
### Practice Exercise
#### 19.1 [15.8][18]
#### 19.1-19.6
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/19.pdf
#### 19.7
In computation migration, an RPC might be sent to a remote processor in order to execute a computation that could be more efficiently executed on the remote node. Whereas, in process migration, the entire process is transported to the remote node, where the process continues its execution.
#### 19.8
The OSI model formalizes some of the earlier work done in network protocols but was developed in the late 1970s and is currently not in widespread use. A specific network layered-protocol may accomplish the equivalent usefulness of the ISO in less layers by utilizing one layer to execute usefulness provided in two (or conceivably more) layers in the ISO model. Different models may conclude there is no requirement for specific layers in the ISO model. For instance, the presentation and session layers are missing in the TCP/IP convention, because it combines several functions in each layer, it is more difficult to implement but more efficient than OSI networking. Protocals with Omitted layers lose some function or header informations and securities.
#### 19.9 [15.6][13]
Increasing the speed could require the traffic packets to be broken down into smaller bits, which could result in dropped packets or collisions. Faster Systems might have the option to send more parcels in a more limited measure of time. The network would then have more parcels travellingon it, resulting in more collisons, and along these lines less throughput relative to the number of packets being sent. More networks can be utilised, with less systems per network, to decrease the quantity of crashes.
#### 19.10
A disadvantage is that routers or gateways as dedicated devices may be more costly than using off-the-shelf components that comprise a modern personal computer. The advantages of using dedicated hardware devices for routers and gateways are that they very fast as all their logic is provided in hardware (firmware.)
#### 19.11 [15.10][13], [15.9][18]
#### 19.12
Hierarchial structures are important as they make it easy to maintain changes. In an hierarchial structure any changes in the identity of name servers require an update only at the next level name server in the hierarchy. Changes are therefore localized.
#### 19.13
The transport layer supports [reliable delivery](https://www.javatpoint.com/computer-network-transport-layer), which has four aspects:
* Error control
* Sequence control
* Loss control
* Duplication control
In transport layer acknowledgement is sent for whole message. if you only provide error control at transport layer then, there is no way u can detect error at particular frame. so transport layer have to send whole message again. In data link layer acknowledge sent for node to node(hop to hop) for each frame. so if any frame is not received correctly then only that frame is send again from failed router, no need to send again from sender. A link-layer reliable-delivery service is often used for links that are prone to high error rates, such as a wireless link. The goal is to correct an error locally, on the link where the error occurs, rather than forcing an end-to-end retransmission of the data by a transport - layer or application-layer protocol.
#### 19.16
UDP can't be used as an appropriate alternative to TCP for HTTP even though it is connection less in nature. UDP is unreliable in nature and the documents delivered by the web must be delivered reliably, hence UDP can't be used.(This is anything but difficult to outline - a solitary packet missing from a picture downloaded from the web makes the picture unreadable.) To improve HTTP performance we can modify how TCP connections are used like [caching](https://www.justanswer.com/computer-networking/77sdw-original-http-protocol-used-tcp-ip-underlying-network.html) the data and reduce duplicated data transmission.
#### 19.17 [15.13][13]
#### 19.18 
The benefits of a DFS compared with a file system in a centralized system include increased performance and fault tolerability as well as higher availability. Because multiple copies of all files live on different file servers, if one of those nodes fails, your file from another location is still available. A transparent DFS facilitates client mobility by bringing the client’s environment to the site where the client logs in.
#### 19.19
The main goal of a client–server architecture is to allow transparent file sharing among one or more clients as if the files were stored locally on the individual client machines. If many applications need to be run in parallel on large data sets with high availability and scalability, the cluster-based model is more appropriate than the client–server model.
* Hosting student files in a university lab: client-server model
* Processing data sent by the Hubble telescope: cluster-based model. Computer clustering can help resolve this problem by using redundant components and clustering methods such that failures are detected and failing over to working components continues server operations.
* Sharing data with multiple devices from a home server: client-server model
#### 19.20 [17.3][19]
* Location transparency: The name of a file does not reveal any hint of the file’s physical storage location.
* Location independence: The name of a file need not be changed when the file’s physical storage location changes. Files can be moved automatically between different file systems when the file is migrated.
#### 19.21 [17.4][19]
#### 19.22 [17.5][19]
#### 19.23 [17.7][19]
#### 19.24 
Block level deduplication is always efficient then file-level deduplication because In file level you have to dump whole file in data storage if its version changed where as in block level you have to dump the changed block which takes comparatively less space in data storage. [ref](https://akashtiwari.github.io/)
#### 19.25 [Data Deduplication metadata list](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831434(v=ws.11)?redirectedfrom=MSDN)
[18]: https://courses.cs.washington.edu/courses/cse451/98au/Section/ch15/
[19]: https://studylib.net/doc/8644957/distributed-file-systems
## Chapter 20
### Practice Exercises
#### 20.1-20.6
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/20.pdf
#### 20.7
* Advantages
The code can be written faster, is more compact, and is easier to understand and debug. In addition, improvements in compiler technology will improve the generated code for the entire operating system by simple recompilation. Finally, an operating system is far easier to port — to move to some other hardware — if it is written in a higher-level language.
* Disadvantages
An OS needs low-level access to memory and hardware and perform dirty tricks on them. This kind of access is generally considered unsafe for application-level programs, so many high-level languages don't allow it.

An OS needs to execute without support software being present, such as interpreters. This makes it extremely hard to write an OS in a language that can't easily be compiled into native instructions.
#### 20.8
Fork() system call is used to create a new process and exec() system call executes this process same as its parent process is running. vfork() is a special case of clone and is used to create new processes without copying the page tables of the parent process but it is not suitable for certain programs where the parent and child processes interact before the child performs an exec. For such programs, the system-call sequence fork() exec() more appropriate.
#### 20.9
Sockets of type SOCK STREAM utilize the TCP protocol for communicating data. The TCP protcol is appropriate for implementing an intercomputer file transfer program since it gives a reliable, flow controlled, and congestion friendly, communication channel. In the event that data packets corresponding to a file transfer are lost, at that point they are retransmitted. Besides, the file transfer doesn't overrun buffer resources at the receiver and adjusts to the accessible bandwidth along the channel. Sockets of type SOCK DGRAM use the UDP protocol for communicating information. The UDP protocol is more fitting for checking whether another PC is up on the network. Since a connection-oriented communication channel isn't needed and since there may not be any active entities on the opposite side to build up a communication channel with, the UDP convention is more suitable.
#### 20.10
The organisation of architecture-dependent and architecture-free code in the Linux kernel is intended to fulfill two design goals: to keep as much code as could reasonably be expected between architectures and to give a perfect method of characterizing architecture specific properties and code. The solution should obviously be consistent with the overriding aims of code maintainability and performance. There are various levels of architecture reliance in the kernel,and various methods are proper for each case to comply with the design requirements. These levels include:

* a. CPU word size and endianness. These are issues that influence the portability of all software written in C, however particularly so for an operating system, where the size and arrangement of data should be carefully arranged.

* b. CPU process architecture . Linux depends on numerous types of hardware support for its process and memory management. Different processors have their own mechanisms for changing between protection domains (e.g., entering kernel mode from user mode),rescheduling processes, overseeing virtual memory, and handling incoming interrupts.
#### 20.11
The advantage of making just a portion of the symbols defined inside a kernel accessible to a loadable kernel module is that there is a fixed set of entry points made available to the kernel module. This ensures that loadable modules can't invoke arbitrary code inside the kernel and thereby meddle with the kernel's execution. By limiting the set of entry points, the kernel is ensured that the interactions with the module occur at controlled points where certain invariants hold. The disadvantage of making just a small set of the symbols defined available to the kernel module is the loss in flexibility and might at times lead to a performance issue as some of the details of the kernel are hidden from the module.
#### 20.12
Conflict resolution keeps various modules from having conflicting access to hardware resources. Specifically, when multiple drivers are trying to access same hardware, it resolves the resulting conflict. This mechanism allows different device drivers to reserve hardware resources and to protect those resources from accidental use by another driver.
#### 20.13
In Linux, threads are implemented within the kernel by aclone mechanism that creates a new process within the same virtualaddress space as the parent process. Unlike some kernel-based threadpackages, the Linux kerneldoes not make any distinction betweenthreads and processes: a thread is simply a process that did not createa new virtual address space when it was initialized.The main advantage of implementing threads in the kernel rather thanin a user-mode library are that:
* kernel threaded systems can take advantage of multiple processorsif they are available.
* if one thread blocks in a kernel service routine (for example, asystem call or page fault), other threads are still able to run.
#### 20.14
Linux threads are kernel-level threads. The threads are visibleto the kernel and are independently scheduleable. User-level threads,on the other hand, are not visible to the kernel and are instead manip-ulated by user-level schedulers.In addition, the threads used in theLinux kernel are used to support both the thread abstraction and theprocess abstraction. A new process is created by simply associated anewly created kernel thread with a distinct address space, whereas anew thread is created by simply creating a new kernel thread with thesame address space. This further indicates that the thread abstaction isintimately tied into the kernel.
#### 20.15
In Linux, creation of a thread involves only the creationof some very simple data structures to describe the new thread. Spacemust be reserved for the new thread’s execution context its saved regis-ters, its kernel stack page and dynamic information such as its securityprofile and signal state but no new virtual address space is created.Creating this new virtual address space is the moste xpensive part of the creation of a new process. The entire page table of the parent process must be copied, with each page being examined so that copy-on-write semantics can be achieved and so that reference counts to physical pages can be updated. The parent process’s virtual memory is also affected by the process creation: any private read/write pages owned by the parent must be marked read-only so that copy-on-write can happen (copy-on-write relies on a page fault being generated when a write to the page occurs).
#### 20.16
The Completely Fair Scheduler (CFS) gives improved fairness over traditional process schedulers by relegating each process to a proportion of the processor, rather than a fixed time slice. CFS thus yields constant fairness but a variable switching rate. As the number of runnable processes on a system approaches infinity, the proportion of allotted processors approaches zero. To guarantee that processes at least a minimum amount of the processor, CFS places a floor on the proportion of processor each process is allotted, called the minimum granularity. Thus CFS guarantees fairness only when the number of runnable processes isn't huge that the proportion of allocated processor is floored by the minimum granularity. In the regular instance of just a handful of runnable processes, CFS is entirely reasonable.
#### 20.17
The Completely Fair Scheduler (CFS) gives two essential configuration knobs: minimum granularity and target latency. The minimum granularity sets a floor on the amount of processor that CFS allots each runnable process, limiting switching costs at the expense of fairness guarantee. Assigning a very small value will extend the fairness assurance to a bigger number of runnable processes, however will increase switching costs as those processes will each run for an extremely small amount of time. An exceptionally large value will yield the opposite: Processes will run for longer periods, however a generally smaller number of runnable processes will cause CFS to abandon its fairness guarantee.
#### 20.18
Linux’s “soft” real-time scheduling provides ordering guar-antees concerning the priorities of runnable processes: real-time pro-cesses will always be given a higher priority by the scheduler thannormal time-sharing processes, and a real-time process will never beinterrupted by another process with a lower real-time priority.

However, the Linux kernel does not support “hard” real-time func-tionality. That is, when a process is executing a kernel service routine,that routine will always execute to completion unless it yields controlback to the scheduler either explicitly or implicitly (by waiting for someasynchronous event). There is no support for preemptive scheduling ofkernel-mode processes. As a result, any kernel system call that runs for a significant amount of time without rescheduling will block executionof any real-time processes.

Many real-time applications require such hard real-time scheduling. Inparticular, they often require guaranteed worst-case response times toexternal events. To achieve these guarantees, and to give user-mode realtime processes a true higher priority than kernel-mode lower-priorityprocesses, it is necessary to find a way to avoid having to wait for low-priority kernel calls to complete before scheduling a real-time process.For example, if a device driver generates an interrupt that wakes upa high-priority real-time process, then the kernel needs to be able to schedule that process as soon as possible, even if some other process isalready executing in kernel mode.

Such preemptive rescheduling of kernel-mode routines comes at a cost.If the kernel cannot rely on non-preemption to ensure atomic updates of shared data structures, then reads of or updates to those structuresmust be protected by some other, finer-granularity locking mechanism.This fine-grained locking of kernel resources is the main requirementfor provision of tight scheduling guarantees.

Many other kernel features could be added to support real-time pro-gramming. Deadline-based scheduling could be achieved by makingmodifications to the scheduler. Prioritization of IO operations could beimplemented in the block-device IO request layer.
#### 20.19
Uninitialized data can be backed by demand-zero memoryregions in a process’s virtual address space. In addition, newly malloced space can also be backed by a demand-zero memory region.
#### 20.20
When a process performs a fork operation, another process is created based on the original binary however with new address space that is a clone of the original address space. One chance is to not make a new address space yet rather to share the address space between the old process and the recently created process. The pages of the address space are planned with the copy-on-write characteristic enabled. Then, when one of the processes performs an update on the shared address space, again copy is made and the processes presently don't have the same page of the address space.
#### 20.21
There are various purposes behind keeping functionality in shared libraries instead of in the kernel itself. These include:
* a. Reliability. Kernel mode programming is naturally higher risk than user mode programming. In case the kernel is coded correctly so that protection between processes is enforced, then an occurrence of a bug in a user mode library is probably going to affect just the currently executing process, though a comparable bug in the kernel could conceivably cut down the whole operating system.
* b.Performance. Keeping however much functionality as could be expected in user mode shared libraries helps performance in two different ways. First of all, it diminishes physical memory consumption: Kernel memory is non-pageable, so every kernel function is for all time resident in physical memory, but a library function can be paged in from disk on request and shouldn't be truly present all of the time. Despite the fact that the library function might be resident in many processes at once, page sharing by the virtual memory system means that it is loaded at most once physical memory.

Second, calling a function in a loaded library is an exceptionally fast operation, yet calling a kernel function through a kernel system service call is substantially more costly. Entering the kernel includes changing the CPU protection domain, and once in the kernel, all of the arguments provided by the process must be deliberately checked for correctness: the kernel can't bear to make any presumptions about the legitimacy of the arguments passed in, though a library function may sensibly do as such. Both of these elements make calling a kernel function much more slow than calling a similar function in a library.
#### 20.22
There are a number of advantages to using a journaling files system.

In a non-journaled file system, problem is that following a crash the fsck (filesystem consistency check) utility has to be run. fsck will scan the entire filesystem validating all entries and making sure that blocks are allocated and referenced correctly. If it finds a corrupt entry it will attempt to fix the problem. The issues here are two-fold. Firstly, the fsck utility will not always be able to repair damage and you will end up with data in the lost+found directory. This is data that was being used by an application but the system no longer knows where they were reference from. The other problem is the issue of time. It can take a very long time to complete the fsck process on a large file system leading to unacceptable down time.

A journaled file system records information in a log area on a disk (the journal and log do not need to be on the same device) during each write. This is a essentially an "intent to commit" data to the filesystem. The amount of information logged is configurable and ranges from not logging anything, to logging what is known as the "metadata" (i.e ownership, date stamp information etc), to logging the "metadata" and the data blocks that are to be written to the file. Once the log is updated the system then writes the actual data to the appropriate areas of the filesystem and marks an entry in the log to say the data is committed.

After a crash the filesystem can very quickly be brought back on-line using the journal log reducing what could take minutes using fsck to seconds with the added advantage that there is considerably less chance of data loss or corruption.
#### 20.23
There are numerous ramifications to supporting different file system types inside the Linux kernel. For one thing, the file system interface ought to be independent of the data layouts and data structures used inside the file system to store file data . For another thing, it may have to give interfaces to file systems where the file data isn't static data and isn't stored on the disk; all things considered, the file data could be computed each time an operation is invoked to access it, just like the case with the /proc file system. These call for a fairly general virtual interface to sit on top of the distinctive file systems.
#### 20.24
Linux augments the standard setuid feature in mainly two ways.

It allows a program to drop and reacquire its effective uid repeatedly. In order to minimize the amount of time that a program executes with all of its privileges, a program might drop to a lower privilege level and thereby prevent the exploitation of security loopholes at the lower-level. However, when it needs to perform privileged operations, it can switch to its effective uid.

Linux allows a process to take on only a subset of the rights of the effective uid. For instance, an user can use a process that serves files without having control over the process in terms of being able to kill or suspend the process.
#### 20.25
The open accessibility of a operating system's source code has both positive and negative effects on security, and it is presumably a mistake to state that it is certainly something worth being thankful for or a terrible thing. Linux's source code is available for investigation by both the good guys and the bad guys. In its favor, this has brought about the code being examined by an enormous number of individuals who are worried about security and who have eliminated any vulnerabilities they have found.

Then again is the security through obscurity argument, which expresses that attacker jobs are made simpler if they have access to the source code of the system they are attempting to penetrate. By denying attackers information about a system, the expectation is that it will be harder for those attackers to discover and abuse any security weaknesses that might be present.
## Chapter 21
### Practice Exercises
#### 21.1-21.13
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/21.pdf
#### 21.14
Deferred procedure calls are utilized to delay interrupt on processing in circumstances where the processing of device interrupts can be broken into a critical portion that is utilized to unblock the device and a non-critical portion that can be scheduled later at a lower priority. The non-critical segment of code is scheduled for later execution by queuing a deferred procedure call.
#### 21.15
User mode code can access kernel mode objects by using a reference value called a handle. An object handle is in this way an identifier (unique to a process) that permits access and manipulation of a system resource. At the point when a user mode process needs to use an object it calls the object manager's open method. A reference to the object is inserted in the process' object table and a handle is returned. Processes can acquire handles by making an object , opening a current object, accepting a copied handle from another process, or by acquiring a handle from a parent process.
#### 21.16
The VM Manager utilizes a page based management scheme. Pages of information assigned to a process that are not in physical memory are put away in either paging fiels on disk or mapped to a regular file on a local or remote file system. To improve execution of this plan, a privileged process is permitted to secure selected pages in physical memory keeping those pages from being paged out. Moreover, since when a page is utilised, adjacent pages will probably be utilized soon, adjacent pages are prefetched to lessen the total number of page deficiencies.
#### 21.17
At the point when a process accesses a no-access page, an exemption is raised. This feature is utilized to check whether a faulty program accesses past the end of an array. The array should be allocated in a way with the end goal that it shows up toward the end of a page, so that buffer overruns would cause exemptions.
#### 21.18
Data is communicated using one of the following three facilities:
* messages are simply copied from one process to the other.
* a shared memory segment is created and messages simply contain a pointer into the shared memory segment, thereby avoiding copies between processes.
* a process directly writes into the other process’s virtual space.
#### 21.19
As opposed to other operating systems where caching is done by the file system, Windows XP gives a centralized cache manager which works closely with the VM supervisor to give caching services to all parts under control of the I/O manager. The size of the cache changes dynamically relying on the free memory accessible in the system. The cache manager maps files into the upper portion of the system cache address space. This cache is separated into blocks which can each hold a memory-mapped region of a record.
#### 21.20
NTFS is usually called the hierarchical or directory tree model. The "base" of the directory structure is the root directory, which is actually one of the key system metadata files on an NTFS volume. Within this root directory, references are stored to files, or to other directories. Unix uses a hierarchical file system structure, much like an upside-down tree, with root (/) at the base of the file system and all other directories spreading from there. It has a root directory (/) that contains other files and directories.
#### 21.21
A process manages the resources required to execute a program. Microsoft's Windows OS manages processes using executable units called threads. Each process is protected from other processes, and contains its own virtual address space, which it shares with all of the threads within the process.
#### 21.22
A fiber is a user-mode code that is scheduled according to a user-defined scheduling algorithm. Its execution is continuous, which means that it has a defined beginning and an end. The fiber abstraction provided by Windows is a user-mode facility and the kernel is not aware that fibers exist.
A fiber is a process's sequential stream of execution. Multiple fibers can exist within a process, but unlike threads, only one fiber can be active at once. To support legacy applications created for a fiber-execution model, the fiber mechanism is used.
This is a part of application processing. Although this may not always be the case depending on the operating system, threads are typically thought of as preemptive whereas fibers are thought of as lightweight, cooperative threads. Both are different ways for your application to run.
* Threads: The current execution path for threads may at any time be interrupted or preempted.
* Fibers: Only when the fiber yields execution does the current execution route with fibers get halted.
#### 21.23
User-mode scheduling (UMS) is a lightweight mechanism that applications can use to schedule their own threads. An application can switch between UMS threads in user mode without involving the system scheduler and regain control of the processor if a UMS thread blocks in the kernel. UMS threads differ from fibers in that each UMS thread has its own thread context instead of sharing the thread context of a single thread. The ability to switch between threads in user mode makes UMS more efficient than thread pools for managing large numbers of short-duration work items that require few system. Unlike fibers, UMS is not intended to be used directly by programmers. The details of writing user-mode schedulers can be very challenging, and UMS does not include such a scheduler. Rather, the schedulers come from programming language libraries that build on top of UMS.
#### 21.24
