# Synchronization

### Race Condition Problem
Critical section is piece of code that only one thread can execute at once. A solution to the critical-section problem must satisfy the following three requirements:
1. Mutual Exclusion: If process pi is executing in its critical section, then no other processes can be executing in their critical sections.
2. Progress: If no process is executing in its critical section and some processes wish to enter their critical sections, then only those processes that are not executing in their remainder sections can participate in deciding which will enter its critical section next, and this selection cannot be postponed indefinitely.
3. Bounded waiting: There exists a bound, or limit, on the number of times that other processes are allowed to enter their critical sections after a ￼process has made a request to enter its critical section and before that request is granted.

1st A naiive solution: Context switch after the testing and before the locking. Hard to debug.
~~~~
if (!lock) {
  lock = true;
  // critical section
  lock = false;
}
~~~~

2nd try: Context switch after the locking and before the testing. Hard to debug.
~~~~
lockA = true;
if (!lockB) {
  // critical section
}
lockA = false;

lockB = true;
if (!lockA) {
  // critical section
}
lockB = false;
~~~~

3rd try: at X: if B is not locked, enter CS; otherwise wait; at Y: if A is not locked, enter CS; otherwise leave. It works, but the it is not symmetric.
~~~~
lockA = true;
while (lockB); //X
// critical section
lockA = false;

lockB = true;
if (!lockA) { //Y
  // critical section
}
lockB = false
~~~~

Peterson's algorithm: Peterson’s solution requires the two processes to share two data items:
~~~~
int turn;
boolean lock[2];
~~~~
The variable turn indicates whose turn it is to enter its critical section. The lock array is used to indicate if a process is ready to enter its critical section.

~~~~
while (true) {
  lock[i] = true;
  turn = j;
  while (lock[j] && turn == j);
  //critical section
  lock[i] = false;
  // remainder section
}
~~~~

### Hardware solution
#### Disable Interrupts
The critical-section problem could be solved simply in a single-processor environment if we could prevent interrupts from occurring while a shared variable was being modified.

Unfortunately, this solution is not as feasible in a multiprocessor environment. Disabling interrupts on a multiprocessor can be time consuming, since the message is passed to all the processors. This message passing delays entry into each critical section, and system efficiency decreases.

Many modern computer systems therefore provide special hardware instructions that allow us either to test and modify the content of a word or to swap the contents of two words atomically — that is, as one uninterruptible unit. We can use these special instructions to solve the critical-section problem in a relatively simple manner. The main concepts could be abstracted to the test_and_set() and compare_and_swap() instructions.

1. test_and_set()
2. compare_and_swap()

The two instructions can executed atomically.

Busy waiting - thread consumes cycles while waiting:
while (TestAndSet (&lock));
while (key == true) Swap (&lock, &key);
- Pros: Machine can receive interrupts
- Pros: User code can use this lock
- Pros: Works on a multiprocessor
- Cons: This is very inefficient because the busy-waiting thread will consume cycles waiting
- Cons: Priority inversion, if busy-waiting thread has higher priority than thread holding lock, no progress!

## Lock solution
The hardware-based solutions to the critical-section problem are complicated as well as generally inaccessible to application programmers. Instead, operating-systems designers build software tools to solve the critical-section problem. The simplest of these tools is the mutex (mutual exclusive) lock.
