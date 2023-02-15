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
