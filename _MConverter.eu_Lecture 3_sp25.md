Lecture \# 3

Multithreading /Cache coherence/Protocol/Synchronization By: Muhammad Zain Uddin

email: zuddin@iba.edu.pk

M. ZAIN UDDIN

1





Multithreading

for \(int i = 0; i < num\_threads; \+\+i\) \{

thread\_data\[i\].start = i \* \(len / num\_threads\); 

\#include <stdio.h> 

thread\_data\[i\].end = \(i == num\_threads - 1\) ? len : \(i \+ 1\) \* \(len / num\_threads\); 

\#include <pthread.h> 

thread\_data\[i\].data = data; 

\#include <stdlib.h> 

thread\_data\[i\].partial\_sum = NULL; 

typedef struct \{

pthread\_create\(&threads\[i\], NULL, worker, &thread\_data\[i\]\); int start; 

\}

int end; 

int\* data; 

int\* partial\_sum; 

int total\_sum = 0; 

\} thread\_data\_t; 

for \(int i = 0; i < num\_threads; \+\+i\) \{

void\* result; 

void\* worker\(void\* arg\) \{

pthread\_join\(threads\[i\], &result\); 

thread\_data\_t\* data = \(thread\_data\_t\*\)arg; total\_sum \+= \*\(int\*\)result; 

int sum = 0; 

free\(result\); 

for \(int i = data->start; i < data->end; \+\+i\) \{

\}

sum \+= data->data\[i\] \* data->data\[i\]; 

\}

int\* result = \(int\*\)malloc\(sizeof\(int\)\); return total\_sum; 

\*result = sum; 

\}

return result; 

\}

int main\(\) \{

int sum\_of\_squares\_multithread\(int data\[\], int len, int num\_threads\) int data\[\] = \{2, 5, 7, 4\}; 

\{

int sum = sum\_of\_squares\_multithread\(data, 4, 2\); pthread\_t threads\[num\_threads\]; 

printf\("Sum of squares: %d\\n", sum\); thread\_data\_t thread\_data\[num\_threads\]; 

return 0; 

\}

M. ZAIN UDDIN

2



**Headers:**

stdio.h: Provides functions for input/output operations like printing to the console. 

pthread.h: Contains functions and types for working with threads, enabling multithreading. 

stdlib.h: Offers general utility functions, including memory allocation and deallocation. 

**Structure:**

thread\_data\_t: A structure for packaging information to be passed to worker threads: Start: The starting index of the data segment assigned to the thread. 

end: The ending index of the data segment. 

data: A pointer to the shared array containing the data to be processed. 

**Worker Function:**

worker:

Takes a thread\_data\_t pointer as input, providing thread-specific data. 

Calculates the sum of squares within its assigned data segment. 

Dynamically allocates memory using malloc to store the calculated partial sum. 

Stores the partial sum in the allocated memory location. 

Returns a pointer to the newly allocated memory containing the partial sum. 

M. ZAIN UDDIN

3



**Sum of Squares Function:**

sum\_of\_squares\_multithread:

Accepts the data array, its length, and the desired number of threads as input. 

Creates an array of threads and thread\_data\_t structures to organize thread-related information. 

Divide the data array into chunks and assign them to different threads for parallel processing. 

Initializes a variable total\_sum to 0, which will accumulate the final result. 

Creates the threads using pthread\_create, each executing the worker function with its corresponding thread\_data\_t. 

Waits for all threads to finish using pthread\_join, collecting their partial sums. 

Iterates through the returned partial sums, adding them to total\_sum. 

Frees the memory allocated for partial sums using free to prevent memory leaks. 

Returns the calculated total\_sum, representing the sum of squares of all elements in the array. 

**Main Function:**

main:

Creates a sample data array to be processed. 

Calls the sum\_of\_squares\_multithread function to perform the multithreaded calculation. 

Prints the final sum of squares obtained from the multithreaded operation. 

Returns 0 to indicate successful 

M. ZAIN UDDIN

4



Caching with multithreading

●

Each core has its own L1 cache, and sometimes its own L2 cache

●

Most caches are write-back, so it doesn't update main memory until the block gets evicted

●

Problem for multithreaded code: If multiple threads are running with shared memory, how do we guarantee that the correct version of data is being used? 

○

Can't access main memory anymore, if another cache has dirty data 6

Caching Example: Multithreaded Interleaved Writes

●

Imagine we run Matrix Multiply on 2 threads with interleaved writes

●

The below shows one block in the L1 caches of each thread, and the right Bt

17

21

25

29

shows the state of the main memory

18

22

26

30

Threa V

Dirty

Data

19

23

27

31

d

**0**

**0**

**0**

**0x14 0xFD 0xBE **

20

24

28

32

**0x5E**

A

C

1

2

3

4

Threa V

Dirty

Data

5

6

7

8

7

d

9

10

11

12

**1**

**0**

**0**

**0xB5 0x81 0x67 **

13

14

15

16

**0x3F**

Caching Example: Multithreaded Interleaved Writes

●

Thread 0 computes C\[0\]

○

Since the cache is write-back, we don't write back to main memory immediately

Bt

17

21

25

29

○

For spatial locality, we copy the full block to the cache 18

22

26

30

Thread V

Dirty

Data

19

23

27

31

**0**

**1**

**1**

**0xFA 0x?? 0x?? **

20

24

28

32

**0x?? **

A

C

1

2

3

4

Thread V

Dirty

Data

5

6

78

8

9

10

11

12

**1**

**0**

**0**

**0xB5 0x81 0x67 **

**0x3F**

13

14

15

16

Caching Example: Multithreaded Interleaved Writes

●

Thread 1 computes C\[1\]

Bt

17

21

25

29

○

Main memory hasn't updated, so the cache block thread 1 gets doesn't have C\[0\] 

computed

18

22

26

30

Thread

V

Dirty

Data

19

23

27

31

20

24

28

32

**0**

**1**

**1**

**0xFA 0x?? 0x?? **

**0x?? **

A

C

1

2

3

4

5

6

7

8

Thread

V

Dirty

Data

9

10

11

12

**1**

**1**

**1**

**0x?? 0x04 0x?? **

13

14

15

16

**0x?? **

9

Caching Example: Multithreaded Interleaved Writes

●

Thread 0 computes C\[2\]

●

Thread 1 computes C\[3\]

Bt

17

21

25

29

Thread

V

Dirty

Data

18

22

26

30

19

23

27

31

**0**

**1**

**1**

**0xFA 0x?? 0x0E **

**0x?? **

20

24

28

32

A

C

1

2

3

4

Thread

V

Dirty

Data

10

5

6

7

8

9

10

11

12

**1**

**1**

**1**

**0x?? 0x04 0x?? **

13

14

15

16

**0x18**

Caching Example: Multithreaded Interleaved Writes

●

Thread 0 evicts the C\[0\] block

Bt

17

21

25

29

Threa V

Dirty

Data

18

22

26

30

d

19

23

27

31

**0**

**0**

**0**

**0xFA 0x?? 0x0E **

20

24

28

32

**0x?? **

A

C

1

2

3

4

FA

?? 

0E

?? 

Threa V

Dirty

Data

5

6

7

11 8

d

9

10

11

12

**1**

**1**

**1**

**0x?? 0x04 0x?? **

13

14

15

16

**0x18**

Caching Example: Multithreaded Interleaved Writes

●

Thread 1 evicts the C\[0\] block

○

Overwrites the data from Thread 0\! 

Bt

17

21

25

29

Threa V

Dirty

Data

18

22

26

30

d

19

23

27

31

**0**

**0**

**0**

**0xFA 0x?? 0x0E **

**0x?? **

20

24

28

32

A

C

1

2

3

4

?? 

04

?? 

18

Threa V

Dirty

Data

12

5

6

7

8

d

9

10

11

12

**1**

**0**

**0**

**0x?? 0x04 0x?? **

**0x18**

13

14

15

16

Caching with multithreading

●

Each core has its own L1 cache, and sometimes its own L2 cache

●

Most caches are write-back, so it doesn't update main memory until the block gets evicted

●

Problem for multithreaded code: If multiple threads are running with shared memory, how do we guarantee that the correct version of data is being used? 

○

Can't access main memory anymore, if another cache has dirty data

●

Three main cases

○

Two threads read

○

Two threads write

○

One thread reads, one thread writes

13

Caching with multithreading

●

Synchronous reads:

○

Should be allowed; as long as no one changes data, things are safe

●

Synchronous writes:

○

Once two different threads have conflicting data, it's difficult to return to a reasonable state

○

Example: git merge conflicts

○

Therefore, we should not allow these to happen

○

If threads attempt to cause this, we need to force a thread to evict

○

These evictions cause **coherence misses**; in a multithreaded system with shared memory, coherence misses can cause significant thrashing

●

Multiple threads read, one writes

○

Could go the safe route and force evictions

■

But causes coherence misses

○

Ideally: Allow threads to read the written data from another core's cache, or set 14 up a way for one cache to 

update other caches

■

Needs some kind of communication protocol

**Introduction to Cache Coherence**

•**Definition:**

• Cache coherence refers to the consistency of shared data in multiple caches that store copies of the same data. 

•**Importance:**

• Ensures that all processors in a multiprocessor system observe a consistent view of memory. 

M. ZAIN UDDIN

15



Coherence Definition

A memory system is coherent if:

The results of a parallel program’s execution are such that for each memory location, there is a hypothetical serial order of all program operations \(executed by all processors\) to the location that is consistent with the results of execution, and:

◦ Memory operations issued by any one processor occur in the order issued by the processor

◦ The value returned by a read is the value written by the last write to the location… as given by the serial order PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

16

MOESI

●

Solution: Set up a system where you can "snoop" on other caches to see if they have a cache block with the same tag

●

Instead of just having a valid and dirty bit, have five different states for a block

○

Modified

○

Owned

○

Exclusive

○

Shared

○

Invalid

●

Invalid: Same as valid bit off in regular cache; the block isn't in the cache

●

Exclusive: Same as valid bit on, dirty bit off in regular cache

○

The block has been read, but not modified

○

Further, no other cache has this block

17

●

Modified: Same as valid bit on, dirty bit on in regular cache

○

The block has been read, and modified

○

Further, no other cache has this block

MOESI

●

Shared

○

The block is in some other cache

○

We haven't modified this block, and we're not allowed to make modifications

■

If we need to make modifications, evict the block from everyone's cache and move to modified

○

Allows for synchronous reads with at most one writer

●

Owner

○

The block is in some other cache

○

We have modified the block, and are the only thread allowed to modify it

○

If we make modifications, it's our responsibility to tell all the other caches in shared state about these changes

○

Allows for writing while other threads read the same data 18



Cache Coherence Invariants

For any memory address x, at any given time period \(epoch\): Single-Writer, Multiple-Read \(SWMR\) Invariant Read-write epoch: there exists only a single processor that may write to x \(and can also read it\)

Read-Only- epoch: some number of processors that may only read x Data-Value Invariant \(write serialization\) The value of the memory address at the start of an epoch is the same as the value of the memory location at the end of its last read-write epoch PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

19

Question

WHAT ABOUT SHARED CACHE? 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

20

Shared caches

One single cache shared by all processors

◦ Eliminates problem of replicating state in multiple caches Obvious scalability problems \(since the point of a cache is to be local and fast\) 

◦ Interference \(conflict misses\) / contention due to many clients\(destructive\) But shared caches can have benefits: 

◦ Facilitates fine-grained sharing \(overlapping working sets\)

◦ Loads/stores by one processor might pre-fetch lines for another processor \(constructive\) PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

21



Shared Cache

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

22

Snooping cache-coherence schemes Main idea: all coherence-related activity is broadcast to all processors in the system \(more specifically: to the processor’s cache controllers\) Cache controllers monitor \(“they snoop”\) memory operations, and follow **cache coherence** **protocol **to maintain memory coherence PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

23



Snooping cache-coherence

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

24



Simple coherence implementation

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

25

Question

DO YOU SEE ANY PROBLEM? 

\(HINT: MAIN MEMORY\)

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

26

Write through policy inefficiency Every write operation goes out to memory

◦ Very high bandwidth requirements 

Write-back caches absorb most write traffic as cache hits 

◦ Significantly reduces bandwidth requirements

◦ But now how do we maintain cache coherence invariants? 

◦ This requires more sophisticated coherence protocols PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

27



Cache coherence with write back cache

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

28

Cache Coherence Protocol Algorithm that maintains cache coherent invariants The logic we are about to describe is performed by each processor’s cache controller in response to: 

◦ Loads and stores by the local processor

◦ Messages from other caches on the bus 

If all cache controllers operate according to this described protocol, then coherence will be maintained

◦ The caches “cooperate” to ensure coherence is maintained PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

29

Invalidation based write back protocol Key ideas: A line in the “modified” state can be modified without notifying the other caches Processor can only write to lines in the modified state 

◦ Need a way to tell other caches that processor wants exclusive access to the line 

◦ We accomplish this by sending message to all the other caches When cache controller sees a request for modified access to a line it contains 

◦ It must **invalidate **the line in its cache PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

30

MSI write-back invalidation protocol Key tasks of protocol 

◦ Ensuring processor obtains exclusive access for a write

◦ Locating most recent copy of cache line’s data on cache miss Three cache line states

◦ Invalid \(I\): same as meaning of invalid in uniprocessor cache

◦ Shared \(S\): line valid in one or more caches, memory is up to date 

◦ Modified \(M\): line valid in exactly one cache \(a.k.a. “dirty” or “exclusive” state\) PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

31

MSI write-back invalidation protocol Two processor operations \(triggered by local CPU\) PrRd \(read\)

PrWr \(write\) 

Three coherence-related bus transactions \(from remote caches\) BusRd: obtain copy of line with no intent to modify BusRdX: obtain copy of line with intent to modify BusWB: write dirty line out to memory

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

32



MSI Invalidation Protocol State Diagram

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

33

MSI Invalidation Protocol Read obtains block in “shared” 

even if only cached copy 

Obtain exclusive ownership before writing BusRdX causes others to invalidate 

If M in another cache, will cause writeback BusRdX even if hit in S - promote to M \(upgrade\) PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

34



Example

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

35



