<!-- Slide number: 1 -->
# Lecture # 9
By: Muhammad Zain Uddin
email: zuddin@iba.edu.pk

M. Zain Uddin
1

### Notes:

<!-- Slide number: 2 -->
# Agenda
GPU Programming
CUDA Programing
Parallel and Distributed Computing – Spring 2025
2

<!-- Slide number: 3 -->
# Attribution
Today’s lecture is based on Stanford's Parallel Computing course and NVIDIA's CUDA Programming Tutorial
Parallel and Distributed Computing – Spring 2025
3

<!-- Slide number: 4 -->
# Question
What is the difference between latency and throughput ?
Parallel and Distributed Computing – Spring 2025
4

<!-- Slide number: 5 -->
# Latency Oriented Design vs Throughput Oriented Design

![](ContentPlaceholder5.jpg)
Parallel and Distributed Computing – Spring 2025
5

<!-- Slide number: 6 -->
# Comparison

![](ContentPlaceholder5.jpg)
Parallel and Distributed Computing – Spring 2025
6

### Notes:
GPU (NVIDIA V100) Analysis:
Each element-wise multiplication requires three memory operations (loading two inputs and storing one result), which totals 12 bytes per operation.
The V100 GPU is capable of 5120 floating-point 32-bit multiplications per clock cycle at 1.6 GHz.
To fully utilize the GPU’s computational power, an enormous memory bandwidth of ~98 TB/sec is required.
However, the actual memory bandwidth available is much lower, leading to an efficiency of less than 1%.
CPU (Xeon E5v4) Analysis:
The Xeon E5v4 CPU is an eight-core processor running at 3.2 GHz.
It is connected to a memory system with a 76 GB/sec memory bandwidth.
The efficiency of the CPU for this computation is around 3%.

<!-- Slide number: 7 -->
# Question
What GPUs were originally designed to do?
Parallel and Distributed Computing – Spring 2025
7

<!-- Slide number: 8 -->
# GPU were designed for..
3D Rendering
computing how each triangle in 3D mesh contributes to appearance of each pixel in the image
in realtime

![A cartoon character running on a hill AI-generated content may be incorrect.](Picture5.jpg)
Parallel and Distributed Computing – Spring 2025
8

<!-- Slide number: 9 -->
# Observation circa 2001-2003
GPUs are very fast processors for performing the same computation (shader programs) in parallel on large collections of data (streams of vertices, fragments, and pixels)
Wait a minute! That sounds a lot like data-parallelism to me!
data-parallelism from exotic supercomputers in the 90s.
And every year GPUs are getting faster because more transistors = more parallelism
Parallel and Distributed Computing – Spring 2025
9

<!-- Slide number: 10 -->
# Hack! early GPU-based scientific computation
Say you want to run a function on all elements of a 512x512 array
Set output image size to be array size (512 x 512) Render two triangles that exactly cover screen
Render two triangles that exactly cover screen
We now can use the GPU like a data-parallel programming system.
Fragment shader function is mapped over 512 x 512 element collection.
Hack!

![](Picture5.jpg)
Parallel and Distributed Computing – Spring 2025
10

<!-- Slide number: 11 -->
# Observation Circa 2002-2004
GPGPU = “general purpose” computation on GPUs
Brook stream programming language
Stanford graphics lab research project
Abstract GPU hardware as data-parallel processor
Brook compiler translated generic stream program into graphics commands (such as drawTriangles) and a set of graphics shader programs that could be run on GPUs of the day.
Parallel and Distributed Computing – Spring 2025
11

<!-- Slide number: 12 -->
# Review: how to run code on a CPU
Lets say a user wants to run a program on a multi-core CPU…
OS loads program text into memory
OS selects CPU execution context
OS interrupts processor, prepares execution context (sets contents of registers, program counter, etc. to prepare execution context)
Go!
Processor begins executing instructions from within the environment maintained in the execution context.
Parallel and Distributed Computing – Spring 2025
12

<!-- Slide number: 13 -->
# How to run code on a GPU (prior to 2007)

![A diagram of a process AI-generated content may be incorrect.](Picture5.jpg)
Let’s say a user wants to draw a picture using a GPU
 Application (via graphics driver) provides GPU shader program binaries
Application sets graphics pipeline parameters (e.g., output image size)
Application provides GPU a buffer of vertices
Application sends GPU a “draw” command: drawPrimitives(vertex_buffer)
Parallel and Distributed Computing – Spring 2025
13

<!-- Slide number: 14 -->
# NVIDIA Tesla architecture (2007)
First alternative, non-graphics-specific (“compute mode”) interface to GPU hardware
Let’s say a user wants to run a non-graphics program on the GPU’s programmable cores…
Application can allocate buffers in GPU memory and copy data to/from buffers
Application (via graphics driver) provides GPU a single kernel program binary
Application tells GPU to run the kernel in an SPMD fashion (“run N instances of this kernel”): launch(myKernel, N)
Parallel and Distributed Computing – Spring 2025
14

<!-- Slide number: 15 -->
# CUDA programming language
Introduced in 2007 with NVIDIA Tesla architecture
“C-like” language to express programs that run on GPUs using the compute-mode hardware interface
Relatively low-level: CUDA’s abstractions closely match the capabilities/performance characteristics of modern GPUs

design goal: maintain low abstraction distance
Parallel and Distributed Computing – Spring 2025
15

<!-- Slide number: 16 -->
# CUDA programs consist of a hierarchy of concurrent threads
Thread IDs can be up to 3-dimensional (2D example below)
Multi-dimensional thread ids are convenient for problems that are naturally N-D

![A screenshot of a computer program AI-generated content may be incorrect.](Picture5.jpg)
Parallel and Distributed Computing – Spring 2025
16

<!-- Slide number: 17 -->
# Basic CUDA Syntax

![](ContentPlaceholder5.jpg)
Parallel and Distributed Computing – Spring 2025
17

<!-- Slide number: 18 -->
# CUDA Threads
A CUDA thread presents a similar abstraction as a pthread in that both correspond to logical threads of control, but the implementation of a CUDA thread is very different

Number of kernel invocations is not determined by size of data collection (a kernel launch is not speci!ed by map(kernel, collection) as was the case with graphics shader programming)
Parallel and Distributed Computing – Spring 2025
18

<!-- Slide number: 19 -->
# Clear separation of host and device code
Separation of execution into host and device code is performed statically by the programmer

![A screenshot of a computer code AI-generated content may be incorrect.](Picture5.jpg)
Parallel and Distributed Computing – Spring 2025
19

<!-- Slide number: 20 -->
# CUDA execution model

![](ContentPlaceholder5.jpg)
Parallel and Distributed Computing – Spring 2025
20

<!-- Slide number: 21 -->
# CUDA device memory model

![](ContentPlaceholder5.jpg)
Parallel and Distributed Computing – Spring 2025
21

<!-- Slide number: 22 -->
# Heterogeneous Computing
Terminology:
Host  The CPU and its memory (host memory)
Device  The GPU and its memory (device memory)

![A close-up of a computer component AI-generated content may be incorrect.](Picture5.jpg)
Parallel and Distributed Computing – Spring 2025
22

<!-- Slide number: 23 -->
# Heterogeneous Computing

![A screenshot of a computer AI-generated content may be incorrect.](ContentPlaceholder5.jpg)
Parallel and Distributed Computing – Spring 2025
23

<!-- Slide number: 24 -->
# Simple Process Flow
Copy input data from CPU memory to GPU memory

![A diagram of a computer program AI-generated content may be incorrect.](Picture5.jpg)
Parallel and Distributed Computing – Spring 2025
24

<!-- Slide number: 25 -->
# Simple Process Flow
Load GPU program and execute, caching data on chip for performance

![A diagram of a computer program AI-generated content may be incorrect.](Picture5.jpg)
Parallel and Distributed Computing – Spring 2025
25

<!-- Slide number: 26 -->
# Simple Process Flow
Copy results from GPU memory to CPU memory

![](Picture5.jpg)
Parallel and Distributed Computing – Spring 2025
26

<!-- Slide number: 27 -->
# Hello, World
int main(void) {
  printf("Hello World!\n");
  return 0;
  }
Standard C that runs on the host
NVIDIA compiler (nvcc) can be used to compile programs with no device code
Output:
 $ nvcc hello_world.cu
 $ a.out
 Hello World!

Parallel and Distributed Computing – Spring 2025
27

<!-- Slide number: 28 -->
# Hello, World with Device Code
 __global__ void mykernel(void) {
  }
  int main(void) {
   mykernel<<<1,1>>>();
   printf("Hello World!\n");
   return 0;
  }

mykernel() does nothing, for now.

Parallel and Distributed Computing – Spring 2025
28

<!-- Slide number: 29 -->
# Hello, World with Device Code
CUDA C/C++ keyword __global__ indicates a function that:
Runs on the device
Is called from host code

nvcc separates source code into host and device components
Device functions (e.g. mykernel()) processed by NVIDIA compiler
Host functions (e.g. main()) processed by standard host compiler: gcc, cl.exe

Parallel and Distributed Computing – Spring 2025
29

<!-- Slide number: 30 -->
# Hello, World with Device Code
 mykernel<<<1,1>>>();

Triple angle brackets mark a call from host code to device code
Also called a “kernel launch”

That’s all that is required to execute a function on the GPU!

Parallel and Distributed Computing – Spring 2025
30

<!-- Slide number: 31 -->
# Addition on the Device
A simple kernel to add two integers
  __global__ void add(int *a, int *b, int *c) {
   *c = *a + *b;
  }

As before __global__ is a CUDA C/C++ keyword meaning
 –add() will execute on the device
 –add() will be called from the host

Parallel and Distributed Computing – Spring 2025
31

<!-- Slide number: 32 -->
# Addition on the Device
•Note that we use pointers for the variables
  __global__ void add(int *a, int *b, int *c) {
  *c = *a + *b;
  }
add() runs on the device, so a, b and c must point to device memory

•We need to allocate memory on the GPU

Parallel and Distributed Computing – Spring 2025
32

<!-- Slide number: 33 -->
# Memory Management
•Host and device memory are separate entities
Device pointers point to GPU memory
May be passed to/from host code
May not be dereferenced in host code
Host pointers point to CPU memory
May be passed to/from device code
May not be dereferenced in device code
Simple CUDA API for handling device memory
cudaMalloc(), cudaFree(), cudaMemcpy()
Similar to the C equivalents malloc(), free(), memcpy()

Parallel and Distributed Computing – Spring 2025
33

<!-- Slide number: 34 -->
# Addition Code
int main(void) {
  int a, b, c;             // host copies of a, b, c
  int *d_a, *d_b, *d_c;       // device copies of a, b, c
  int size = sizeof(int);

  // Allocate space for device copies of a, b, c
  cudaMalloc((void **)&d_a, size);
  cudaMalloc((void **)&d_b, size);
  cudaMalloc((void **)&d_c, size);

  // Setup input values
  a = 2;
  b = 7;

// Copy inputs to device
  cudaMemcpy(d_a, &a, size, cudaMemcpyHostToDevice);
  cudaMemcpy(d_b, &b, size, cudaMemcpyHostToDevice);

  // Launch add() kernel on GPU
  add<<<1,1>>>(d_a, d_b, d_c);

  // Copy result back to host
  cudaMemcpy(&c, d_c, size, cudaMemcpyDeviceToHost);

  // Cleanup
  cudaFree(d_a); cudaFree(d_b); cudaFree(d_c);
  return 0;
}

Parallel and Distributed Computing – Spring 2025
34

<!-- Slide number: 35 -->
# Moving to Parallel
GPU computing is about massive parallelism
So how do we run code in parallel on the device?

		add<<< 1, 1 >>>();

		add<<< N, 1 >>>();

Instead of executing add() once, execute N times in parallel
Parallel and Distributed Computing – Spring 2025
35

<!-- Slide number: 36 -->
# Vector Addition on the Device
With add() running in parallel we can do vector addition

Terminology: each parallel invocation of add() is referred to as a block
The set of blocks is referred to as a grid
Each invocation can refer to its block index using blockIdx.x

__global__ void add(int *a, int *b, int *c) {
	c[blockIdx.x]=a[blockIdx.x] + b[blockIdx.x];
}

By using blockIdx.x to index into the array, each block handles a different index
Parallel and Distributed Computing – Spring 2025
36

<!-- Slide number: 37 -->
# Vector Addition on the Device
__global__ void add(int *a, int *b, int *c) {
	c[blockIdx.x] = a[blockIdx.x] + b[blockIdx.x];
}

On the device, each block can execute in parallel:

Block 2
Block 3
Block 0
Block 1
c[2]  = a[2] + b[2];
c[3]  = a[3] + b[3];
c[0]  = a[0] + b[0];
c[1]  = a[1] + b[1];
Parallel and Distributed Computing – Spring 2025
37

<!-- Slide number: 38 -->
# Modified main()
#define N 512
    int main(void) {
	int *a, *b, *c;	// host copies of a, b, c
	int *d_a, *d_b, *d_c;	// device copies of a, b, c
	int size = N * sizeof(int);

	// Alloc space for device copies of a, b, c
	cudaMalloc((void **)&d_a, size);
	cudaMalloc((void **)&d_b, size);
	cudaMalloc((void **)&d_c, size);

	// Alloc space for host copies of a, b, c and setup input values
	a = (int *)malloc(size); random_ints(a, N);
	b = (int *)malloc(size); random_ints(b, N);
	c = (int *)malloc(size);
        // Copy inputs to device
        cudaMemcpy(d_a, a, size, cudaMemcpyHostToDevice);
        cudaMemcpy(d_b, b, size, cudaMemcpyHostToDevice);

        // Launch add() kernel on GPU with N blocks
        add<<<N,1>>>(d_a, d_b, d_c);

        // Copy result back to host
        cudaMemcpy(c, d_c, size, cudaMemcpyDeviceToHost);

        // Cleanup
        free(a); free(b); free(c);
        cudaFree(d_a); cudaFree(d_b); cudaFree(d_c);
        return 0;
    }
Parallel and Distributed Computing – Spring 2025
38

<!-- Slide number: 39 -->
# CUDA Threads
Terminology: a block can be split into parallel threads

Let’s change add() to use parallel threads instead of parallel blocks

__global__ void add(int *a, int *b, int *c) {
    c[threadIdx.x] = a[threadIdx.x] + b[threadIdx.x];
}

We use threadIdx.x instead of blockIdx.x
Parallel and Distributed Computing – Spring 2025
39

<!-- Slide number: 40 -->
# Modified main()
 #define N 512
    int main(void) {
        int *a, *b, *c;		// host copies of a, b, c
        int *d_a, *d_b, *d_c;		// device copies of a, b, c
        int size = N * sizeof(int);

        // Alloc space for device copies of a, b, c
        cudaMalloc((void **)&d_a, size);
        cudaMalloc((void **)&d_b, size);
        cudaMalloc((void **)&d_c, size);

        // Alloc space for host copies of a, b, c and setup input values
        a = (int *)malloc(size); random_ints(a, N);
        b = (int *)malloc(size); random_ints(b, N);
        c = (int *)malloc(size);

        // Copy inputs to device
        cudaMemcpy(d_a, a, size, cudaMemcpyHostToDevice);
        cudaMemcpy(d_b, b, size, cudaMemcpyHostToDevice);

        // Launch add() kernel on GPU with N threads
        add<<<1,N>>>(d_a, d_b, d_c);

        // Copy result back to host
        cudaMemcpy(c, d_c, size, cudaMemcpyDeviceToHost);

        // Cleanup
        free(a); free(b); free(c);
        cudaFree(d_a); cudaFree(d_b); cudaFree(d_c);
        return 0;
    }
Parallel and Distributed Computing – Spring 2025
40

<!-- Slide number: 41 -->
# Combining Blocks and Threads
We’ve seen parallel vector addition using:
Many blocks with one thread each
One block with many threads

Let’s adapt vector addition to use both blocks and threads
Parallel and Distributed Computing – Spring 2025
41

<!-- Slide number: 42 -->
# Indexing Arrays with Blocks and Threads
No longer as simple as using blockIdx.x and threadIdx.x
Consider indexing an array with one element per thread (8 threads/block)

With M threads/block a unique index for each thread is given by:
	int index = threadIdx.x + blockIdx.x * M;
threadIdx.x
threadIdx.x
threadIdx.x
threadIdx.x
5
6
7
0
1
2
3
4
5
6
7
0
1
2
3
4
5
6
7
0
1
2
3
4
1
2
3
4
5
6
7
0

blockIdx.x = 3
blockIdx.x = 2
blockIdx.x = 0
blockIdx.x = 1
Parallel and Distributed Computing – Spring 2025
42

<!-- Slide number: 43 -->
# Indexing Arrays: Example
Which thread will operate on the red element?

13
14
15
16
17
18
19
20
21
22
23
24
1
2
3
4
5
6
7
8
9
10
11
12
25
26
27
28
29
30
31
0

threadIdx.x = 5
M = 8

5
6
7
0
1
2
3
4
5
6
7
0
1
2
3
4
5
6
7
0
1
2
3
4
1
2
3
4
5
6
7
0
blockIdx.x = 2
Parallel and Distributed Computing – Spring 2025
43

<!-- Slide number: 44 -->
# Vector Addition with Blocks and Threads
Use the built-in variable blockDim.x for threads per block
	int index = threadIdx.x + blockIdx.x * blockDim.x;

Combined version of add() to use parallel threads and parallel blocks

__global__ void add(int *a, int *b, int *c) {
    int index = threadIdx.x + blockIdx.x * blockDim.x;
    c[index] = a[index] + b[index];
}

Parallel and Distributed Computing – Spring 2025
44

<!-- Slide number: 45 -->
# Question
What changes need to be made in the main program?
Parallel and Distributed Computing – Spring 2025
45

<!-- Slide number: 46 -->
# Modified main()
    #define N (2048*2048)
    #define THREADS_PER_BLOCK 512
    int main(void) {
        int *a, *b, *c;		// host copies of a, b, c
        int *d_a, *d_b, *d_c;		// device copies of a, b, c
        int size = N * sizeof(int);

        // Alloc space for device copies of a, b, c
        cudaMalloc((void **)&d_a, size);
        cudaMalloc((void **)&d_b, size);
        cudaMalloc((void **)&d_c, size);

        // Alloc space for host copies of a, b, c and setup input values
        a = (int *)malloc(size); random_ints(a, N);
        b = (int *)malloc(size); random_ints(b, N);
        c = (int *)malloc(size);

        // Copy inputs to device
        cudaMemcpy(d_a, a, size, cudaMemcpyHostToDevice);
        cudaMemcpy(d_b, b, size, cudaMemcpyHostToDevice);

        // Launch add() kernel on GPU
        add<<<N/THREADS_PER_BLOCK,THREADS_PER_BLOCK>>>(d_a, d_b, d_c);

        // Copy result back to host
        cudaMemcpy(c, d_c, size, cudaMemcpyDeviceToHost);

        // Cleanup
        free(a); free(b); free(c);
        cudaFree(d_a); cudaFree(d_b); cudaFree(d_c);
        return 0;
    }
Parallel and Distributed Computing – Spring 2025
46

<!-- Slide number: 47 -->
# Question
Do you see any issue with this approach?
Parallel and Distributed Computing – Spring 2025
47

<!-- Slide number: 48 -->
# Handling Arbitrary Vector Sizes
Typical problems are not friendly multiples of blockDim.x

Avoid accessing beyond the end of the arrays:

__global__ void add(int *a, int *b, int *c, int n) {
    int index = threadIdx.x + blockIdx.x * blockDim.x;
    if (index < n)
        c[index] = a[index] + b[index];
}

Update the kernel launch:
	add<<<(N + M-1) / M,M>>>(d_a, d_b, d_c, N);

Parallel and Distributed Computing – Spring 2025
48

<!-- Slide number: 49 -->
# Why Bother with Threads?
Threads seem unnecessary
They add a level of complexity
What do we gain?

Unlike parallel blocks, threads have mechanisms to:
Communicate
Synchronize
Parallel and Distributed Computing – Spring 2025
49

<!-- Slide number: 50 -->
# 1D Stencil
Consider applying a 1D stencil to a 1D array of elements
Each output element is the sum of input elements within a radius

If radius is 3, then each output element is the sum of 7 input elements:

radius
radius
Parallel and Distributed Computing – Spring 2025
50

<!-- Slide number: 51 -->
# Implementing Within a Block
Each thread processes one output element
blockDim.x elements per block

Input elements are read several times
With radius 3, each input element is read seven times

Parallel and Distributed Computing – Spring 2025
51

<!-- Slide number: 52 -->
# Sharing Data Between Threads
Terminology: within a block, threads share data via shared memory

Extremely fast on-chip memory, user-managed

Declare using __shared__, allocated per block

Data is not visible to threads in other blocks
Parallel and Distributed Computing – Spring 2025
52

<!-- Slide number: 53 -->
# Implementing With Shared Memory
Cache data in shared memory
Read (blockDim.x + 2 * radius) input elements from global memory to shared memory
Compute blockDim.x output elements
Write blockDim.x output elements to global memory

Each block needs a halo of radius elements at each boundary

halo on right
halo on left

blockDim.x output elements
Parallel and Distributed Computing – Spring 2025
53

<!-- Slide number: 54 -->
# Stencil Kernel (ignore edge cases)
__global__ void stencil_1d(int *in, int *out) {
  __shared__ int temp[BLOCK_SIZE + 2 * RADIUS];
  int gindex = threadIdx.x + blockIdx.x * blockDim.x;
  int lindex = threadIdx.x + RADIUS;

  // Read input elements into shared memory
  temp[lindex] = in[gindex];
  if (threadIdx.x < RADIUS) {
    temp[lindex - RADIUS] = in[gindex - RADIUS];
    temp[lindex + BLOCK_SIZE] =  in[gindex + BLOCK_SIZE];
  }
 // Apply the stencil
  int result = 0;
  for (int offset = -RADIUS ; offset <= RADIUS ; offset++)
    result += temp[lindex + offset];

  // Store the result
  out[gindex] = result;
}

Parallel and Distributed Computing – Spring 2025
54

<!-- Slide number: 55 -->
# Question
What is the problem with this code?
Parallel and Distributed Computing – Spring 2025
55

<!-- Slide number: 56 -->
# Data Race!
The stencil example will not work…

Suppose thread 15 reads the halo before thread 0 has fetched it…

 temp[lindex] = in[gindex];
  if (threadIdx.x < RADIUS) {
    temp[lindex – RADIUS = in[gindex – RADIUS];
    temp[lindex + BLOCK_SIZE] = in[gindex + BLOCK_SIZE];
  }

  int result = 0;
  result += temp[lindex + 1];
Store at temp[18]

Skipped, threadIdx > RADIUS
Load from temp[19]

Parallel and Distributed Computing – Spring 2025
56

<!-- Slide number: 57 -->
# __syncthreads()
void __syncthreads();

Synchronizes all threads within a block
Used to prevent RAW / WAR / WAW hazards

All threads must reach the barrier
In conditional code, the condition must be uniform across the block
Parallel and Distributed Computing – Spring 2025
57

<!-- Slide number: 58 -->
# Stencil Kernel
__global__ void stencil_1d(int *in, int *out) {

    __shared__ int temp[BLOCK_SIZE + 2 * RADIUS];
    int gindex = threadIdx.x + blockIdx.x * blockDim.x;
    int lindex = threadIdx.x + radius;

    // Read input elements into shared memory
    temp[lindex] = in[gindex];
    if (threadIdx.x < RADIUS) {
        temp[lindex – RADIUS] = in[gindex – RADIUS];
        temp[lindex + BLOCK_SIZE] = in[gindex + BLOCK_SIZE];
    }

    // Synchronize (ensure all the data is available)
    __syncthreads();

    // Apply the stencil
    int result = 0;
    for (int offset = -RADIUS ; offset <= RADIUS ; offset++)
        result += temp[lindex + offset];

    // Store the result
    out[gindex] = result;
}
Parallel and Distributed Computing – Spring 2025
58