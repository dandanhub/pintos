## Source files
#### Kernel Loader
- 'loader.S', 'load.h'
  * The first part of Pintos that runs is the loader, in ‘threads/loader.S’. The PC BIOS loads the loader into memory. The loader, in turn, is responsible for initializing the CPU, loading the rest of Pintos into memory, and then jumping to its start.
- 'kernel.lds.S'
  * The linker script used to link the kernel. Sets the load address of the kernel and arranges for ‘start.S’ to be at the very beginning of the kernel image.
- 'start.S'
  * Jumps to main().

#### Initialization
- 'init.c', 'init.h'
  * Kernel initialization, including main(). The kernel proper starts with the main() function.
  * The first step is to initialize the kernel's BSS segment to all zeros.
  * Next, main() calls read_command_line() to break the kernel command line into arguments, then parse_options() to read any options at the beginning of the command line.
  * thread_init() initializes the thread system.
  * The final step is to initialize memory system.

#### Thread
- 'thread.c', 'thread.h'
  * Basic thread struct.

## Requirements
#### Alarm Clock
`void timer_sleep (int64_t ticks)`
- Reimplement without using busy waiting

#### Priority Scheduling
- Implement priority Scheduling
- Implement priority donation (for locks)
- Implement set/get priority functions
