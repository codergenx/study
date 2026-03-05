Lecture \# 7

By: Muhammad Zain Uddin

email: zuddin@iba.edu.pk

M. ZAIN UDDIN

1

Good Read

HTTPS://RESEARCH.SWTCH.COM/HWMM

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

2

Agenda

Locks continue

Open MP in detail

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

3

Attribution TODAY’S LECTURE IS BASED ON STANFORD’S 

COURSE ON PARALLEL COMPUTING AND 

HTTPS://RESEARCH.SWTCH.COM/HWMM

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

4

Litmus Test: Write Queue Can this program see r1 = 0, r2 = 0? 

// Thread 1 // Thread 2

x = 1 y = 1

r1 = y r2 = x On sequentially consistent hardware: no. 

On x86 \(or other TSO\): yes\! 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

5

Litmus Test: Independent Reads of Independent Writes \(IRIW\)

Can this program see r1 = 1, r2 = 0, r3 = 1, r4 = 0? 

\(Can Threads 3 and 4 see x and y change in different orders?\)

// Thread 1 // Thread 2 // Thread 3 // Thread 4

x = 1 

y = 1 r1 = x 

r3 = y

r2 = y r4 = x

On sequentially consistent hardware: no. 

On x86 \(or other TSO\): no. 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

6

Barrier

To fix algorithms that depend on stronger memory ordering, non-sequentially-consistent hardware supplies explicit instructions called memory barriers \(or fences\) that can be used to control the ordering. 

We can add a memory barrier to make sure that each thread flushes its previous write to memory before starting its read

// Thread 1 // Thread 2

x = 1 

y = 1

barrier 

barrier

r1 = y 

r2 = x

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

7

Preliminaries: some terminology

Deadlock

Livelock

Starvation

Deadlock and livelock concern program correctness. 

Starvation is really an issue of fairness. 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

8



Deadlock

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

9

Deadlock

Mutual exclusion: only one processor can hold a given resource at once Hold and wait: processor must hold the resource while waiting for other resources it needs to complete an operation No preemption: processors don’t give up resources until operation they wish to perform is complete Circular wait: waiting processors have mutual dependencies \(a cycle exists in the resource dependency graph\) PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

10



Starvation

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

11



Test and Set Based Lock

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

12



Test and Set Lock: Coherence Traffic

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

13



Test and Set Lock Performance PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

14

Desirable lock characteristics Low latency

Low interconnect traffic

Scalability

Low storage cost

Fairness

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

15

Test-and-test-and-set lock void Lock\(int\* lock\) \{

while \(1\) \{

while \(\*lock \!= 0\); // while another processor has the lock… 

// \(assume \*lock is NOT register allocated\) if \(test\_and\_set\(\*lock\) == 0\)

// when lock is released, try to acquire it return; 

\}

\}

void Unlock\(int\* lock\) \{

\*lock = 0; 

\}

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

16



Test and Test and Set: 

Coherence Traffic

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

17

Test-and-test-and-set characteristics

Slightly higher latency than test-and-set in no contention case Generates much less interconnect traffic More scalable

Storage cost unchanged

Still no provisions for fairness PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

18

Comparison **Lock Type**

**Mechanism**

**Performance**

High contention, 

Always writes 

**Test-and-Set \(TAS\)**

inefficient for many 

\(test\_and\_set in loop\)

threads

Reduces cache 

**Test-and-Test-and-Set **

Reads first \(if \(lock == 0\), contention, better **\(TTAS\)**

then test\_and\_set\)

performance

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

19



Ticket lock

No atomic operation needed to acquire the lock \(only a read\) Result: only one invalidation per lock release \(O\(P\) interconnect tra\!c\) PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

20



Example: Sorted Linked List PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

21



Example: simultaneous 

insertion

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

22



Example: simultaneous 

insertion/deletion

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

23

Question

HOW CAN YOU SOLVE THE ISSUE? 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

24



Solution: Protect list with a single lock

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

25

Question

WHAT ARE THE ISSUES AND WHAT ARE THE 

ADVANTAGES? 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

26

Question

CAN YOU DO BETTER? 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

27





Solution 2: “hand-over-hand” 

locking

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

28

Blocking algorithms/data structures

A blocking algorithm allows one thread to prevent other threads from completing operations on a shared data structure indefinitely Example:

◦ Thread 0 takes a lock on a node in our linked list

◦ Thread 0 is swapped out by the OS, or crashes, or is just really slow \(takes a page fault\), etc. 

◦ Now, no other threads can complete operations on the data structure \(although thread 0 is not actively making progress modifying it\) An algorithm that uses locks is blocking regardless of whether the lock implementation uses spinning or pre-emption PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

29



Lock Free Data Structures

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

30

Why is atomic\_min\(\) a Lock-Free Approach? 

A lock-free approach ensures that multiple threads can safely update a shared variable without using explicit locks \(e.g., mutexes, spinlocks, or semaphores\). Instead of blocking other threads while one thread updates a value, it relies on atomic operations, specifically Compare-And-Swap \(CAS\). 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

31

How Does It Avoid Locks? 

Instead of locking the variable before modification, it tries to update it optimistically using atomicCAS\(\). 

If another thread has modified the value in the meantime, the function simply retries \(while loop\), without blocking other threads. 

This makes it non-blocking, meaning no thread gets stuck waiting for another. 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

32

Role of Compare-And-Swap \(CAS\)

The atomicCAS\(\) function works as follows: Reads the current value at addr. 

If addr still contains old, it updates it to new atomically. 

Otherwise, it fails and returns the latest value, requiring the caller to retry

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

33

Why is This Lock-Free? 

No thread gets blocked: Unlike locks, if a thread fails to update addr, it retries immediately. 

Progress is guaranteed: At least one thread will always succeed in updating addr, ensuring forward progress. 

Avoids deadlocks and priority inversion: Since no explicit locking mechanism is used, threads don’t wait indefinitely. 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

34

**Approach** **Mechanism Blocking? **

**Fairness**

**Performance**

**Scalability**

**Use Case**

Atomic 

**Test-and-Set \(TAS\) **

High contention, CPU 

Short critical 

test\_and\_set, 

Yes \(Spins\)

No

Poor

**Lock**

overhead

sections

spinlocks

**Test-and-Test-and-**

Checks before 

Reduces cache 

Slightly improved 

Yes \(Spins\)

No

Moderate

**Set \(TTAS\) Lock**

atomic set

contention

spinlock

**Handoff Lock \(MCS, **

Queue-based 

Reduces contention, 

Many threads, 

Yes

Yes

Good

**Ticket Lock\)**

handover

avoids spinning

fairness required

Avoids CPU waste but 

When fairness & 

**Mutex \(Blocking **

OS-managed 

Yes \(Threads sleep\)

Yes

adds context switch 

Good

low CPU usage 

**Lock\)**

blocking

overhead

matter

Managing access 

Counter-based, 

Moderate overhead 

to a limited 

**Semaphore**

allows multiple 

Yes \(if using wait\)

Yes

due to kernel 

Good

resource \(e.g., 

accesses

interaction

database 

connections\)

High-

Uses atomic 

No \(depends 

**Lock-Free **

Very fast, avoids 

performance, 

compare-and-

No

on 

Excellent

**\(CAS-based\)**

context switching

concurrent 

swap \(CAS\)

algorithm\)

data structures

35



