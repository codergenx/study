Lecture \# 2

Caches/C-languge intro /Flynn Taxonomy /Multi threading By: Muhammad Zain Uddin

email: zuddin@iba.edu.pk

M. ZAIN UDDIN

1





Whatarecaches? 

▪ **Acacheisahardwareimplementationdetailthatdoesnotimpacttheoutputofaprogram,onlyitsperformance**

▪ **Cacheison-chipstoragethatmaintainsacopyofasubsetofthevaluesinmemory**

▪ **Ifanaddressisstored“inthecache”theprocessorcanload/storetothisaddressmorequicklythanifthedataresidesonlyinDRAM**

▪ **Cachesoperateatthegranularityof“cachelines”. **

**Inthefigure,thecache:**

**Implementationofmemoryabstraction**

**Address **

**Value**

**- Hasacapacityof2lines**

**0x0**

**16**

**- Eachlineholds4bytesofdata**

**0x1 **

**255**

**0x2**

**14**

**Processor**

**0x3**

**0**

**0x4**

**0**

**0x5 **

**0**

**Fetch/ **

**0x6**

**6**

**Decode**

**0x7 **

**0**

**0x8**

**32**

**ALU**

**0x9**

**48**

**\(Execute\)**

**0xA **

**255**

**DataCache**

**Execution **

**0xB**

**255**

**Context**

**Line**

**Valuesin**

**0xC **

**255**

**Address**

**line**

**0xD**

**0**

**0x4**

**0**

**0**

**6**

**0**

**0xE **

**0**

**DRAM**

**0xC**

**255**

**0**

**0**

**0**

**0xF**

**0**

**0x10**

**128**

**. **

**. **

**. **

**. **

**. **

**. **

**0x1F**

**0**





Cacheexample1

**Address **

**Cachestate **

**Cacheaction**

**accessed**

**\(after loadiscomplete\)**

**Arrayof16bytesinmemory **

**0x0 “coldmiss”,load**

**0x0**

**Address**

**Value**

**0x0 0x1 hit**

**0x0**

**Assume:**

**0x0 16**

**0x2 hit**

**0x0**

**e**

**0**

**0x3 hit**

**0x0**

**n**

**0x1 255**

**Totalcachecapacityof8bytes**

**iL 0x**

**0x2 hit**

**0x0**

**0x2 14**

**Cachewith4-bytecache**

**0x1 hit**

**0x0**

**0x3 0**

**lines \(So2linesfitincache\)**

**0x4 “coldmiss”,load**

**0x0**

**0x4**

**0x4 0**

**0x4 0x1 hit**

**0x0**

**0x4**

**Leastrecentlyused**

**e**

**4**

**0x5**

**n**

**0**

**\(LRU\) replacement**

**iL 0x**

**policy**

**0x6 6**

**Therearetwoformsof“datalocality”inthissequence:** **time**

**0x7 0**

**e**

**Spatiallocality:loadingdatainacacheline“preloads”the** **n**

**8**

**i**

**0x8**

**32**

**L**

**0x**

**dataneededforsubsequentaccessestodiferentaddresses** **0x9**

**48**

**inthesameline,leadingtocachehits**

**e**

**0xA**

**255**

**Temporallocality:repeatedaccessestothesameaddress** **n**

**C**

**iL 0x**

**0xB**

**255**

**resultinhits. **

**0xC**

**255**





Cacheexample2

**Address **

**Cachestate **

**Cacheaction**

**accessed**

**\(after loadiscomplete\)**

**Arrayof16bytesinmemory **

**Address**

**Value**

**0x0 “coldmiss”,load**

**0x0**

**0x0**

**16**

**0x0 0x1 hit**

**0x0**

**Assume:**

**0x2 hit**

**0x0**

**0x1**

**255**

**e**

**0x3 hit**

**n**

**0**

**Totalcachecapacityof8bytes**

**0x0**

**iL 0x**

**0x2**

**14**

**0x4 “coldmiss”,load**

**0x0**

**0x4**

**0x3**

**0**

**Cachewith4-bytecache**

**0x4 0x5 hit**

**0x0**

**0x4**

**lines \(So2linesfitincache\)**

**e**

**0x4**

**0**

**0x6 hit**

**0x0**

**0x4**

**n**

**4**

**i**

**0x7 hit**

**0x0**

**0x4**

**L**

**0x**

**0x5**

**0**

**Leastrecentlyused**

**0x8 “coldmiss”,load0x8\(evict**

**0x8**

**0x4**

**\(LRU\) replacement**

**0x6**

**6**

**0x0\) 0x9 hit**

**policy**

**0x8**

**0x4**

**en 8 0x7**

**0**

**0xA hit**

**0x8**

**0x4**

**iL 0x**

**0xB hit**

**0x8**

**0x4**

**0x8**

**32**

**0xC “coldmiss”,load0xC\(evict**

**0x8**

**0xC**

**0x9**

**48**

**0x4\) 0xD hit**

**0x8**

**0xC**

**0xA**

**255**

**0xE hit**

**0x8**

**0xC**

**time**

**0xF hit**

**0x8**

**0xC**

**0xB**

**255**

**e**

**C**

**0x0**

**n**

**“capacitymiss”,load0x0\(evict0x8\) 0x0**

**0xC**

**iL 0x**

**0xC**

**255**

**0xD**

**0**

Cachesreducelengthofstals 

\(reducememoryaccess latency\)

▪ **Processorsrunefficientlywhentheyaccessdatathatisresidentincaches**

▪ **Cachesreducememoryaccesslatencywhenprocessorsaccessesdatathattheyhave** **recentlyaccessed\!\***

**\*Cachesalsoprovidehighbandwidthdatatransfer**





Theimplementationofthelinearmemoryaddressspaceabstraction onamodern computeriscomplex

Theinstruction“loadthevaluestoredataddressXintoregisterR0”mightinvolvea complexsequenceof operationsbymultipledatacachesandaccess toDRAM

**Processor**

**L1cache **

**\(32KB\)**

**L3**

**DRAM **

**L2cache **

**\(256 KB\)**

**cache **

**\(64 GB\)**

**\(20MB\)**

**Commonorganization:hierarchyof**

**caches: Level1\(L1\),level2\(L2\),level3**

**\(L3\)**

**Smalercapacitycachesnearprocessor→lowerlatency** **Largercapacitycachesfartheraway→largerlatency**

Dataaccess times

\(KabyLakeCPU\)

**Latency\(numberofcyclesat4GHz\)**

**Data in L1 cache**

**4**

**Data in L2 cache**

**12**

**DatainL3cache**

**38**

**DatainDRAM\(bestcase\)**

**~248**



Now lets get back to basic understanding 

of C

**int main\(int argc, char\*\* argv\) **

**\{**

**int x = 1; **

**for \(int i=0; i<10; i\+\+\) **

**\{ x = x \+ x; **

**\}**

**printf\(“%d\\n”, x\); **

**return 0; **

**\}**

M. ZAIN UDDIN

8



But what exactly does this code does, 

**int main\(int argc, char\*\* argv\) \{**

**int x = 1; **

? 

? 

? 

**for \(int i=0; i<10; i\+\+\) \{ **

**x = x \+ x; **

? 

**\}**

**printf\(“%d\\n”, x\); **

**return 0; **

**\}**

M. ZAIN UDDIN

9



Introduction to C \(1/2\)

Kernighan and Ritchie

◦ *C is not a “very high-level” language, nor a “big” one, and is not specialized* *to any particular area of application. But its absence of restrictions and its* *generality make it more convenient and effective for many tasks than* *supposedly more powerful languages. *

Enabled first operating system not written in assembly language\! 

◦ UNIX - A portable OS\! 

Introduction to C \(2/2\)

Why C? 

◦ We can write programs that allow us to exploit underlying features of the architecture

◦ memory management, special instructions, parallelism C and derivatives \(C\+\+/Obj-C/C\#\) still one of the most popular programming languages after >40 years\! 

If you are starting a new project where performance matters use either Go or Rust

◦ Rust, “C-but-safe”: By the time your C is \(theoretically\) correct w/all necessary checks it should be no faster than Rust

◦ Go, “Concurrency”: Practical concurrent programming to take advantage of modern multi-core microprocessors





Compilation: Overview

C compilers map C programs directly into 

architecture-specific machine code \(string of 1s and 0s\)

◦ Unlike Java, which converts to architecture-independent bytecode that may then be compiled by a just-in-time compiler \(JIT\)

◦ Unlike Python environments, which converts to a byte code at runtime

◦ These differ mainly in exactly when your program is converted to low-level machine instructions \(“levels of interpretation”\)

For C, generally a two part process of compiling .c files to .o files, then linking the .o files into executables; 

◦ Assembling is also done \(but is hidden, i.e., done automatically, by default\); we’ll talk about that later





C Compilation Simplified Overview \(more later\) **foo.c**

bar.c

C source files \(text\)

**Compiler**

**Compiler**

Compiler/assembler 

combined here

foo.o

bar.o

Machine code object files

Pre-built object 

**Linker**

lib.o

file libraries

a.out

Machine code executable file





C vs. Java \(1/3\)

**C**

**Java**

**Type of Language**

Function Oriented 

Object Oriented 

**Programming Unit **

Function 

Class = Abstract Data Type 

**Compilation gcc hello.c **creates **javac Hello.java **creates Java virtual machine language code 

machine language bytecode 

**Execution **

**a.out **loads and 

executes program 

**java Hello **interprets bytecodes 

**\#include <stdio.h> public class HelloWorld \{**

**int main\(void\)**

**public static void **

**hello, world \{**

**main\(String\[\] args\) \{ **

**printf\("Hi\\n"\); **

**System.out.println\("Hi"\); **

**return 0; **

**\} \} **

**\}**

**Storage **Manual \(**malloc**, **free**\) New allocates & initializes, 

Automatic \(garbage col ection\) frees

From http://www.cs.princeton.edu/introcs/faq/c2java.html

C vs. Java \(2/3\)

**C**

**Java**

**Comments \(C99 **

**same as Java\)**

**/\* … \*/**

**/\* … \*/ **or **// **… end of line 

**Constants \#define**, **const**

**final**

**Preprocessor**

Yes

No

**Variable **At beginning of a 

**declaration \(C99 **

**same as Java\)**

block

Before you use it 

**Variable naming **

**conventions sum\_of\_squares**

**sumOfSquares**

**\#include **

**Accessing a library**

**import java.io.File; **

**<stdio.h> **

From http://www.cs.princeton.edu/introcs/faq/c2java.html

C vs. Java \(3/3\) …operators nearly identical

arithmetic: **\+, -, \*, /, %**

assignment: **=**

augmented assignment: **\+=, -=, \*=, /=, %=, &=, |=, ^=, <<=, >>=**

bitwise logic: **~, &, |, **

bitwise shifts: **<<, >> **

boolean logic: **\!, &&, ||**

equality testing: **==, \!=**

subexpression grouping: **\(\)**

order relations: **<, <=, >, >=**

increment and decrement: **\+\+ **and **--**

member selection: **. **, **-> **

◦

Slightly different than Java because there are both structures and pointers to structures, more later conditional evaluation: **? :**

C Syntax: main

To get the **main **function to accept arguments, use this:

◦ **int main \(int argc, char \*argv\[\]\)**

What does this mean? 

◦ **argc **will contain the number of strings on the command line \(the executable counts as one, plus one for each argument\). Here **argc **is 2:

◦ **unix% sort myFile**

◦ **argv **is a pointer to an array containing the arguments as strings \(more on pointers later\). 





M. ZAIN UDDIN

20



Char

M. ZAIN UDDIN

21

int main\(int argc, char\*\* argv\) **argc stands for "argument count," and argv stands for "argument vector." These parameters** **are commonly used in C and C\+\+ programs to handle command-line arguments when the** **program is executed from the command line. **

argc: It is an integer that represents the number of command-line arguments passed to the program, including the program name itself. The value of argc is at least 1, as it includes the program name. 

argv: It is an array of strings \(char\*\*\), where each element is a pointer to a null-terminated string representing a command-line argument. argv\[0\] is the program name, and subsequent elements contain the additional arguments. 

M. ZAIN UDDIN

22





Another example

\#include <stdio.h> 

Command after saving the file:

int main\(int argc, char\*\* argv\) \{

./myprogram arg1 arg2 arg3

// Print the program name \(first argument\)

printf\("Program Name: %s\\n", argv\[0\]\); 

// Print the count of command-line arguments printf\("Argument Count: %d\\n", argc\); 

// Print each command-line argument

printf\("Arguments:\\n"\); 

for \(int i = 0; i < argc; \+\+i\) \{

printf\("argv\[%d\]: %s\\n", i, argv\[i\]\); 

\}

return 0; 

\}

M. ZAIN UDDIN

23

M. ZAIN UDDIN

23

Output will be

**Program Name: ./myprogram**

**Argument Count: 4**

**Arguments:**

**argv\[0\]: ./myprogram**

**argv\[1\]: arg1**

**argv\[2\]: arg2**

**argv\[3\]: arg3**

M. ZAIN UDDIN

24

But why did we use “char\*\* argv” 

This is alternative of “**\(char argv\[\]\[MAX\_LENGTH\]\)” so,** **argv as an Array of Strings, **

**char\*\* for Strings, **

**argv as an Array of Pointers, **

M. ZAIN UDDIN

25

Advantage of pointer

Using char\*\* for argv allows for flexibility. Each argv\[i\] can point to a different string of varying lengths. This is in contrast to using a two-dimensional array \(char argv\[\]\[MAX\_LENGTH\]\), where all strings would need to have the same fixed size. 

By using pointers, only the addresses of strings are stored in memory, not the actual string contents. This is memory-efficient, especially when dealing with a large number of arguments or long strings. 

M. ZAIN UDDIN

26



Understanding Different Flavors of 

Parallelism

•SISD:

• Single instruction stream, single data 

stream. 

• Traditional single-core CPUs fall under this category. 

•SIMD:

• Single instruction stream, multiple data 

streams. 

• Vector processors and GPUs excel at this 

type of parallelism. 

•MIMD:

• Multiple instruction streams, multiple data streams. 

• Most parallel and distributed systems 

belong to this category. 

Source: https://media.geeksforgeeks.org/wp-content/uploads/cao.png M. ZAIN UDDIN

27





Dive Deeper into MIMD Architectures

•Focus: Shared memory vs. distributed memory MIMD systems. 

•Shared memory: Processors share a common memory space for direct data access. 

•Distributed memory: Each processor has its own local memory, requiring message passing for communication. 

M. ZAIN UDDIN

29



exampleprogram

**void sinx\(int N, int terms, float\* x, float\* y\)** **Compute**sin\( *x*\) **usingTaylorexpansion:**

**\{**

**for \(int i=0; i<N; i\+\+\)**

sin\( *x*\) = *x *- *x* 3/3\! \+ *x* 5/5\! - *x* 7/7\! \+ ... 

**\{**

**float value = x\[i\]; **

**foreachelementofanarrayofNfloating-pointnumbers** **float numer = x\[i\] \* x\[i\] \* x\[i\]; **

**int denom = 6; **

**// 3\! **

**int sign = -1; **

**x\[0\]**

**x\[1\]**

**…**

**x\[N-2\] x\[N-1\]**

**for \(int j=1; j<=terms; j\+\+\)**

**\{**

**value \+= sign \* numer / denom; **

**numer \*= x\[i\] \* x\[i\]; **

**denom \*= \(2\*j\+2\) \* \(2\*j\+3\); **

**sign \*= -1; **

**y\[0\]**

**y\[1\]**

**…**

**y\[N-2\] y\[N-1\]**

**\}**

**y\[i\] = value; **

**\}**

**\}**





Compileprogram

**Compiledinstructionstream **

**\(scalarinstructions\)**

**void sinx\(int N, **

**int terms, float\* x, float\* y\)**

**\{**

**x\[i\]**

**for \(int**

**i<N; i\+\+\)**

**i=0; **

**\{float value = x\[i\]; **

**float numer = x\[i\] \* x\[i\] \* x\[i\]; **

**int denom = 6; **

**// 3\! **

**ld**

**r0, addr\[r1\]**

**int sign = -1; **

**mul**

**r1, r0, r0**

**mul**

**r1, r1, r0**

**... **

**for**

**\(int**

**j=1; **

**j<=terms; **

**j\+\+\)**

**compiler**

**... **

**\{**

**... **

**value**

**\+= sign \* numer / denom; **

**... **

**numer**

**\*= x\[i\] \* x\[i\]; **

**... **

**denom**

**\*= \(2\*j\+2\) \* \(2\*j\+3\); **

**... **

**sign \*= -1; **

**st**

**addr\[r2\], r0**

**\}**

**y\[i\] = value; **

y**\[i\]**

**\}**

**\}**





Executeprogram

Myvery simpleprocessor:executesoneinstructionperclock **x\[i\]**

**Fetch/ **

**Decode**

**ld**

**r0, addr\[r1\]**

**mul**

**r1, r0, r0**

**Execution Unit **

**mul**

**r1, r1, r0**

**\(ALU\)**

**... **

**... **

**... **

**Execution **

**... **

**Context**

**... **

**... **

**st**

**addr\[r2\], r0**

y**\[i\]**





Superscalar processor

**The processor shown here can decode and execute two instructions per clock** **\(if independent instructions exist in an instruction stream\)** **x\[i\]**

**Out-of-order control logic**

**Fetch/ **

**Fetch/ **

**Decode **

**Decode **

**1**

**2**

**ld**

**r0, addr\[r1\]**

**mul**

**r1, r0, r0**

**Exec **

**mul**

**r1, r1, r0**

**Exec **

**... **

**1**

**2**

**... **

**... **

**... **

**Execution **

**... **

**Context**

**... **

**st**

**addr\[r2\], r0**

y**\[i\]**

**Note:NoILPexistsinthisregionoftheprogram**





Pre multi-core era processor

Majority of chip transistors used to perform operations that help make a single instruction stream run fast

**Fetch/ **

**Fetch/ **

**Decode**

**Decode**

**Data cache **

**Exec Unit **

**\(abig one\)**

**Exec Unit **

**\(ALU\)**

**\(ALU\)**

**Execution **

**Out-of-order control logic**

**Context**

**Fancybranch predictor**

**Memorypre-fetcher**

**More transistors = larger cache, smarter out-of-order logic, smarter branch predictor, etc. **





Multi-core era processor

**Fetch/ **

**Idea \#1:**

**Decode**

**Rather than use transistors to **

**Exec Unit **

**increase sophistication of processor **

**\(ALU\)**

**logic that accelerates a single **

**instruction stream**

**Execution **

**Context**

**\(e.g., out-of-order and speculative **

**operations\)**

**Use increasing transistor count to **

**add more cores to the processor**

**zain uddin**





Two cores: compute two elements in paral el **x\[i\]**

**x\[j\]**

**Fetch/ **

**Fetch/ **

**Decode**

**Decode**

**ld**

**r0, addr\[r1\]**

**Exec **

**Exec **

**ld**

**r0, addr\[r1\]**

**mul**

**r1, r0, r0**

**mul**

**r1, r0, r0**

**mul**

**r1, r1, r0**

**\(ALU\)**

**\(ALU\)**

**mul**

**r1, r1, r0**

**... **

**... **

**... **

**... **

**... **

**... **

**Execution **

**Execution **

**... **

**... **

**... **

**Context**

**Context**

**... **

**... **

**... **

**st**

**addr\[r2\], r0**

**st**

**addr\[r2\], r0**

**x\[i\]**

**x\[j\]**

**Simpler cores: each core may be slower at running a single instruction** **stream than our original “fancy” core \(e.g., 25% slower\)** **But there are now two cores: 2 ×0.75 = 1.5\(potential for speedup\!\)**





**But our program expresses no parallelism** **void sinx\(int N, int terms, float\* x, float\***

**y\)**

**\{**

**for \(int i=0; i<N; i\+\+\)**

**This C program will compile to an instruction **

**\{**

**stream that runs as one thread on one **

**float value = x\[i\]; **

**float numer = x\[i\] \* x\[i\] \* x\[i\]; **

**processor core. **

**int denom = 6; // 3\! **

**int sign = -1; **

**If each of the simpler processor cores was 25% **

**for**

**\(int**

**j=1; **

**j<=terms; **

**j\+\+\)**

**slower than the original single complicated one, **

**\{**

**our program now runs 25% slower than before. **

**value**

**\+=**

**sign \* numer / denom; **

**numer**

**\*=**

**x\[i\] \* x\[i\]; **

\! 

**denom**

**\*=**

**\(2\*j\+2\) \* \(2\*j\+3\); **

**sign \*= -1; **

**\}**

**y\[i\] = value; **

**\}**

**\}**





**Example: expressing parallelism using C\+\+ threads** **typedef struct \{ **

**void sinx\(int N, int terms, float\* x, float\***

**y\)**

**int N; **

**int terms; **

**\{**

**float\* x; **

**for \(int i=0; i<N; i\+\+\)**

**float\* y; **

**\{**

**float value = x\[i\]; **

**\} my\_args; **

**float numer = x\[i\] \* x\[i\] \* **

**x\[i\]; int denom = 6; **

**// 3\! **

**void my\_thread\_func\(my\_args\* args\)**

**int sign = -1; **

**\{**

**sinx\(args->N, args->terms, args->x, args->y\); // do work** **for \(int j=1; j<=terms; j\+\+\)**

**\}**

**\{**

**value \+= sign \* numer / **

**void parallel\_sinx\(int N, int terms, float\* x, float\* y\)** **denom numer \*= x\[i\] \* x\[i\]; **

**\{**

**denom \*= \(2\*j\+2\) \***

**std::thread my\_thread; **

**\(2\*j\+3\); sign \*= -1; **

**my\_args args; **

**\}**

**args.N = N/2; **

**\}**

**args.terms = terms; **

**y\[i\] = value; **

**\}**

**args.x = x; **

**args.y = y; **

**my\_thread = std::thread\(my\_thread\_func, &args\); // launch thread** **sinx\(N - args.N, terms, x \+ args.N, y \+ args.N\); // do work on main** **thread my\_thread.join\(\); **

**// wait for thread to complete**

**\}**



**Data-paralelexpression\(inKayvon’sfictitiousprogramminglanguagewitha“foral”construct\)** **void sinx\(int N, int terms, float\* x, float\* y\)** **In this code, loop iterations are declared **

**\{**

**// declares that loop iterations are independent** **by the programmer to be independent **

**forall \(int i from 0 to N\)**

**\(see the ‘forall’\)**

**\{**

**float value = x\[i\]; **

**float numer = x\[i\] \* x\[i\] \* x\[i\]; **

**With this information, you could **

**int denom = 6; **

**// 3\! **

**imagine how a compiler might **

**int sign = -1; **

**automatical y generate threaded code **

**for \(int j=1; j<=terms; j\+\+\)**

**for you. **

**\{**

**value \+= sign \* numer / denom; **

**numer \*= x\[i\] \* x\[i\]; **

**denom \*= \(2\*j\+2\) \* \(2\*j\+3\); **

**sign \*= -1; **

**\}**

**y\[i\] = value; **

**\}**

**\}**

**ZAIN UDDIN**





Fourcores:computefourelementsinparalel

**Fetch/ **

**Fetch/ **

**Decode**

**Decode**

**Exec **

**Exec **

**\(ALU\)**

**\(ALU\)**

**Execution **

**Execution **

**Context**

**Context**

**Fetch/ **

**Fetch/ **

**Decode**

**Decode**

**Exec **

**Exec **

**\(ALU\)**

**\(ALU\)**

**Execution **

**Execution **

**Context**

**Context**





Sixteen cores: compute sixteen elements in paral el **Sixteencores,sixteensimultaneousinstructionstreams**





Example: multi-core CPU

Intel “Comet Lake” 10th Generation Core i9 10-core CPU \(2020\) **Core1**

**Core2**

**Core3**

**Core4**

**Core5**

**Core6**

**Core7**

**Core8**

**Core9**

**Core10**





Multi-core GPU

**GeForce RTX 4090 \(2022\)**

**144 processing blocks **

**\(called SMs\)**





AppleA15Bionic

**Two“bigcores”\+ four“smal ”cores**

**2“big”CPUcores**

**4“smal ”CPUcores**

**ImageCredit:TechInsightsInc. **



**Data-paralelexpression**

**\(inKayvon’sfictitiousprogramminglanguagewitha“foral”construct\)** **void sinx\(int N, int terms, float\* x, float\* result\)** **Anotherinterestingpropertyofthiscode:**

**\{**

**// declares that loop iterations are independent** **forall \(int i from 0 to N\)**

**Paralelismisacrossiterationsoftheloop. **

**\{**

**float value = x\[i\]; **

**float numer = x\[i\] \* x\[i\] \* x\[i\]; **

**Al theiterationsoftheloopcarryouttheexactsame** **int denom = 6; **

**// 3\! **

**int sign = -1; **

**sequenceofinstructions\(definedbytheloopbody\),** **for**

**\(int**

**j=1; j<=terms; **

**j\+\+\)**

**butondifferentinputdatagivenbyx\[i\]**

**\{**

**value**

**\+=**

**sign \* numer / denom; **

**numer**

**\*=**

**x\[i\] \* x\[i\]; **

**\(theloopbodycomputessine\(x\[i\]\)\)**

**denom**

**\*=**

**\(2\*j\+2\) \* \(2\*j\+3\); **

**sign \*= -1; **

**\}**

**result\[i\] = value; **

**\}**

**\}**





Addexecutionunits\(ALUs\)toincreasecomputecapability **Fetch/ **

**Idea\#2:**

**Decode**

**Amortizecost/complexity ofmanaging**

**ALU 0**

**ALU 1**

**ALU 2**

**ALU 3**

**an instructionstreamacrossmany ALUs**

**ALU 4**

**ALU 5**

**ALU 6**

**ALU 7**

**SIMDprocessing**

**Singleinstruction,multipledata**

**Sameinstructionbroadcasttoal ALUs**

**Execution Context**

**Thisoperationisexecutedinparalelonal ALUs**





**Recal ouroriginalscalarprogram**

**void sinx\(int N, int terms, float\* x, float\* y\)** **Originalcompiledprogram:**

**\{**

**for \(int i=0; i<N; i\+\+\)**

**Processesonearrayelementusingscalarinstructions **

**\{**

**onscalarregisters\(e.g.,32-bitfloats\)**

**float value = x\[i\]; **

**float numer = x\[i\] \* x\[i\] \***

**x\[i\]**

**int denom = 6; // 3\! **

**x\[i\]; **

**int sign = -1; **

**ld**

**r0, addr\[r1\]**

**mul**

**r1, r0, r0**

**for \(int j=1; j<=terms; j\+\+\)**

**mul**

**r1, r1, r0**

**\{**

**... **

**value**

**\+=**

**sign \* numer**

**/ denom; **

**... **

**numer**

**\*=**

**x\[i\] \* x\[i\]; **

**... **

**... **

**denom**

**\*= \(2\*j\+2\)**

**\* \(2\*j\+3\); **

**sign \*= -1; **

**... **

**... **

**\}**

**st**

**addr\[r2\], r0**

**y\[i\] = value; **

**\}**

y**\[i\]**

**\}**



**Vectorprogram\(usingAVXintrinsics\)**

**\#include <immintrin.h> **

**void sinx\(int N, int terms, float\* x, float\* y\)** **Intrinsicdatatypesandfunctions **

**\{**

**float three\_fact = 6; **

**// 3\! **

**availabletoCprogrammers**

**for \(int i=0; i<N; i\+=8\)**

**\{**

**m256 origx = \_mm256\_load\_ps\(&x\[i\]\); **

**Intrinsic functions operate on vectors of** **m256 value = origx; **

**eight32-bitvalues\(e.g.,vectorof8floats\)**

**m256 numer = \_mm256\_mul\_ps\(origx, \_mm256\_mul\_ps\(origx, origx\)\);** **m256 denom = \_mm256\_broadcast\_ss\(&three\_fact\);** **int sign = -1; **

**for \(int j=1; j<=terms; j\+\+\)**

**\{**

**ZAIN UDDIN**

**// value \+= sign \* numer / denom**

**m256 tmp = \_mm256\_div\_ps\(\_mm256\_mul\_ps\(\_mm256\_set1ps\(sign\), numer\), denom\);** **value = \_mm256\_add\_ps\(value, tmp\); **

**numer = \_mm256\_mul\_ps\(numer, \_mm256\_mul\_ps\(origx, origx\)\);** **denom = \_mm256\_mul\_ps\(denom, \_mm256\_broadcast\_ss\(\(2\*j\+2\) \* \(2\*j\+3\)\)\);** **sign \*= -1; **

**\}**

**\_mm256\_store\_ps\(&y\[i\], value\); **

**\}**

**\}**





Vectorprogram\(usingAVXintrinsics\)

**x\[i:i\+8\]**

**\#include <immintrin.h> **

**void sinx\(int N, int terms, float\* x, float\* y\)** **vloadps**

**xmm0, **

**\{**

**addr\[r1\]**

**float three\_fact = 6; **

**// 3\! **

v**mulps**

**xmm1, xmm0, **

**for \(int i=0; i<N; i\+=8\)**

**xmm0**

**\{**

v**mulps**

**xmm1, xmm1, **

**m256 origx = \_mm256\_load\_ps\(&x\[i\]\); **

**xmm0**

**... **

**m256 value = origx; **

**... **

**m256 numer = \_mm256\_mul\_ps\(origx, \_mm256\_mul\_ps\(origx, origx\)\); **

**... **

**m256 denom = \_mm256\_broadcast\_ss\(&three\_fact\); **

**... **

**int sign = -1; **

**... **

**... **

**vstoreps**

**addr\[xmm2\], xmm0**

**for \(int j=1; j<=terms; j\+\+\)**

**\{**

**// value \+= sign \* numer / denom**

**m256 tmp = \_mm256\_div\_ps\(\_mm256\_mul\_ps\(\_mm256\_set1ps\(sign\), numer\), denom\);** **value = \_mm256\_add\_ps\(value, tmp\); **

**y\[i:i\+8\]**

**numer = \_mm256\_mul\_ps\(numer, \_mm256\_mul\_ps\(origx, origx\)\);** **Compiledprogram:**

**denom = \_mm256\_mul\_ps\(denom, \_mm256\_broadcast\_ss\(\(2\*j\+2\) \* \(2\*j\+3\)\)\);** **sign \*= -1; **

**Processeseightarray elements **

**\}**

**simultaneouslyusingvectorinstructions **

**\_mm256\_store\_ps\(&y\[i\], value\); **

**\}**

**on256-bitvectorregisters**

**\}**





16SIMDcores:128elementsinparalel

**16cores,128ALUs,16simultaneousinstructionstreams**

Summary: three different forms of paral el execution

▪ **Superscalar: exploit ILP within an instruction stream. Process different instructions from the** **same instruction stream in parallel \(within a core\)**

- **Parallelism automatically discovered by the hardware during execution**

▪ **SIMD: multiple ALUs controlled by same instruction \(within a core\)**

- **Efficient for data-parallel workloads: amortize control costs over many ALUs**

- **Vectorization done by compiler \(explicit SIMD\) or at runtime by hardware \(implicit SIMD\)**

▪ **Multi-core: use multiple processing cores**

- **Provides thread-level parallelism: simultaneously execute a completely different** **instruction**

**stream on each core**

- **Software creates threads to expose parallelism to hardware \(e.g., via threading API\)**

But first let start with basic example with different flavors of parallelism 

Let’s code an example of calculating the sum of squares for all elements in an array, demonstrating its transformation across different processing models M. ZAIN UDDIN

52



Array processing 

• \#include <stdio.h>: this line includes the standard input/output library for printing the result. 

• int sum\_of\_squares\_array\(int data\[\], int len\): Declares a function named sum\_of\_squares\_array with two arguments: an integer array 

\#include <stdio.h> 

data and its length len. This function operates on the entire array simultaneously, a key characteristic of array processing. 

int sum\_of\_squares\_array\(int data\[\], int len\) \{

• int sum = 0;: Initializes the sum variable to 0, similar to the SISD 

int sum = 0; 

example. 

for \(int i = 0; i < len; \+\+i\) \{

• for \(int i = 0; i < len; \+\+i\): This loop iterates through each element in sum \+= data\[i\] \* data\[i\]; 

the data array, similar to the SISD example. However, the focus here 

\}

isn't on individual elements but on the entire array as a whole. 

• sum \+= data\[i\] \* data\[i\];: This line remains the same as the SISD 

return sum; 

example, squaring each element and adding it to the sum. Again, 

\}

although the loop iterates through each element, the operation affects the entire array's sum. 

int main\(\) \{

• return sum;: Returns the final sum of squares as the function's int data\[\] = \{2, 5, 7, 4\}; 

output. 

int sum = sum\_of\_squares\_array\(data, 4\); 

• int main\(\): Same as the SISD example, this marks the program entry printf\("Sum of squares: %d\\n", sum\); point. 

•

return 0; 

int data\[\] = \{2, 5, 7, 4\};: Defines the same sample data array. 

• int sum = sum\_of\_squares\_array\(data, 4\);: Calls the 

\}

sum\_of\_squares\_array function with the data array and its length, similar to the SISD example. 

• printf\("Sum of squares: %d\\n", sum\);: Prints the calculated sum to the console, just like before. 

• return 0;: Indicates successful program termination. 

M. ZAIN UDDIN

53





Multithreading

for \(int i = 0; i < num\_threads; \+\+i\) \{

thread\_data\[i\].start = i \* \(len / num\_threads\); thread\_data\[i\].end = \(i == num\_threads - 1\) ? len : \(i \+ 1\) \* \(len / num\_threads\); 

\#include <stdio.h> 

thread\_data\[i\].data = data; 

\#include <pthread.h> 

thread\_data\[i\].partial\_sum = NULL; 

\#include <stdlib.h> 

pthread\_create\(&threads\[i\], NULL, worker, &thread\_data\[i\]\); typedef struct \{

\}

int start; 

int end; 

int\* data; 

int total\_sum = 0; 

int\* partial\_sum; 

for \(int i = 0; i < num\_threads; \+\+i\) \{

\} thread\_data\_t; 

void\* result; 

pthread\_join\(threads\[i\], &result\); 

void\* worker\(void\* arg\) \{

total\_sum \+= \*\(int\*\)result; 

thread\_data\_t\* data = \(thread\_data\_t\*\)arg; 

free\(result\); 

int sum = 0; 

\}

for \(int i = data->start; i < data->end; \+\+i\) \{

sum \+= data->data\[i\] \* data->data\[i\]; return total\_sum; 

\}

int\* result = \(int\*\)malloc\(sizeof\(int\)\); 

\}

\*result = sum; 

return result; 

int main\(\) \{

\}

int data\[\] = \{2, 5, 7, 4\}; 

int sum\_of\_squares\_multithread\(int data\[\], int len, int num\_threads\) int sum = sum\_of\_squares\_multithread\(data, 4, 2\); 

\{

printf\("Sum of squares: %d\\n", sum\); pthread\_t threads\[num\_threads\]; 

thread\_data\_t thread\_data\[num\_threads\]; 

return 0; 

\}

M. ZAIN UDDIN

54

Multithreading

Include Headers:

\#include <stdio.h>: Standard input/output functions. 

\#include <pthread.h>: POSIX threads library for multithreading support. 

\#include <stdlib.h>: Standard library functions, including memory allocation \(malloc\). 

Define Thread Data Structure:

thread\_data\_t: A structure to hold data specific to each thread. 

start, end: Define the range of data each thread will process. 

data: Pointer to the array of data. 

partial\_sum: Pointer to the partial sum computed by each thread. 

Thread Function \(worker\):

worker: The function that each thread executes. 

arg: Void pointer to the thread-specific data \(thread\_data\_t\). 

sum: Local variable to compute the partial sum for the thread. 

The thread iterates over its assigned range of data, squares each element, and adds to sum. 

Allocates memory for an integer \(result\) and stores the partial sum in it. 

Returns the result. 

Multithreading Function \(sum\_of\_squares\_multithread\): Creates an array of threads \(pthread\_t threads\[num\_threads\]\) and an array of thread-specific data \(thread\_data\_t thread\_data\[num\_threads\]\). 

Assigns the start, end, data array, and partial\_sum for each thread. 

Creates threads using pthread\_create, passing the worker function and thread-specific data. 

Waits for each thread to complete using pthread\_join. 

Accumulates the results and frees allocated memory. 

M. ZAIN UDDIN

55

Refrence

Reference: Flynn, M. J. \(1972\). Some computer organizations and their effectiveness. 

IEEE Transactions on Computers, 100\(9\), 948-960. 

M. ZAIN UDDIN

56



