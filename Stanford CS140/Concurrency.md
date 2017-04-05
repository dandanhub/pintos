# Concurrency and Process Scheduling

### Thread
1. Can have non-preemptive threads: one thread executes exclusively until it makes a blocking call.
2. Preemptive threads: may switch to another thread between any two instructions.
3. Using multiple CPUs is inherently preemptive

### Sequential Consistency
The result of execution is as if all operations were executed in some sequential order, and the operations of each processor occurred in the order specified by the program.
1. maintain program order on individual processors
2. ensure write atomicity

### Process Scheduling
1. FCFS: keep CPU until thread blocks.
  - Simple
  - Short jobs get stuck begind long ones
2. RR: each process gets a small unit of CPU time quantum, after quantum expires, the process is preempted and moved to the end of the ready queue.
  - Better/fair for short job
  - Context-switching time adds up for long jobs
  - Time quantum too big, response time suffers
  - Time quantum too small, throughput suppers, the overhead for context switch is high
3. Non-preemptive SJF： Shortest Job First, run whatever job has the least amount of computation to do.
4. Preemptive SRTF: Shortest Remaining Time First, if job arrives and has a shorter time to completion than the remaining time on the current job, immediately preempt CPU.
  - SRTF can lead to starvation if many small jobs as large jobs never get to run.
  - Hard to predict the future, unfair.
5. Multi-level feedback queue: multiple queues with different priority, each queue has its own scheduling algorithm
  - Ask the user
    - when you submit a job, have to say how long it will take
    - to stop cheating, system kills job if takes too long
    - even non-malicious users have trouble predicting runtime of their jobs
  - Adapting SRTF
    - use SRTF as a yardstick for measuring other policies
    - predicting the length of next CPU burst
  - Adjust each job's priority as follows:
    - Job starts in highest priority queue
    - If timeout expires, drop one level
    - If timeout doesn't expire, push up one level (or to top)
