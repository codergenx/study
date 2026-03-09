

CSE 317: Design and Analysis of Algorithms
## Sample Questions: Midterm
1.O-notation questions.  Prove/disprove:
(a)  Iff(n) =O(g(n)) andg(n) =O(h(n)) thenf(n) =O(h(n)).
(b)  Iff(n) =O(g(n)) thenf(n) =o(g(n)).
(c)  Iff(n) =o(g(n)) andf(n) =ω(h(n)) thenh(n) =o(g(n)).
-  Solve recurrences:
(a)A(n) = 3T
## 
n
## 4
## 
+nlognwithA(1) = 1.
(b)B(n) = 3B(n−1)−2B(n−2) withB(0) = 1 andB(1) = 2.
(c)  **C(n) = 2C(
## √
n) + 3 log
## 2
nwhenn >2 andC(n) = 1 forn= 2.
-  LetGbe a connected undirected graph with distinct edge weights.  Prove that the MST is
unique.
-  In  any  connected  graph,  removing  the  heaviest  edge  from  the  MST  always  increases  its
weight.
-  The minimum edge incident to every vertex must appear in every MST.
-  Suppose a graph has negative edge weights but no negative cycles.  Does Prim’s algorithm
still work correctly?  Explain.
-  Given two sorted arraysAandB, each of lengthn, find the median of all elements ofA∪B
inO(logn) time.
-  Given sorted arraysAandB, find whether there existsa∈A, b∈Bsuch thata−b=k.
AchieveO(n) time.
-  Given two sorted arraysA, B, find thek-th smallest sum among alla+bpairs.
-  Given a sorted arrayA, count the number of triplets (i, j, k) such thatA[i] +A[j] =A[k].
-  Given ann×nmatrix where each row and column is sorted, design anO(n)-time search
algorithm for an elementx.
-  Modify your algorithm if the matrix rows are sorted ascending but columns descending.
-  Devise a divide-and-conquer algorithm to compute the transpose of a large square matrix
in parallel.  Analyze work and depth.
-  Write the recurrence for the Longest Common Subsequence (LCS) and analyze time com-
plexity.