## Processes

### What is a process?
A process is an instance of a program running.

### Multi Processes
Moderns OSes run multiple processes simultaneously. Multiple processes can increase CPU utilization and reduce latency.

#### A Process's View
Each process has own view of machine:
- Own address space
- Own open files
- Own virtual CPU

#### Inter-Process Communication
How can processes interact in real time?
- By passing messages via kernel
- By sharing a region of physical memory
- By asynchronous signals or alerts

## User View of Processes
#### Creating Processes
1. `int fork (void);`
  - Create a copy of current process
  - Return process ID
2. `int waitpid (int pid, int *stat, int opt);`

#### Deleting Processes
1. `void exit (int status);`
  - Current process ceases to exist
2. `int kill (int pid, int sig);`
  - Send sig to process *pid*
  - SIGTERM most common vale, terminate process
  - SIGKILL stronger, kills process always

#### Running Processes
1. `int execve (char *prog, char **argv, char **envp);`

## Kernel View of Processes
#### Process Control Block (PCB)
- Called proc in Unix, task_struct in Linux, and just struct thread in Pintos.
- Tracks state of the process, running, ready (runnable), waiting, etc.
- Includes registers, virtual memory mapping, open files, etc.
- Other data about the process, credentials, signal mask, controlling terminal, priority, and etc.

#### Process States
Process can be in one of several states.
- new: beginning of life
- running: currently executing
- ready: can run, but kernel has chosen different process to run
- waiting: needs async event (e.g. disk operation) to proceed
- terminated: end of life

#### Scheduling
If there are >1 runnable process, how to pick which process to run? - No universal policy.

- Context Switch: changing running processes is called context switch.

## Threads
A thread is a schedulable execution context.
- Simple program use one thread per process, but can also have multi-threaded programs.
- All threads in one process share memory, file descriptors, etc.

#### Thread API
1. ` tid thread_create (void (*fn) (void *), void *);`
- Create a new thread
2. `void thread_exit();`
- Destroy current thread
3. `void thread_join (tid thread);`
- Wait for thread to exit.

#### Kernel Thread
- Every thread operation must go through kernel.
- Requires a fixed-size stack within kernel.

#### User Thread
- Implement as user-level library.
- Keep a queue of runnable threads.
- If operation would block, switch and run different thread.
- Switch to another thread on timer signals.
- Cannot take advantage of multiple CPUs or cores
- A page fault blocks all threads
