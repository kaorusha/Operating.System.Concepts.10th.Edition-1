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
#### 11.11 [12.18][1]
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
#### 11.18 [2][3] and additional note [11.14][4]
#### 11.19 [4][3]
#### 11.20 [11.15][4]
#### 11.21 [12.28][1]
#### 11.22
RAID Level 5 organization will be faster than RAID Level 1 organization when writing multiple blocks of data. This is because multiple blocks are split between disks meaning that RAID Level 5 can write concurrently on more than one disk. [compare other aspect](https://www.diffen.com/difference/RAID-1-vs-RAID-5)
#### 11.23 [11.16][4]
#### 11.24 [11.17][4]
#### 11.25 [11.25][2]
#### 11.26 [11.26][2]
[1]: http://hscc.cs.nthu.edu.tw/~sheujp/homework/os09/HW12_ref.pdf
[2]: https://www.studocu.com/en-us/document/jacksonville-state-university/fundamentals-of-computer-operating-systems/cs350-chapter-11/41845684
[3]: https://efreidoc.fr/L3/Operating%20System/Exercises/2012-13/2012-13.exercises.week10.answers.op.pdf4
[4]: https://blog.csdn.net/apple_72111807/article/details/128245197
## Chapter 12
### Practice Exercises
#### 12.1-12.7
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/12.pdf
#### 12.8 [12.8][1]
#### 12.9 [12.9][1]
#### 12.10 [13.3][2]
#### 12.11 [12.11][1]
#### 12.12 [10][3]
#### 12.13 [13.6][2]
#### 12.14 [13.14][4]
#### 12.15 
Direct virtual memory access (DVMA), using virtual addresses that undergo translation to physical addresses. DVMA can perform a transfer between two memory-mapped devices without the intervention of the CPU or the use of main memory. Platforms that support DVMA provide the device with a virtual address rather than a physical address. With this memory access method, the platform translates device accesses to the provided virtual address into the proper physical addresses using a type of Memory Management Unit (MMU). The device transfers data to and from a contiguous virtual image that can be mapped to dis-contiguous physical pages. Devices that operate on these platforms do not require Scatter/Gather DMA capability. [9.1.3 Performing DMA on SPARC](https://www.jungo.com/st/support/documentation/windriver/901/wdpci_man_mhtml/node48.html)
#### 12.16 [13.7][5]
#### 12.18
In a reliable transfer of data, the modules are required to check whether space is available on the target module. It is also required to block the sending module if space is not available. This process requires extra coordination between the modules, but overhead enables the system to provide stronger abstraction than one which does not guarantee the reliable transfer, this abstraction reduces the complexity of the code.

[1]: https://www.studocu.com/en-us/document/jacksonville-state-university/fundamentals-of-computer-operating-systems/cs350-chapter-12/41845698
[2]: https://sites.cs.ucsb.edu/~tyang/class/170.w06/solutions/solution3.html
[3]: https://nanopdf.com/download/exe-c07-io_pdf
[4]: https://framist.github.io/2021/10/08/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F%E4%BD%9C%E4%B8%9A%E5%8D%81%E4%B8%89/
[5]: http://alumni.cs.ucr.edu/~choua/school/cs153/Solution%20Manual.pdf
## Chapter 13
### Practice Exercises
#### 13.1-13.8
https://codex.cs.yale.edu/avi/os-book/OS10/practice-exercises/PDF-practice-solu-dir/13.pdf
#### 13.9 [11.1][1]
#### 13.10 [11.10][2]
#### 13.11 [11.11][2]
#### 13.12 [11.12][2]
#### 13.13 [11.8][1]
#### 13.14
When a block is accessed, the file system could prefetch the subsequent blocks in anticipation of future requests to these blocks. This prefetching optimization would reduce the waiting time experienced by the process for future requests.
#### 13.15
A database. A file in the database will be searched for the file by a file pointer; if the file is found, it's contents will be fetched.
#### 13.16 [11.10][1]
[1]: http://alumni.cs.ucr.edu/~choua/school/cs153/Solution%20Manual.pdf
[2]: https://framist.github.io/2021/10/08/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F%E4%BD%9C%E4%B8%9A%E5%8D%81%E4%B8%80/
