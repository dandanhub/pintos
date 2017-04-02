# Processes

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

### User View of Processes
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

### Kernel View of Processes
#### PCB
