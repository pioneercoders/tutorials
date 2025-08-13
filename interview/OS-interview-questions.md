####  1. What is an Operating System?
An Operating System (OS) is system software that acts as an interface between the user and the hardware. It manages resources like CPU, memory, and I/O devices, and provides services such as process management, file management, and security.
Examples: Windows, Linux, macOS, Android.

#### 2. What are the main functions of an OS?
Process Management – Scheduling, execution, and termination of processes.

Memory Management – Allocating and freeing memory for processes.

File System Management – Handling storage, retrieval, and organization of files.

I/O Device Management – Communication with hardware devices.

Security & Protection – Controlling access to system resources.

User Interface – CLI or GUI for user interaction.

#### 3.What is a process?

A process is a program in execution. It consists of:

Program Code (text section)

Program Counter (next instruction to execute)

Stack (function calls, local variables)

Heap (dynamically allocated memory)

Data Section (global variables)

#### 4.What are the different states of a process?

New – Process is being created.

Ready – Process is ready to run, waiting for CPU.

Running – Process is currently executing.

Waiting – Process is waiting for I/O or event.

Terminated – Process has finished execution.

#### 5. What is the difference between process and thread?
## Differences between process and thread

| Process | Thread |
| ------- | ------ |
| Independent unit with its own memory space. | Shares memory space with other threads in the same process. |
| Heavier, requires more resources to create. | Lightweight, faster to create. |
| Context switch is slower. | Context switch is faster. |



#### 6.What is deadlock?

Deadlock occurs when a set of processes are blocked because each process is holding a resource and waiting for another resource held by another process, creating a circular wait.
Conditions for Deadlock (Coffman’s conditions):

Mutual Exclusion

Hold and Wait

No Preemption

Circular Wait

#### 7.How can deadlock be prevented?

Avoid Mutual Exclusion – Use shareable resources if possible.

Avoid Hold and Wait – Request all resources at once.

Allow Preemption – Forcefully take a resource from a process.

Avoid Circular Wait – Impose an ordering on resource requests.

#### 8.What is virtual memory?

Virtual memory is a memory management technique where the OS uses a combination of RAM and disk space to give an illusion of a larger memory space. It allows programs to use more memory than physically available.
Implemented using: Paging or Segmentation.

#### 9.What is paging?

Paging is a memory management scheme that eliminates external fragmentation by dividing memory into fixed-size blocks:

Pages – Fixed-size blocks in logical memory.

Frames – Fixed-size blocks in physical memory.
The OS maintains a page table to map pages to frames.

#### 10.What is segmentation?

Segmentation is a memory management technique where memory is divided into variable-sized segments based on logical divisions such as functions, arrays, or objects.
Each segment has:

Segment Number

Segment Offset

#### 11. What is the difference between paging and segmentation?
| Paging                                                                | Segmentation                                                          |
| --------------------------------------------------------------------- | --------------------------------------------------------------------- |
| Fixed-size blocks.                                                    | Variable-size blocks.                                                 |
| Prevents external fragmentation but may cause internal fragmentation. | Prevents internal fragmentation but may cause external fragmentation. |
| Mapping is page-based.                                                | Mapping is segment-based.                                             |


#### 12.What is a scheduling algorithm?
A scheduling algorithm decides the order in which processes access the CPU.
Types:

FCFS (First Come First Serve) – Processes executed in arrival order.

SJF (Shortest Job First) – Process with smallest execution time first.

Priority Scheduling – Based on process priority.

Round Robin – Each process gets a fixed time slice.

Multilevel Queue – Separate queues for different process types.

#### 13.What is a page fault?
A page fault occurs when a program tries to access a page not currently in RAM. The OS then:

Pauses the process.

Loads the required page from disk to RAM.

Updates the page table.

Resumes execution.

#### 14.What is a context switch?
A context switch is the process of saving the state of a currently running process and loading the state of another process.
It involves:

Saving CPU registers, program counter, and memory state.

Loading the saved state of the next process.

#### 15.What is the difference between multitasking, multithreading, and multiprocessing?
Multitasking – Multiple processes share CPU time.

Multithreading – Multiple threads within a process share CPU time.

Multiprocessing – Multiple CPUs execute processes simultaneously.

#### 16.What is demand paging?

Demand paging loads a page into memory only when it is needed, rather than preloading all pages at process start.

#### 17.What is thrashing?

Thrashing occurs when the system spends more time swapping pages in and out of memory than executing actual processes, due to insufficient RAM or poor paging policy.

#### 18.What is a semaphore?
A semaphore is a synchronization tool used to control access to a shared resource in concurrent programming.

Binary Semaphore – Value 0 or 1, works like a lock.

Counting Semaphore – Allows multiple instances of a resource.

#### 19.What is the difference between internal and external fragmentation?
Internal Fragmentation – Wasted space inside allocated memory blocks due to fixed allocation sizes.

External Fragmentation – Wasted space between allocated memory blocks due to variable-size allocations.

#### 20.What is the difference between kernel mode and user mode?

| Kernel Mode                                   | User Mode                        |
| --------------------------------------------- | -------------------------------- |
| Full access to hardware and system resources. | Restricted access to resources.  |
| Runs OS services.                             | Runs user applications.          |
| Switching requires a mode bit change.         | Cannot directly access hardware. |

