# Introduction to OS

### What is OS?
A layer between applications and hardware

### Primitive OS
#### Multitasking
More than one process can be running at once.
When one process blocks because of waiting for disk, network, user input and etc., run another process. OS provides:
1. take CPU away from looping process
2. protect process's memory from another

#### Multi-user OSes
With N users, system not N timer slower. OS provides protection to server distrustful users or applications.
1. pre-allocate resource for applications
2. mediation between applications
3. protection operations in OS privileged kernel mode

### Typical OS Structure

#### System Calls
Most applications run in user mode while OS runs in privileged kernel mode.
Applications can invoke kernel through system calls.

Higher user-level functions built on syscall interfaces:
- printf
- scanf
- fgets

Some syscall examples - UNIX file syscall
1. `int open(char *path, int flags, /*int mode*/...)`

  Returns file descriptor number - used for all I/O to file.
  Returns -1 if open fails.

2. `int read (int fd, void *buf, int nbytes)`

3. `int write (int fd, const void *buf, int nbytes)`

4. `off_t lseek (int fd, off_t pos, int whence)`

#### CPU Preemption
Protection to prevent monopolizing CPU, like kernel timer to interrupt every 10 ms.

However, the protection is not secure. We can monopolize CPU using multiple processes or using all memory.

#### Memory Protection
Protect memory of one program from actions of others.

Do address translation between virtual address and physical address.
- Address space: all memory locations of a program
- Virtual address: addresses in a process's address space
- Physical address: address of real memory
- Translation: map virtual to physical address

#### Resource Allocation
Multitasking permits higher resource utilization.
