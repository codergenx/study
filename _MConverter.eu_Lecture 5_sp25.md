Lecture \# 5

By: Muhammad Zain Uddin

email: zuddin@iba.edu.pk

M. ZAIN UDDIN

1





M. ZAIN UDDIN

2





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

3



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

4



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

5





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

6



Headers:

stdio.h: Provides standard input/output functions like printf. 

pthread.h: Includes functions for multithreading, such as thread creation and mutexes. 

Structure:

thread\_data\_t: Represents data passed to worker threads: start: Starting index for the thread's data segment. 

end: Ending index for the thread's data segment. 

data: Pointer to the shared array of integers. 

partial\_sum: Not used in this version. 

Global Variables:

total\_sum: Stores the cumulative sum of squares, shared among threads. 

mutex: Mutex lock to protect total\_sum from concurrent access. 

Worker Function:

worker:

Takes a thread\_data\_t pointer as input. 

Calculates a partial sum of squares within its assigned data segment. 

Acquires the mutex lock to protect total\_sum. 

Adds the partial sum to total\_sum. 

Releases the mutex lock. 

Returns NULL. 

M. ZAIN UDDIN

7



Sum of Squares Function:

sum\_of\_squares\_multithread:

Takes the data array, its length, and the desired number of threads as input. 

Creates an array of threads and thread\_data\_t structures. 

Divides the data into chunks and assigns them to threads. 

Initializes the mutex lock. 

Creates the threads, passing worker and corresponding thread\_data\_t. 

Waits for all threads to finish using pthread\_join. 

Destroys the mutex lock. 

Returns the final sum of squares \(total\_sum\). 

Main Function:

main:

Creates a sample data array. 

Calls sum\_of\_squares\_multithread with the array, its length, and 2 threads. 

Prints the calculated sum of squares. 

Returns 0 to indicate successful execution. 

M. ZAIN UDDIN

8





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

std::mutex mtx; // Global mutex for synchronization

return total\_sum; 

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

9

**Structure:**

Data Structures:

thread\_data\_t: This structure holds information for each thread, including its start and end indices within the data array, a pointer to the data itself, and a pointer to an integer partial\_sum. 

global mutex: A single std::mutex object used for thread synchronization when accessing the total sum. 

**Functions:**

worker: This function is executed by each thread. It calculates the sum of squares for its assigned subset of the data array and stores it in the partial\_sum variable. Then, it acquires the global mutex lock, adds its partial sum to the total sum, releases the lock, and exits. 

sum\_of\_squares\_multithread: This function performs the overall multithreaded computation. It creates threads, defines and assigns data to each thread, joins the threads to wait for completion, and finally aggregates the partial sums into the final total sum. 

M. ZAIN UDDIN

10

**Algorithm:**

• **Initialization:**

• Define the data array, number of threads, and chunk size for dividing the work. 

• Allocate and initialize thread data structures and the global mutex. 

• **Thread Creation:**

• For each thread, set its start and end indices based on the chunk size and thread ID. 

• Create a thread and pass the corresponding thread\_data\_t structure as an argument. 

• **Thread Execution:**

• Each thread iterates over its assigned sub-array, calculating the sum of squares for each element. 

• The thread then acquires the global mutex lock, ensuring atomic access to the total sum. 

• It adds its partial sum to the total sum and releases the lock. 

• **Result Aggregation:**

• The main thread waits for all created threads to finish using pthread\_join. 

• After all threads are done, it iterates through the partial\_sum variables of each thread data structure. 

• It acquires the mutex lock again for each iteration to protect the total sum. 

• It adds each partial sum to the total sum and releases the lock. 

• **Cleanup:**

• The main thread frees the allocated memory for each thread data structure. 

• It destroys the global mutex. 

M. ZAIN UDDIN

11

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

12

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

13

Posix Threading API:

All three codes use the Posix Threading API for creating and managing threads. This API provides functions like pthread\_create, pthread\_join, and pthread\_mutex\_init/destroy to handle thread creation, synchronization, and resource management. 

•pthread\_create: Spawns a new thread to run a function with arguments. 

•pthread\_join: Waits for a specific thread to finish its execution. 

•pthread\_mutex\_init/destroy: Initializes and cleans up a mutex object for thread synchronization. 

•pthread\_mutex\_lock/unlock: Acquires and releases a lock on a mutex, managing access to shared resources. 

Code 1 and 2 use mutexes \(pthread\_mutex\_t\) to synchronize access to the shared total\_sum variable and avoid race conditions. 

Code 3 introduces separate partial\_sum variables for each thread, reducing the need for frequent mutex access and potential contention. 

M. ZAIN UDDIN

14

GDB \(GNU Debugger\)

1. Compile with debugging symbols:

Run this command in your terminal to compile the code with debugging information: gcc TH\_EXAMP.C -o THREAD

2. Start GDB:

Open a new terminal window and type the following command to start GDB: gdb sum\_squares

3. Set breakpoints:

Use the break command followed by the line number or function name to set breakpoints at the places you want to pause the program execution. Here's how you can set breakpoints at the commented lines in your code:

•Observe thread creation: break main

•Inspect final result: break main:14 \(replace 14 with the actual line number where you want to break after printing the sum\)

•Observe worker thread execution: break worker

•Observe thread synchronization: break sum\_of\_squares\_multithread 4. Run the program:

After setting your breakpoints, type run to start the program execution. 

5. Use GDB commands at breakpoints:

Once the program hits a breakpoint, you can use various GDB commands to inspect the state of your program. Here are some helpful commands:

•info threads: Display information about all threads, including their IDs and states. 

•thread N: Switch to thread N \(replace N with the thread ID\). 

•print var: Print the value of a variable named var. 

•next: Step over the next line of code without entering a function. 

•step: Step into the next line of code, even if it's a function call. 

•continue: Resume program execution until the next breakpoint or the end of the program. 

M. ZAIN UDDIN

15





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

printf\("Sum of squares: %f\\n", total\_sum\); 

element using vector instructions

printf\("Execution Time: %f seconds\\n", \(\(double\)\(end\_time -

total = \_mm\_add\_ps\(total, chunk\); // Accumulate the 

start\_time\)\) / CLOCKS\_PER\_SEC\); 

squared elements\}

return 0; 

return total; // Return the vector containing the sum of 

\}

squares

M. ZAIN UDDIN

\}\}

16

1. Header Inclusion:

immintrin.h: Provides intrinsic functions for accessing SIMD instructions \(like \_mm\_setzero\_ps, \_mm\_loadu\_ps, \_mm\_mul\_ps, \_mm\_add\_ps, \_mm\_hadd\_ps, and \_mm\_cvtss\_f32\). 

stdio.h: Contains functions for input/output, like printf. 

2. Function for Sum of Squares Using SIMD:

\_\_m128 Data Type: Represents a 128-bit vector register capable of holding 4 single-precision floating-point values. 

\_mm\_setzero\_ps\(\): Initializes a vector register to all zeros. 

\_mm\_loadu\_ps\(data \+ i \* 4\): Loads 4 floats from memory into a vector register, allowing for unaligned data. 

\_mm\_mul\_ps\(chunk, chunk\): Performs element-wise multiplication of a vector with itself, squaring each element. 

\_mm\_add\_ps\(total, chunk\): Adds two vectors element-wise, accumulating the squared values. 

3. Main Function:

\_mm\_hadd\_ps\(sum, sum\): Performs horizontal addition, combining elements pairwise to reduce the number of active elements. 

\_mm\_cvtss\_f32\(sum\_horizontal\): Extracts a single float from a vector register. 

printf\("Sum of squares: %f\\n", total\_sum\): Prints the calculated sum of squares. 

M. ZAIN UDDIN

17

Advantages and Disadvantages of all

Array Processing:

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

18

Synchronization

•**Definition:**

• Synchronization involves coordinating the execution of threads or processes to maintain consistency and order. 

•**Types of Synchronization:**

• **Semaphores: **Control access to resources with a counter. 

• **Mutex \(Mutual Exclusion\):**

• Protect critical sections by allowing only one thread at a time. 

M. ZAIN UDDIN

19

Mutual Exclusion

Definition:

Mutual exclusion ensures that only one thread or process accesses a critical section at a time. 

Example:

Scenario:

Two threads attempting to update a shared counter simultaneously. 

M. ZAIN UDDIN

20

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

21



M. ZAIN UDDIN

22



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

23



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

24

OpenMP

●

OpenMP is an extension of C used for multi-threaded code \(shared memory, so no multi-node computation\)

●

Compiled with the additional flag "gcc -fopenmp foo.c" 

○

"\#include <omp.h>" 

●

Standardized over many languages

●

Generally follows the fork-join framework

●

Each thread has its own stack for private variables, but otherwise shares memory with other threads

●

OpenMP code generally is written using lines like "\#pragma omp <command>" 

25

\#pragma omp parallel

●

In order to create a parallel section:

\#pragma omp parallel

\{

//parallel code

\}

●

C syntax note: brackets mean "previous declaration applies to the all the lines inside me". This means that if we write only one line of code in a parallel section \(or if clause, or for loop\), we don't need to write brackets. 

●

The code in the parallel section gets run on all threads, so we need some way to distinguish threads

●

In a parallel segment:

26

○

omp\_get\_num\_threads\(\) returns the number of threads running

○

opm\_get\_thread\_num\(\) returns a unique number from 0-num\_threads per thread

Parallel Hello World

\#include <stdio.h> 

\#include <omp.h> 

int main \(\) \{

int x = 0; //Shared variable

\#pragma omp parallel

\{

int tid = omp\_get\_thread\_num\(\); //Private variable

x\+\+; 

printf\("Hello World from thread %d, x = %d\\n", tid, x\); if\(tid==0\) \{

printf\("Number of threads = %d\\n", omp\_get\_num\_threads\(\)\); 

\}

\}

printf\("Done with parallel segment\\n"\); 

\}

Shared vs Private variables

●

By default, any variable declared outside the parallel segment is shared: all threads write/read from the same variable

●

Any variable declared inside the parallel segment is private: Each thread has its own version of the variable. 

●

Can overrule this with the private and shared keywords:

\#pragma omp parallel private\(var\) shared\(var2\)

●

Note that heap memory is always shared, though we can have private pointers and private mallocs \(if we do the malloc in the parallel segment, and free them within the parallel segment\) 28

For loops

●

Problem: You have to do some work over an array of 1 million numbers, with 4 people. How do you split the work? 

●

Assumptions: 

○

We need to decide this before we run the code

○

Each element of the array is independent, so we can do this in any order

○

The threads are about equally fast at work, so we want to assign each of them 250k numbers 29

For loops

●

Option 1: Do every 4

○

for\(int i = tid; i<1000000;i\+=4\)

○

"Interweaving" 

●

Option 2: Thread 0 does 0-249999, 1 does 250000-499999, etc. 

○

for\(int i = tid\*250000;i<\(tid\+1\)\*250000;i\+\+\)

○

"Blocking" 

●

Which one's better? 

○

With standard multithreading, Option 1 actually is as slow as the serial version of this code due to cache coherency issues… More on this in coming class

○

Option 2 speeds things up correctly

○

Aside: Option 1 does end up being the preferred option when dealing with GPU programming, though that's due to how GPU threads differ from normal threads. 

30

For loops

●

Option 3: Let the compiler do it for you with the \#pragma omp for keyword. 

●

\#pragma omp for must be written inside an already existing parallel segment

●

If a parallel segment consists only of one for loop, we can combine the two declarations with 

\#pragma omp parallel for

○

\#pragma omp parallel for

for\(int i = 0; i<1000000;i\+\+\)

31

Data Races

●

Note that when we ran Hello World parallel, we ended up with the threads running in random order

○

In fact, every time we run Hello World, we get a different order\! 

○

The x values stayed largely in-order, but didn't always strictly increase

●

Recall the OS can choose whichever threads it wants to run, and change threads at any time

●

This is one of the biggest downsides to multithreading: A multithreaded program is no longer deterministic, and will have a random execution order every time we run the program. 

●

Formally, a multithreaded program is only considered correct if ANY interlacing of threads yield the same result. 

32

Data Race: Example

●

To analyze this, we need to see the equivalent assembly code

○

C will compile to x86, but we can still do a correct analysis by compiling to RISC-V, since we're mainly trying to reduce the code to atomic instructions. We can assume that no two atomic instructions happen simultaneously. 

●

Only the loads and stores affect shared memory, so we only need to consider the different ways we can order the loads and stores

●

Even with this, there are 8\!/\(2\!\)4=2520 different possible orders

■

Can use the fact that all the threads are identical to reduce this to 105 orders, but still too many to check manually sw x0 0\(sp\)

33

**lw t0 0\(sp\)**

**lw t0 0\(sp\)**

**lw t0 0\(sp\)**

**lw t0 0\(sp\)**

**addi t0 t0 1**

**addi t0 t0 1**

**addi t0 t0 1**

**addi t0 t0 1**

**sw t0 0\(sp\)**

**sw t0 0\(sp\)**

**sw t0 0\(sp\)**

**sw t0 0\(sp\)**

Data Race: Example

●

Case 1: All the threads run one at a time

sw x0 0\(sp\)

○

Purple thread reads x = 0

**lw t0 0\(sp\)**

○

Purple thread stores x = 1

○

Brown thread reads x = 1

**addi t0 t0 1**

○

Brown thread stores x = 2

**sw t0 0\(sp\)**

○

Red thread reads x = 2

○

Red thread stores x = 3

**lw t0 0\(sp\)**

○

Blue thread reads x = 3

○

Blue thread stores x = 4

**addi t0 t0 1**

●

Final value: 4

**sw t0 0\(sp\)**

**lw t0 0\(sp\)**

34

**addi t0 t0 1**

**sw t0 0\(sp\)**

**lw t0 0\(sp\)**

**addi t0 t0 1**

**sw t0 0\(sp\)**

Data Race: Example

sw x0 0\(sp\)

●

Case 2: The threads are perfectly interleaved

**lw t0 0\(sp\)**

○

Purple thread reads x = 0

**lw t0 0\(sp\)**

○

Red thread reads x = 0

○

Brown thread reads x = 0

**lw t0 0\(sp\)**

○

Blue thread reads x = 0

**lw t0 0\(sp\)**

○

Purple thread stores x = 1

○

Brown thread stores x = 1

**addi t0 t0 1**

○

Red thread stores x = 1

**addi t0 t0 1**

○

Blue thread stores x = 1

●

Final value: 1

**addi t0 t0 1**

**addi t0 t0 1**

**sw t0 0\(sp\)**

**sw t0 0\(sp\)**

**sw t0 0\(sp\)**

**sw t0 0\(sp\)**

35

Data Race: Example

●

Case 3: Same as case 1, except purple's store happens last sw x0 0\(sp\)

○

Purple thread reads x = 0

**lw t0 0\(sp\)**

○

Brown thread reads x = 0

○

Brown thread stores x = 1

**addi t0 t0 1**

○

Red thread reads x = 1

**lw t0 0\(sp\)**

○

Red thread stores x = 2

○

Blue thread reads x = 2

**addi t0 t0 1**

○

Blue thread stores x = 3

○

Purple thread stores x = 1

**sw t0 0\(sp\)**

●

Final value: 1

**lw t0 0\(sp\)**

**addi t0 t0 1**

36

**sw t0 0\(sp\)**

**lw t0 0\(sp\)**

**addi t0 t0 1**

**sw t0 0\(sp\)**

**sw t0 0\(sp\)**

Data Race: Example

●

Some other ordering? 

sw x0 0\(sp\)

sw x0 0\(sp\)

○

We can find orderings that give x=2,3

●

Can we do any more/less? 

**lw t0 0\(sp\)**

**lw t0 0\(sp\)**

●

Can't go above 4

**lw t0 0\(sp\)**

**lw t0 0\(sp\)**

○

Only 4 "\+1s" overall, so can't increase to 5 or **lw t0 0\(sp\)**

**addi t0 t0 1**

more

●

Can't go below 1

**addi t0 t0 1**

**addi t0 t0 1**

○

The smallest value that can be loaded by a 

**addi t0 t0 1**

**sw t0 0\(sp\)**

thread is 0, so the smallest value that can be 

stored is 1. Therefore, the last store must be at 

**addi t0 t0 1**

**lw t0 0\(sp\)**

least 1. 

**sw t0 0\(sp\)**

**addi t0 t0 1**

●

Therefore, we can get any value between 1 and 

37

4

**lw t0 0\(sp\)**

**sw t0 0\(sp\)**

**addi t0 t0 1**

**lw t0 0\(sp\)**

**sw t0 0\(sp\)**

**addi t0 t0 1**

**sw t0 0\(sp\)**

**sw t0 0\(sp\)**

**sw t0 0\(sp\)**

**sw t0 0\(sp\)**

Avoiding Data Races

●

Formally, a multithreaded program is only considered correct if ANY interlacing of threads yield the same result. 

●

For today: if you make sure that each thread works on independent data \(no two threads write to the same value, or read a value that another thread wrote to\), you can guarantee correctness

●

Tommorow: how to handle cases where coordination is mandatory

●

The hardest part of multithreading is maintaining correctness while also speeding up the code, but this ends up being a fairly transferable skill to project management

○

If you can coordinate a group of threads to perform a task, you can coordinate a group of people to perform a task more easily. 

38

Data Races/Race Conditions

●

Note that when we ran Hello World parallel, we ended up with the threads running in random order

○

In fact, every time we run Hello World, we get a different order\! 

○

The x values stayed largely in-order, but didn't always strictly increase

●

Recall the OS can choose whichever threads it wants to run, and change threads at any time

●

This is one of the biggest downsides to multithreading: A multithreaded program is no longer deterministic, and will have a random execution order every time we run the program. 

●

Formally, a multithreaded program is only considered correct if ANY interlacing of threads yield the same result. 

39

Data Race Example: Retrospective

●

In practice, most times you run this code, you get 4

○

Each thread is small enough that it's unlikely to get interrupted

●

Empirical tests suggest an error rate around 0.01%. 

●

In summation, race condition bugs are:

○

Rare

○

Nondeterministic

○

Silent-failing \(you get the wrong answer instead of crashing the program\)

●

Very difficult to debug. You have been warned…

40

Avoiding Data Races

●

Formally, a multithreaded program is only considered correct if ANY interlacing of threads yield the same result. 

●

If you make sure that each thread works on independent data \(no two threads write to the same value, or read a value that another thread wrote to\), you can guarantee correctness

●

The hardest part of multithreading is maintaining correctness while also speeding up the code, but this ends up being a fairly transferable skill to management

○

If you can coordinate a group of threads to perform a task, you can coordinate a group of people to perform a task more easily. 

●

How to handle cases where coordination is mandatory? 

41

Locks

●

A lock is an object which helps with synchronization

●

Essentially, each thread can try to "acquire" a lock, but only one thread can have the lock at a given time. 

○

Think bathroom stall lock; only one person can use the stall at a time, and we use atomics to make sure two people don't go into the same stall at the same time

●

Formally, has two operations

○

acquire: Tries to acquire the lock. If successful, keep going. Otherwise, wait a bit and try again later. 

○

release: Unlocks the lock and continues. Only works if we had the lock to start with. 

○

Optional but common: try-acquire: Same as acquire, but if the lock is being used, return false and let the thread continue running

●

Code surrounded by a lock is called a "critical section", because only one thread is allowed to run that section at a time. 

42

Locks: Downsides

●

Using a lock inherently means you need to pause one thread while waiting for another thread to run the critical segment

●

Ends up making some parts of your code serial

○

Amdahl's Law strikes again\! 

●

Is it possible for all threads to get stuck? 

43



