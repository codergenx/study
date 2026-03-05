Lecture \# 4

Latency/multithread/Concurrency 

By: Muhammad Zain Uddin

email: zuddin@iba.edu.pk

M. ZAIN UDDIN

1





M. ZAIN UDDIN

2



MSI Invalidation Protocol State Diagram

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

3

MSI Invalidation Protocol

Read obtains block in “shared” 

even if only cached copy 

Obtain exclusive ownership before writing 

BusRdX causes others to invalidate 

If M in another cache, will cause writeback

BusRdX even if hit in S - promote to M \(upgrade\)

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

4



Example

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

5

How Does MSI Satisfy Cache Coherence Invariants? 

Single-Writer, Multiple-Read \(SWMR\) Invariant

Only one cache can be in M-state all others get invalidation message Multiple caches can be in read-only S-state

Data-Value Invariant \(write serialization\)

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

6

Summary MSI

A line in the M state can be modified without notifying other caches 

◦ No other caches have the line resident, so other processors cannot read these values 

◦ \(without generating a memory read transaction\)

Processor can only write to lines in the M state 

◦ If processor performs a write to a line that is not exclusive in cache, cache controller must first broadcast a read-exclusive transaction to move the line into that state

◦ Read-exclusive tells other caches about impending write

◦ Read-exclusive transaction is required even if line is valid \(but not exclusive… it’s in the S state\) in processor’s local cache

◦ Dirty state implies exclusive

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

7

Summary MSI

When cache controller snoops a “read exclusive” for a line it contains

◦ Must invalidate the line in its cache

◦ Because if it didn’t, then multiple caches will have the line \(and so it wouldn’t be exclusive in the other cache\!\)

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

8

MESI invalidation protocol

MSI requires two interconnect transactions for the common case of reading an address, then writing to it

◦ Transaction 1: BusRd to move from I to S state

◦ Transaction 2: BusRdX to move from S to M state

This inefficiency exists even if application has no sharing at all PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

9

Question

WHAT CAN BE DONE AVOID THIS INEFFICIENCY? 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

10



MESI invalidation protocol

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

11

MESI invalidation protocol

Solution: add additional state E \(“exclusive clean”\) Line has not been modified, but only this cache has a copy of the line Decouples exclusivity from line ownership \(line not dirty, so copy in memory is valid copy of data\)

Upgrade from E to M does not require a bus transaction PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

12



Directory coherence in Intel Core i7 CPU

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

13

Question

WHAT ARE THE IMPLICATIONS OF CACHE COHERENCE TO THE 

PROGRAMMER? 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

14



Communication Overhead

Communication time is a key parallel overhead

Appears as increased memory access time in multiprocessor

◦ Extra main memory accesses in UMA systems

◦ Must determine increase in cache miss rate vs. uniprocessor

◦ Some accesses have higher latency in NUMA systems

◦ Only a fraction of a % of these can be significant\! 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

15



Unintended communication via false 

sharing

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

16



Demo: false sharing

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

17

False sharing

Condition where two processors write to different addresses, but addresses map to the same cache line 

Cache line “ping-pongs” between caches of writing processors, generating significant amounts of communication due to the coherence protocol 

No inherent communication, this is entirely artifactual communication \(cache lines > 4B\) False sharing can be a factor in when programming for cache coherent architectures PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

18



Impact of cache line size on miss rate

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

19



Memory coherence vs. memory 

consistency

**Memory coherence **defines requirements for the observed behavior of reads and writes to the same memory location 

◦ All processors must agree on the order of reads/writes to X

◦ In other words: it is possible to put all operations involving X on a timeline such that the observations of all processors are consistent with that timeline 

**Memory consistency **defines the behavior of reads and writes to different locations \(as observed by other processors\)

◦ Coherence only guarantees that writes to address X will eventually propagate to other processors

◦ Consistency deals with when writes to X propagate to other processors, relative to reads and writes to other addresses PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

20

Memory coherence vs. memory 

consistency

The goal of cache coherence is to ensure that the memory system in a parallel computer behaves as if the caches were not there

◦ Just like how the memory system in a uniprocessor system behaves as if the cache was not there 

◦ A system without caches would have no need for cache coherence Memory consistency defines the allowed behavior of loads and stores to different addresses in a parallel system

◦ The allowed behavior of memory should be specified whether or not caches are present \(and that’s what a memory consistency model does\)

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

21

Memory operation ordering

A program defines a sequence of loads and stores \(this is the “program order” of the loads and stores\)

Four types of memory operation orderings 

WX→RY: write to X must commit before subsequent read from Y \*

RX →RY : read from X must commit before following read from Y

RX →WY : read to X must commit before subsequent write to Y 

WX →WY : write to X must commit before subsequent write to Y

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

22

Multiprocessor Execution

Initially A = B = 0

Proc 0

Proc 1

\(1\) A = 1 \(3\) B = 1

\(2\) print B

\(4\) print A

What can be printed? 

“01”? 

“10”? 

“11”? 

“00”? 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

23

Orderings That Should Not Happen

The program should not print “00” or “10” 

A “happens-before” graph shows the order in which events must execute to get a desired outcome

If there’s a cycle in the graph, an outcome is impossible—an event must happen before itself\! 

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

24

Sequential Consistency

All operations executed in some sequential order 

◦ As if they were manipulating a single shared memory Each thread’s operations happen in program order

A sequentially consistent memory system maintains all four memory operation orderings PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

25



Sequential consistency \(switch 

metaphor\)

All processors issue loads and stores in program order Memory chooses a processor at random, performs a memory operation to completion, then chooses another processor, …

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

26



Relaxed Sequential Consistency

Relaxed memory consistency models allow certain orderings to be violated Motivation for relaxed consistency: hiding latency

◦ To gain performance

◦ Overlap memory access operations with other operations when they are independent

◦ Memory access in a cache coherent system is not just reading/writing data PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

27



Problem with Sequential Consistency

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

28



Optimization: Write Buffer

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

29



Write Buffer Performance

Base: Sequentially consistent execution. Processor issues one memory operation at a time, stalls until completion 

W-R: relaxed W→R ordering constraint \(write latency almost fully hidden\) PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

30



Write Buffers Change Memory Behavior

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

31

Allowing reads to move ahead of writes Four types of memory operation orderings

- WX→RY: write must complete before subsequent read

- RX→RY : read must complete before subsequent read

- RX →WY : read must complete before subsequent write

- WX →WY : write must complete before subsequent write Processor P can read B before its write to A is seen by all processors \(processor can move its own reads in front of its own writes\)

Can be achieved using either:

Total store ordering \(TSO\)

Processor consistency \(PC\)

PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

32

Allowing reads to move ahead of writes Total store ordering \(TSO\)

Reads by other processors cannot return new value of A until the write to A is observed by all processors

Processor consistency \(PC\)

Any processor can read new value of A before the write is observed by all processors In TSO and PC, only WX →RY order is relaxed. The WX →WY constraint still exists. Writes by the same thread are not reordered \(they occur in program order\) PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

33

Clarification

The cache coherency problem exists because hardware implements the optimization of duplicating data in multiple processor caches. The copies of the data must be kept coherent. 

Relaxed memory consistency issues arise from the optimization of reordering memory operations. \(Consistency is unrelated to whether or not caches exist in the system\) PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

34



Allowing writes to be reordered

Four types of memory operation orderings

- WX→RY: write must complete before subsequent read

- RX→RY : read must complete before subsequent read

- RX →WY : read must complete before subsequent write

- WX →WY : write must complete before subsequent write Partial Store Ordering \(PSO\) - Execution may not match sequential consistency

◦ \(P2 may observe change to flag before change to A\) PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

35

Why might it be useful to allow more aggressive memory operation reorderings? 

WX→WY: processor might reorder write operations in a write buffer \(e.g., one is a cache miss while the other is a hit\) 

RX→WY, RX→RY: processor might reorder independent instructions in an instruction stream \(out-of-order execution\) 

Keep in mind these are all valid optimizations if a program consists of a single instruction stream PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

36

Allowing all reorderings

Four types of memory operation orderings

- WX→RY: write must complete before subsequent read

- RX→RY : read must complete before subsequent read

- RX →WY : read must complete before subsequent write

- WX →WY : write must complete before subsequent write No guarantees about operations on data\! 

◦ Everything can be reordered

Motivation is increased performance

◦ Overlap multiple reads and writes in the memory system

◦ Execute reads as early as possible and writes as late as possible to hide memory latency PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

37

Synchronization to the Rescue 

Memory reordering seems like a nightmare \(it is\!\)

Every architecture provides synchronization primitives to make memory ordering stricter Fence \(memory barrier\) instructions prevent reorderings, but are expensive 

◦ All memory operations complete before any memory operation after it can begin PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

38

Problem: Data Races 

Every example so far has involved a data race

Two accesses to the same memory location

At least one is a write

Unordered by synchronization operations

Two memory accesses by different processors conflict if…

◦ They access the same memory location

◦ At least one is a write 

If conflicting accesses are not ordered by synchronization can contain data races:

◦ the output of the program depends on relative speed of processors PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

39

Synchronized Programs

Synchronized programs yield SC results on non-SC systems

◦ Synchronized programs are data-race-free 

If there are no data races, reordering behavior doesn’t matter 

◦ Accesses are ordered by synchronization, and synchronization forces sequential consistency In practice, most programs you encounter will be synchronized PARALLEL AND DISTRIBUTED COMPUTING – SPRING 2025

40





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

thread\_data\_t\* data = \(thread\_data\_t\*\)arg; 

total\_sum \+= \*\(int\*\)result; 

int sum = 0; 

free\(result\); 

for \(int i = data->start; i < data->end; \+\+i\) \{

\}

sum \+= data->data\[i\] \* data->data\[i\]; 

\}

int\* result = \(int\*\)malloc\(sizeof\(int\)\); 

return total\_sum; 

\*result = sum; 

\}

return result; 

\}

int main\(\) \{

int sum\_of\_squares\_multithread\(int data\[\], int len, int num\_threads\) int data\[\] = \{2, 5, 7, 4\}; 

\{

int sum = sum\_of\_squares\_multithread\(data, 4, 2\); 

pthread\_t threads\[num\_threads\]; 

printf\("Sum of squares: %d\\n", sum\); 

thread\_data\_t thread\_data\[num\_threads\]; 

return 0; 

\}

M. ZAIN UDDIN

41





Multithreading\(2\)

\#include <stdio.h> 

for \(int i = 0; i < num\_threads; \+\+i\) \{

\#include <pthread.h> 

thread\_data\[i\].start = i \* \(len / num\_threads\); 

thread\_data\[i\].end = \(i == num\_threads - 1\) ? len : \(i \+ 1\) \* \(len / num\_threads\); typedef struct \{

int start; 

thread\_data\[i\].data = data; 

int end; 

thread\_data\[i\].partial\_sum = NULL; // Not used in this version int\* data; 

pthread\_create\(&threads\[i\], NULL, worker, &thread\_data\[i\]\); int\* partial\_sum; 

\}

\} thread\_data\_t; 

pthread\_mutex\_init\(&mutex, NULL\); // Initialize mutex int total\_sum = 0; 

pthread\_mutex\_t mutex; 

for \(int i = 0; i < num\_threads; \+\+i\) \{

pthread\_join\(threads\[i\], NULL\); // Wait for threads to finish void\* worker\(void\* arg\) \{

thread\_data\_t\* data = \(thread\_data\_t\*\)arg; 

\}

int partial\_sum = 0; 

for \(int i = data->start; i < data->end; \+\+i\) \{

pthread\_mutex\_destroy\(&mutex\); // Clean up mutex partial\_sum \+= data->data\[i\] \* data->data\[i\]; 

\}

return total\_sum; 

\}

pthread\_mutex\_lock\(&mutex\); // Protect shared variable access total\_sum \+= partial\_sum; 

int main\(\) \{

pthread\_mutex\_unlock\(&mutex\); 

int data\[\] = \{2, 5, 7, 4\}; 

return NULL; 

int sum = sum\_of\_squares\_multithread\(data, 4, 2\); 

\}

printf\("Sum of squares: %d\\n", sum\); 

int sum\_of\_squares\_multithread\(int data\[\], int len, int num\_threads\) 

\{

return 0; 

pthread\_t threads\[num\_threads\]; 

\}

thread\_data\_t thread\_data\[num\_threads\]; 

M. ZAIN UDDIN

42





int sum\_of\_squares\_multithread\(int data\[\], int len, int num\_threads\) \{

pthread\_t threads\[num\_threads\]; 

Multithreading\(3\)

thread\_data\_t thread\_data\[num\_threads\]; 

int total\_sum = 0; 

g\+\+ -o myprogram TH\_EXAMP3.C -pthread -lstdc\+\+

int chunk\_size = len / num\_threads; 

for \(int i = 0; i < num\_threads; \+\+i\) \{

\#include <stdio.h> 

thread\_data\[i\].start = i \* chunk\_size; 

\#include <pthread.h> 

thread\_data\[i\].end = \(i == num\_threads - 1\) ? len : \(i \+ 1\) \* chunk\_size; 

\#include <time.h> 

thread\_data\[i\].data = data; 

\#include <mutex> 

thread\_data\[i\].partial\_sum = new int\(0\); // Separate partial sum for each thread pthread\_create\(&threads\[i\], NULL, worker, &thread\_data\[i\]\); typedef struct \{

\}

int start; 

for \(int i = 0; i < num\_threads; \+\+i\) \{

int end; 

pthread\_join\(threads\[i\], NULL\); 

int\* data; 

std::lock\_guard<std::mutex> lock\(mtx\); 

int\* partial\_sum; 

total\_sum \+= \*\(thread\_data\[i\].partial\_sum\); // Aggregate partial sums safely

\} thread\_data\_t; 

delete thread\_data\[i\].partial\_sum; 

\}

std::mutex mtx; // Global mutex for synchronization return total\_sum; 

\}

void\* worker\(void\* arg\) \{

int main\(\) \{

thread\_data\_t\* data = \(thread\_data\_t\*\)arg; 

int data\[\] = \{2, 5, 7, 4\}; 

int sum = 0; 

for \(int i = data->start; i < data->end; \+\+i\) \{

clock\_t start\_time = clock\(\); 

sum \+= data->data\[i\] \* data->data\[i\]; 

int sum = sum\_of\_squares\_multithread\(data, 4, 2\); 

\}

clock\_t end\_time = clock\(\); 

std::lock\_guard<std::mutex> lock\(mtx\); // Acquire mutex printf\("Sum of squares: %d\\n", sum\); 

before updating partial sum

printf\("Execution Time: %f seconds\\n", \(\(double\)\(end\_time - start\_time\)\) / 

\*\(data->partial\_sum\) \+= sum; 

CLOCKS\_PER\_SEC\); 

return NULL; 

return 0; 

\}

\}

M. ZAIN UDDIN

43

Difference of three code

**Functionality:**

All three codes calculate the sum of squares of elements in an array using multiple threads. 

**Structure:**

Code 1: Simplest structure, but requires dynamic memory allocation for partial\_sum in each thread. 

Code 2: Global mutex for synchronization, potentially introduces contention. 

Code 3: Separate partial\_sum for each thread, reducing mutex usage and contention. 

**Synchronization:**

Code 1: Lacks synchronization on total\_sum, leading to potential race conditions and incorrect results. 

Code 2: Uses a global mutex to protect total\_sum, avoids race conditions. 

Code 3: Minimal mutex usage, only acquires lock when aggregating partial sums. 

**Performance:**

Code 1: Potentially faster due to lack of synchronization, but unreliable. 

Code 2: May suffer from mutex contention, impacting performance with many threads. 

Code 3: Generally better performance and scalability due to reduced contention. 

M. ZAIN UDDIN

44

Difference of three codes \(con.t\)

**Memory Usage:**

Code 1: Requires dynamic memory allocation for partial\_sum in each thread, potentially impacting memory overhead. 

Code 2: No additional memory usage beyond data and thread structures. 

Code 3: Similar to Code 2, but adds the cost of separate partial\_sum variables. 

**Recommendation:**

Code 3: Generally the best choice for most multithreaded scenarios due to its combination of: Thread safety through synchronization. 

Improved performance and scalability with minimal contention. 

Reasonable memory usage. 

Code 2: Acceptable if contention is not a major concern and simplicity is preferred. 

Code 1: Avoidable in multithreaded contexts as it lacks proper synchronization and can lead to inaccurate results. 

**Additional Considerations:**

False Sharing: All three codes could be susceptible to false sharing depending on memory layout and hardware. consider strategies like padding or data reorganization to mitigate this. 

Overhead: Thread creation and synchronization have inherent overhead. Consider if the gains from multithreading outweigh this overhead for small datasets or tasks. 

Alternative Parallelization: Explore libraries like OpenMP or TBB for simplified parallel programming and potential further performance optimizations. 

M. ZAIN UDDIN

45





Vector processing 

**gcc -msse3 -o vector\_examp**

**vector\_examp.c**

\#include <immintrin.h> 

\#include <stdio.h> 

int main\(\) \{

float data\[\] = \{2.0f, 5.0f, 7.0f, 4.0f\}; // Use floats for SIMD 

\#include <time.h> 

compatibility

\_\_m128 sum\_of\_squares\_vector\(float data\[\], int len\) \{

clock\_t start\_time = clock\(\); 

\_\_m128 sum = sum\_of\_squares\_vector\(data, 4\); 

\_\_m128 total = \_mm\_setzero\_ps\(\); // Initialize vector accumulator \(using \_\_m128 for floats\)

// Extract sum of all elements using horizontal addition: int chunks = len / 4; 

\_\_m128 sum\_horizontal = \_mm\_hadd\_ps\(sum, sum\); // 

Combine elements pairwise

for \(int i = 0; i < chunks; \+\+i\) \{

sum\_horizontal = \_mm\_hadd\_ps\(sum\_horizontal, 

sum\_horizontal\); // Combine pairs again

\_\_m128 chunk = \_mm\_loadu\_ps\(data \+ i \* 4\); // Load 4 

float total\_sum = \_mm\_cvtss\_f32\(sum\_horizontal\); // Extract floats into a vector register

final sum

// Consider aligned load \(\_mm\_load\_ps\) if data is aligned clock\_t end\_time = clock\(\); 

chunk = \_mm\_mul\_ps\(chunk, chunk\); // Square each 

printf\("Sum of squares: %f\\n", total\_sum\); element using vector instructions

printf\("Execution Time: %f seconds\\n", \(\(double\)\(end\_time -

total = \_mm\_add\_ps\(total, chunk\); // Accumulate the start\_time\)\) / CLOCKS\_PER\_SEC\); 

squared elements\}

return 0; 

return total; // Return the vector containing the sum of 

\}

squares

\}\}

M. ZAIN UDDIN

46

Advantages and Disadvantages of all Array Processing:

Functionality: Applies the same operation to all elements of an array simultaneously. 

Advantages: Faster than SISD due to avoiding loop overhead, utilizes CPU caches efficiently. 

Disadvantages: Still sequential data access, not as efficient for highly parallelizable tasks. 

Vector Processing:

Functionality: Exploits SIMD instructions to operate on multiple data elements within a single vector register simultaneously. 

Advantages: Significantly faster than array processing for vectorizable tasks, utilizes dedicated vector units on CPUs. 

Disadvantages: Requires specific data types and instruction sets, more complex code, limited efficiency for non-vectorizable tasks. 

Multi-thread Processing:

Functionality: Splits the workload into smaller chunks and distributes them among multiple threads for parallel execution. 

Advantages: Exploits multiple CPU cores to potentially achieve significant speedups, suitable for independent tasks. 

Disadvantages: Overhead of thread creation and management, synchronization challenges, may not always provide benefits depending on task and hardware. 

M. ZAIN UDDIN

47





Sum of Square using Multiprocessing

\#include <stdio.h> 

\#include <unistd.h> 

if \(child\_pid == 0\) \{

\#include <sys/wait.h> 

// Child process:

\#include <time.h> 

float chunk\_sum = sum\_of\_squares\_scalar\(data \+ i \* chunk\_size, chunk\_size\); write\(pipefd\[1\], &chunk\_sum, sizeof\(float\)\); // Send chunk\_sum to parent float sum\_of\_squares\_scalar\(float data\[\], int len\) \{

close\(pipefd\[0\]\); // Close unused read end

float total = 0.0f; 

close\(pipefd\[1\]\); // Close write end

for \(int i = 0; i < len; \+\+i\) \{

return 0; 

total \+= data\[i\] \* data\[i\]; 

\} else if \(child\_pid > 0\) \{

\}

// Parent process:

return total; 

float chunk\_sum; 

\}

read\(pipefd\[0\], &chunk\_sum, sizeof\(float\)\); // Receive chunk\_sum from child total\_sum \+= chunk\_sum; 

int main\(\) \{

\} else \{

clock\_t start\_time = clock\(\); 

perror\("fork"\); 

float data\[\] = \{2.0f, 4.0f, 5.0f, 7.0f\}; 

return 1; 

\}

int num\_processes = 2; 

\}

int chunk\_size = sizeof\(data\) / num\_processes / sizeof\(float\); close\(pipefd\[0\]\); // Close read end in parent

// Create a pipe for communication

int pipefd\[2\]; 

// Wait for all child processes

if \(pipe\(pipefd\) == -1\) \{

for \(int i = 0; i < num\_processes; \+\+i\) \{

perror\("pipe"\); 

wait\(NULL\); 

return 1; 

\}

\}

clock\_t end\_time = clock\(\); 

printf\("Sum of squares: %f\\n", total\_sum\); float total\_sum = 0.0f; 

Printf\("Execution Time: %f seconds\\n", \(\(double\)\(end\_time - start\_time\)\) / CLOCKS\_PER\_SEC\); return 0; 

for \(int i = 0; i < num\_processes; \+\+i\) \{

\}

int child\_pid = fork\(\); 

Advantages of multiprocessing

**1. Improved Performance: **In scenarios where tasks can be effectively divided and run independently, multiprocessing can significantly improve performance by leveraging the parallelism offered by modern CPUs. Each process can execute its portion of the workload simultaneously, potentially reducing the overall execution time. This is particularly beneficial for computationally intensive tasks and applications. 

**2. Responsiveness: **In certain cases, even for tasks that might not be perfectly parallelizable, using multiple processes can enhance perceived responsiveness. For example, a web server handling multiple client requests could create a separate process for each request, allowing it to handle more concurrent requests without noticeably slowing down individual responses. 

**3. Efficient Resource Utilization: **Multiprocessing can take advantage of idle cores or processors, ensuring that available resources are used effectively. This can be crucial for optimizing performance and scalability on multi-core systems. 

**4. Modularity and Maintainability: **Breaking down complex tasks into smaller, independently running processes can improve code modularity and maintainability. This makes the code easier to understand, debug, and test, potentially reducing development and maintenance costs. 

M. ZAIN UDDIN

49





My single core, superscalar processorexecutesup

**Fetch/ **

**Fetch/ **

**Decode Decode**

totwoinstructionsperclock fromasingle

instructionstream\(ifthe instructionsare

**Exec **

**Exec **

**1**

**2**

independent\)

**MySIMDquad-coreprocessor: **

**executesone8-wideSIMDinstructionper clock**

**Execution **

**fromoneinstructionstreamoneachcore. **

**Context**

**Fetch/ **

**Fetch/ **

**Decode**

**Decode**

**Mydual-coreprocessor:**

**Execution **

**Execution **

**Context**

**Context**

**executesoneinstructionperclock**

**fromoneinstructionstreamoneachcore. **

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Decode**

**Decode**

**Decode**

**Decode**

**ALU**

**ALU**

**\(Execute\)**

**\(Execute\)**

**Execution **

**Execution **

**Context**

**Context**

**Execution **

**Execution **

**Context**

**Context**





Example:four-coreInteli7-7700KCPU

**\(KabyLake\)**

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Fetch/ **

**4coreprocessor**

**Decode**

**Decode**

**Decode**

**Decode**

**Decode**

**Decode**

**Three8-wideSIMDALUsper core **

**\(AVX2instructions\)**

**Execution **

**Execution **

**Contexts**

**Contexts**

**Core1**

**Core2**

**4coresx8-wideSIMDx3x4.2GHz= 400GFLOPs**

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Decode**

**Decode**

**Decode**

**Decode**

**Decode**

**Decode**

**Execution **

**Execution **

**Contexts**

**Contexts**

**Core3**

**Core4**

**\* ShowingonlyAVXmathunits,andfetch/decodeunitforAVX\(additionalcapabilityforintegermath\)** **zain uddin**





Example:NVIDIAV100GPU

**L2Cache\(6MB\)**

**80“SM”cores**

**128SIMDALUsper“SM”\(@1.6 GHz\)= 16TFLOPs \(~250Watts\)**





M. ZAIN UDDIN

53



Issues with accessing memory

Memory

Recall: \[very\] long latency of data access \(Kaby Lake CPU\)

**Latency\(numberofcyclesat4GHz\)**

**Data in L1 cache**

**4**

**Data in L2 cache**

**12**

**DatainL3cache**

**38**

**DatainDRAM\(bestcase\)**

**~248**





Caches reduce the length of stalls \(reduce memory 

access latency\)

**Processors run efficiently when they access data resident in caches** **Caches reduce memory access latency when accessing data that they have recently accessed\! \***

**L1 cache **

**\(32KB\)**

**Core1**

**L2 cache **

**\(256KB\)**

**38GB/sec**

**Memory**

**. **

**DDR4DRAM**

**L3cache **

**. **

**\(8MB\)**

**\(Gigabytes\)**

**L1 cache **

**\(32KB\)**

**CoreN**

**L2 cache **

**\(256KB\)**

**\*Cachesalsoprovidehighbandwidthdatatransfer**

Recall this access pattern

**Address **

**Cacheaction**

**accessed**

**0x0 “coldmiss”,load0x0**

**The program reads an entire array of 16 bytes, and then reads** **0x1 hit**

**the entire array again in the future. **

**Address **

**Value **

**0x2 hit**

**0x0**

**16**

**0**

**0x3 hit**

**0x1**

**255**

**0xe 0x2**

**14**

**0x4 “coldmiss”,load**

**n**

**Assume:**

**iL 0x3**

**0**

**0x4 0x5 hit**

**Total cache capacity = 8 bytes**

**0x4**

**0**

**0x6 hit**

**4**

**Cache has 4-byte cache lines \(So 2 **

**0x5**

**0**

**0x**

**0x7 hit**

**lines fit in cache\)**

**e**

**0x6 **

**6**

**0x8 “coldmiss”,load0x8\(evict**

**ni**

**0x7**

**0**

**The least recently used \(LRU\) **

**L**

**0x0\) 0x9 hit**

**0x8 **

**32**

**replacement policy**

**8**

**0x9**

**48**

**0xA hit**

**0x**

**Discussion Questions:**

**0xA **

**255**

**0xB hit**

**ne**

**Why is there no “hit” on second read of address **

**i**

**0xB**

**255**

**0xC “coldmiss”,load0xC\(evict**

**L**

**0x0? What about second read of address 0x4? **

**0xC **

**255**

**C**

**0x4\) 0xD hit**

**0xD**

**0**

**Would your answer change if the cache had **

**0xe 0xE **

**0**

**0xE hit**

**a capacity of 4 lines? **

**niL 0xF**

**0**

**0xF hit**

**0x0 “capacitymiss”,load0x0\(evict0x8\)**

Data prefetching reduces stalls \(hides latency\)

▪ Many modern CPUs have logic for guessing what data will be accessed in the future and “pre-fetching” this data into caches

**- **Dynamicaly analyze the program’s memory access patterns to make predictions

▪ Prefetching reduces stal s since data is resident in cache when accessed **predict value of r2, initiate load**

**predict value of r3, **

**initiate load**

**... **

**Note: Prefetching can also reduce **

**... **

**performance if the guess is wrong **

**... **

**dataarrivesin**

**\(consumes bandwidth, pollutes **

**caches\)**

**... **

**cache**

**... **

**dataarrivesin**

**... **

**cache**

**ld r0 mem\[r2\]**

**Theseloadsarecachehits**

**ld r1 mem\[r3\]**

**add r0, r0, r1**

**Butwhatifdatahasn’tbeenreadrecently,** **sodoesnotresideincache? **

**Andthenextpieceofdatato **

**readisnoteasilypredictable? **

Multi-threading reduces stalls

▪ **Idea \#3: interleave processing of multiple threads on the same** **core to hide stalls**

**- If you can’t make progress on the current thread… work on** **another one**





Hidingstalswithmulti-threading

**Thread1**

**Time Elements0… 7**

**1Core\(1thread\)**

**Fetch/ **

**Decode**

**ALU0 ALU1 ALU2 ALU3**

**ALU4 ALU5 ALU6 ALU7**

**Exec Ctx**





Hidingstalswithmulti-threading

**Thread1**

**Thread2**

**Thread3**

**Thread4**

**Elements0… 7**

**Elements8… 15**

**Elements16… 23**

**Elements24… 31**

**Time**

**1**

**2**

**3**

**4**

**1Core\(4hardwarethreads\)**

**Fetch/ **

**Decode**

**ALU0 ALU1 ALU2 ALU3**

**ALU4 ALU5 ALU6 ALU7**

**1**

**2**

**3**

**4**





Hidingstalswithmulti-threading

**Thread1**

**Thread2**

**Thread3**

**Thread4**

**Elements0… 7**

**Elements8… 15**

**Elements16… 23**

**Elements24… 31**

**Time**

**1**

**2**

**3**

**4**

**1Core\(4hardwarethreads\)**

**Stal**

**Fetch/ **

**Decode**

**ALU0 ALU1 ALU2 ALU3**

**ALU4 ALU5 ALU6 ALU7**

**Runnable**

**1**

**2**

**3**

**4**





Hiding stalls with multi-threading

**Thread1**

**Thread2**

**Thread3**

**Thread4**

**Elements0… 7**

**Elements8… 15**

**Elements16… 23**

**Elements24… 31**

**Time**

**1**

**2**

**3**

**4**

**1Core\(4hardwarethreads\)**

**Stal**

**Fetch/ **

**Decode**

**ALU0 ALU1 ALU2 ALU3**

**Stal**

**ALU4 ALU5 ALU6 ALU7**

**Runnable**

**Stal**

**1**

**2**

**Stal**

**Runnable**

**3**

**4**

**Runnable**

**Done\! **

**Runnable**

**Done\! **





Throughput computing: a trade-off

**Thread 1**

**Thread 2**

**Thread 3**

**Thread 4**

**Elements 0 … 7 Elements 8 … 15**

**Elements 16 … 23 Elements 24 … 31**

**Time**

**Key idea of throughput-oriented systems:**

**Stall**

**Potentially increase time to complete work by **

**any one thread, in order to increase overall **

**system throughput when running multiple **

**threads. **

**Runnable**

**Note: during this time, this thread is runnable,** **but it is not being executed by the processor **

**core. **

**\(The core is executing instructions from **

**another thread.\)**

**Done\! **





No free lunch: storing execution contexts

Consider on-chip storage of execution contexts as a finite resource **Fetch/ **

**Decode**

**ALU0**

**ALU1**

**ALU2**

**ALU3**

**ALU4**

**ALU5**

**ALU6**

**ALU7**

**Context storage **

**\(or L1 cache\)**





Many small contexts \(high latency hiding ability\)

**16 hardware threads: storage for a small working set per thread** **Fetch/ **

**Decode**

**ALU0**

**ALU1**

**ALU2**

**ALU3**

**ALU4**

**ALU5**

**ALU6**

**ALU7**

**1**

**2**

**3**

**4**

**5**

**6**

**7**

**8**

**9**

**10**

**11**

**12**

**13**

**14**

**15**

**16**





Four large contexts \(low latency hiding ability\)

**4 hardware threads: storage for large working set per thread** **Fetch/ **

**Decode**

**ALU0**

**ALU1**

**ALU2**

**ALU3**

**ALU4**

**ALU5**

**ALU6**

**ALU7**

**1**

**2**

**3**

**4**





Exercise: Consider a simple two-threaded core

**Memory**

**Data **

**Cache**

**Fetch/ **

**Decode**

**ALU**

**\(Execution unit\)**

**Execution **

**Execution **

**Context 0**

**Context 1**

**\(HWthread\) **

**\(HWthread\) **

**PC**

**PC**

**R0**

**R4**

**R0**

**R4**

**R1**

**R5**

**R1**

**R5**

**R2**

**R6**

**R2**

**R6**

**R3**

**R7**

**R3**

**R7**

**Singlecoreprocessor,multi-threadedcore\(2threads\). **

**Canrunonescalarinstructionperclockfrom **

**oneofthehardwarethreads**

What is the utilization of the core? \(one thread\) **Thread 0**

***stal***

***stal***

***stal …***

**3/15 = 20%**

**Assume we are running a **

**program where threads **

**perform three arithmetic **

**instructions, fol owed by **

**memory load**

**\(with 12 cycle latency\)**

**0**

**5**

**1**

**1**

**2**

**2**

**3**

**3**

**0**

**5**

**0**

**5**

**0**

**5**

What is the utilization of the core? \(two threads\) **Thread0**

**Thread1**

**Assumewearerunninga**

**6/15= 40%**

**programwherethreadsperform **

**threearithmeticinstructions, **

**folowed bymemoryload**

**\(with12cyclelatency\)**

**0**

**5**

**10**

**15**

**20**

**25**

**30**

**35**

How many threads are needed to achieve 100% utilization? 

**Thread0**

**Thread1**

**Assumewearerunning a **

**programwherethreads **

**perform threearithmetic**

**instructions, folowed bya **

**memory load**

**\(with12cycleslatency\)**

**0**

**5**

**10**

**15**

**20**

**25**

**30**

**35**

Fivethreadsneededtoobtain100%utilization **Thread0**

**Thread1**

**Thread2**

**Thread3**

**Thread4**

**Fivethreads**

**required for100%**

**utilization**

**0**

**5**

**10**

**15**

**20**

**25**

**30**

**35**

Additionalthreadsyieldnobenefit\(already100%utilization\) **Thread0**

**Thread1**

**Thread2**

**Thread3**

**Thread4**

**Thread5**

**Thread6**

**Thread7**

**0**

**15**

**20**

**25**

**30**

**35**

**S5til 100%**

**10**

How many threads are needed to achieve 100% utilization? 

Threads now perform *six arithmetic instructions*, folowed by memory load \(with 12 cycle latency\) **Thread 0**

**0**

**5**

**10**

**15**

**20**

**25**

**30**

**35**

Now only three threads needed for 100% utilization? 

Threads now perform *six arithmetic instructions*, folowed by memory load \(with 12 cycle latency\) **Thread 0**

**Thread 1**

**Thread 2**

**0**

**5**

**10**

**15**

**20**

**25**

**30**

**35**

**100% utilization using only three threads**

**How does a higher ratio of math instructions to memory latency afect the number of threads needed for latency hiding? **

**Takeaway \(point 1\):**

**A processor with multiple hardware threads can *avoid stalls *****by** **performing instructions from other threads when one thread must wait** **for a long latency operation to complete. **

**Note: the latency of the memory operation is not** **changed by multi-threading, it just no longer causes** **reduced processor utilization. **

**Takeaway \(point 2\):**

**A multi-threaded processor hides memory latency by performing** **arithmetic from other threads. **

**Programs that feature more arithmetic per memory** **access need fewer threads to hide **

**memory stalls. **

Hardware-supported multi-threading

▪ **Core manages execution contexts for multiple threads**

- **Core still has the same number of ALU resources: multi-threading only helps use them** **more efficiently in the face of high-latency operations like memory access**

- **Processor makes decision about which thread to run each clock**

▪ **Interleaved multi-threading \(a.k.a. temporal multi-threading\)**

- **What I described on the previous slides: each clock, the core chooses a thread, and** **runs an instruction from the thread on the core’s ALUs**

▪ **Simultaneous multi-threading \(SMT\)**

- **Each clock, core chooses instructions from multiple threads to run on ALUs**

- **Example: Intel Hyper-threading \(2 threads per core\)**

- **See “going further videos” provided online**





fictitious multi-core chip

**16 cores**

**8 SIMD ALUs per core \(128 **

**total\)**

**4 threads per core**

**16 simultaneous **

**instruction streams**

**64 total concurrent **

**instruction streams**

**512 independent pieces of work **

**are needed to run a chip with **

**maximal latency hiding ability**





Example: Intel Skylake/Kaby Lake core

**Core 0**

**L2 Data **

**Cache**

**L1 Data **

**Cache**

**instruction selection**

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Decode**

**Decode**

**Decode**

**Decode**

**Decode**

**Decode**

**ALU ALU ALU ALU **

**ALU**

**ALU**

**ALU**

**ALU**

**ALU ALU ALU ALU ALU ALU ALU ALU **

**ALU ALU ALU ALU ALU ALU ALU ALU ALU ALU ALU ALU**

**8-wide vector ALU MUL or **

**scalar ALU**

**scalar ALU**

**\(scalar ALU\) \(scalar ALU\)**

**8-wide vector ALU **

**8-wide vector ALU **

**FP ADD or MUL FP ADD or MUL**

**ADD**

**MUL or ADD**

**ADD**

**Execution **

**Execution **

**Context 0**

**Context 1**

**Two-way multi-threaded cores \(2 threads\). **

**Each core can run up to four independent scalar instructions** **and up to three 8-wide vector instructions**

**\(up to 2 vector mul or 3 vector add\)**

**Not shown on this diagram: units for LD/ST operations**





NVIDIAV100

▪ **SM= “StreamingMulti-processor” **

GPUs:extremethroughput-orientedprocessors **ThisisoneNVIDIAV100streamingmulti-processor\(SM\)unit** **WarpSelector**

**WarpSelector**

**WarpSelector**

**WarpSelector**

**64 “warp” execution contexts per SM**

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Fetch/ **

**Decode**

**Decode**

**Decode**

**Decode**

**Wide SIMD: 16-wide SIMD ALUs \(carry **

**out 32-wide SIMD execute over 2 **

**clocks\)**

**64 x 32 = up to 2048 data items **

**processed concurrently per “SM” **

**core**

**R0 0 1 2**

**…**

**30 31**

**R0 0 1 2**

**…**

**30 31**

**R0 0 1 2**

**…**

**30 31**

**R0 0 1 2**

**…**

**30 31**

**R1**

**R1**

**R1**

**R1**

**R2**

**Warp 0**

**R2**

**Warp 1**

**R2**

**Warp 2**

**R2**

**Warp 3**

**64KB**

**… **

**… **

**… **

**… **

**R0**

**R0**

**R0**

**R0**

**registers per **

**R1**

**R1**

**R1**

**R1**

**sub-core**

**R2**

**Warp 4**

**R2**

**Warp 5**

**R2**

**Warp 6**

**R2**

**Warp 7**

**…**

**…**

**…**

**…**

**256KB**

**…**

**…**

**…**

**…**

**registers in**

**totalper SM**

**R**

**R**

**R**

**R**

**0 **

**0 **

**0 **

**0 **

**Registersdivided among **

**Warp 60**

**Warp 61**

**Warp 62**

**Warp 63**

**R2**

**R2**

**R2**

**R2**

**1**

**…**

**1**

**…**

**1**

**…**

**1**

**…**

**\(upto\)64“warps”per SM**

**“Shared” memory \+L1 cache storage\(128 KB\)**

**= SIMDfp32functionalunit, **

**= SIMDintfunctionalunit, **

**= SIMDfp64functionalunit, **

**= Tensorcoreunit**

**controlsharedacross16units **

**controlsharedacross16units **

**controlsharedacross8units **

**= Load/storeunit**

**\(16xMUL-ADDperclock\*\)**

**\(16xMUL/ADDperclock\*\)**

**\(8xMUL/ADDperclock\*\*\)**

**\* one32-wideSIMDoperationevery2clocks**

**\*\* one32-wideSIMDoperationevery 4clocks**





NVIDIAV100

**Thereare80SMcoresontheV100:**

**That’s163,840piecesofdatabeing **

**processedconcurrentlytoget **

**maximallatencyhiding\! **

**L2Cache\(6MB\)**

**900GB/sec**

**\(4096bitinterface\)**

**GPUmemory \(HBM\)**

**\(16GB\)**

The story so far…

**To utilize modern parallel processors efficiently, an application must:** **1. Have sufficient parallel work to utilize all available** **execution units \(across many cores and many execution** **units per core\)**

**2. Groups of parallel work items must require the same sequences** **of instructions \(to utilize SIMD execution\)**

**3. Expose more parallel work than processor ALUs to enable** **interleaving of work to hide memory stalls**

Introduction to Concurrency Control Definition:

Concurrency control involves managing simultaneous access to shared resources in a way that ensures the correctness of the program's execution. 

Importance:

Ensures consistency and avoids data corruption in multithreaded and multiprocessor applications. 

M. ZAIN UDDIN

86

Synchronization

•**Definition:**

• Synchronization involves coordinating the execution of threads or processes to maintain consistency and order. 

•**Types of Synchronization:**

• **Semaphores: **Control access to resources with a counter. 

• **Mutex \(Mutual Exclusion\):**

• Protect critical sections by allowing only one thread at a time. 

M. ZAIN UDDIN

87

Mutual Exclusion

Definition:

Mutual exclusion ensures that only one thread or process accesses a critical section at a time. 

Example:

Scenario:

Two threads attempting to update a shared counter simultaneously. 

M. ZAIN UDDIN

88

Techniques for Mutual Exclusion

•**Mutex \(Mutual Exclusion\):**•**Semaphore:**

• A synchronization primitive to • A synchronization primitive for protect shared resources. 

controlling access to a shared 

• Example

resource

•

•

pthread\_mutex\_t mutex; 

Example

•

• sem\_t semaphore; 

pthread\_mutex\_init\(&mutex, NULL\); 

• sem\_init\(&semaphore, 0, 1\); // Initialize with 

• pthread\_mutex\_lock\(&mutex\); 

a counter of 1

• // Critical section

• sem\_wait\(&semaphore\); 

• pthread\_mutex\_unlock\(&mutex\); 

• // Critical section

• sem\_post\(&semaphore\); 

M. ZAIN UDDIN

89



M. ZAIN UDDIN

90



\#include <stdio.h> 

\#include <pthread.h> 

MUTEX

int shared\_counter = 0; 

pthread\_mutex\_t mutex; 

void\* update\_counter\(void\* arg\) \{

pthread\_mutex\_lock\(&mutex\); // Acquire the lock to ensure mutual exclusion shared\_counter\+\+; 

printf\("Thread %ld updated counter to %d\\n", \(long\)arg, shared\_counter\); pthread\_mutex\_unlock\(&mutex\); // Release the lock after updating the counter return NULL; 

\}

int main\(\) \{

pthread\_t thread1, thread2; 

pthread\_mutex\_init\(&mutex, NULL\); // Initialize the mutex

// Create two threads to update the shared counter

pthread\_create\(&thread1, NULL, update\_counter, \(void\*\)1\); pthread\_create\(&thread2, NULL, update\_counter, \(void\*\)2\); 

// Wait for both threads to complete

pthread\_join\(thread1, NULL\); 

pthread\_join\(thread2, NULL\); 

pthread\_mutex\_destroy\(&mutex\); // Destroy the mutex return 0; 

\}

M. ZAIN UDDIN

91



\#include <stdio.h> 

\#include <pthread.h> 

\#include <semaphore.h> 

SEMAPHORE

int shared\_counter = 0; 

sem\_t semaphore; 

void\* update\_counter\(void\* arg\) \{

sem\_wait\(&semaphore\); // Wait on the semaphore, decrementing its value shared\_counter\+\+; 

printf\("Thread %ld updated counter to %d\\n", \(long\)arg, shared\_counter\); sem\_post\(&semaphore\); // Signal the semaphore, incrementing its value return NULL; 

\}

int main\(\) \{

pthread\_t thread1, thread2; 

sem\_init\(&semaphore, 0, 1\); // Initialize the semaphore with an initial value of 1

// Create two threads to update the shared counter

pthread\_create\(&thread1, NULL, update\_counter, \(void\*\)1\); pthread\_create\(&thread2, NULL, update\_counter, \(void\*\)2\); 

// Wait for both threads to complete

pthread\_join\(thread1, NULL\); 

pthread\_join\(thread2, NULL\); 

sem\_destroy\(&semaphore\); // Destroy the semaphore after its use return 0;\}

M. ZAIN UDDIN

92

Conclusion

•**Key Takeaways:**

•Have sufficient parallel work to utilize all available execution units \(across many cores and many execution units per core\)

•Groups of parallel work items must require the same sequences of instructions \(to utilize SIMD execution\)

•Expose more parallel work than processor ALUs to enable interleaving of work to hide memory stalls

• Mutual exclusion and synchronization are crucial for avoiding data corruption in concurrent programs. 

M. ZAIN UDDIN

93



