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
* 
