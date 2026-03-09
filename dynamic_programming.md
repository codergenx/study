

CSE 317: Design and Analysis of Algorithms
## Dynamic Programming
## Shahid Hussain
## Fall 2025
## SMCS, IBA

## Dynamic Programming
•The idea of dynamic programming is the following
•For a given problem, we define the notion of a subproblem and an ordering of
subproblems from“smallest”to“largest”.
•(i) the number of subproblems is polynomial, and
•(ii) the solution of a subproblem can be easily (in polynomial time) computed
from the solution of smaller subproblems
•If (i) and (ii) then we can design a polynomial algorithm for the initial problem
## 1

Shortest Paths in DAGS
•A graphGis called adirected acyclic graph(DAG) if it has no directed cycles
•For a given DAGGwe can perform a topological sort of the vertices ofG
(linearization ofG)
a
b
c
d
e
f
## 1
## 6
## 2
## 4
## 3
## 2
## 1
## 1
ac
bd
e
f
## 24611
## 1
## 3
## 2
## 2

Longest Increasing Subsequences (LIS)
•Given a sequence of numbers⟨a
## 1
## ,a
## 2
## ,...,a
n
## ⟩
•Asubsequenceis a sequence of numbers⟨a
i
## 1
## ,a
i
## 2
## ,...,a
i
k
## ⟩where
## 1≤i
## 1
< i
## 2
<···< i
k
## ≤n
•A subsequence isincreasing subsequenceifa
i
## 1
< a
i
## 2
<···< a
i
k
•For example, given sequence⟨5,2,8,6,3,6,9,7⟩, the LIS is⟨2,3,6,9⟩
•Following graphG= (V,E)is a DAG
## 52863697
## 3

Longest Increasing Subsequences (LIS)
Algorithm:LIS
Input:A sequence of numbers⟨a
## 1
## ,a
## 2
## ,...,a
n
## ⟩
Output:The length of the longest increasing subsequence
1.G(V,E)←create-dag(a
## 1
## ,a
## 2
## ,...,a
n
)//Gis the DAG for the input sequence
## 2.forj∈{1,2,...,n}
3.L(j) = 1 + max{L(i) : (i,j)∈E}
4.returnmax{L(j) :j∈{1,2,...,n}}
## 4

## Longest Common Subsequence
•LetΣbe some fixed and finite alphabet
•AstringXoverΣis a sequence of symbols fromΣi.e.,X=x
## 1
x
## 2
## ...x
n
## ,n≥0
•LetXbe a sequence of lengthnoverΣ
•We say that asubsequenceof lengthkofXis a sequencex
i
## 1
x
i
## 2
## ...x
i
k
such that
i
## 1
< i
## 2
<···< i
k
•Given two sequencesXandYlengthsnandm, respectively
•Acommon subsequenceof sequencesXandYis any sequence such that is
common to bothXandY
•The problemlongest common subsequenceis to find such a common subsequence
of maximum length
## 5

Longest Common Subsequence: Bruteforce approach
•A brute-force approach to solve such a problem would require to enumerate all
subsequences ofXand check if they are also common toY
•We can see that there areΘ(2
n
)subsequences of the sequenceXand we can
check whether it is also a subsequence inYin linear time i.e,Θ(m)
•Hence, brute-force algorithm would requireΘ(m·2
n
## )time.
## 6

## Longest Common Subsequence: Dynamic Programming
•We can solve this problem very efficiently usingdynamic programming
•We can define the problem of finding the longest common subequence ofXand
Yof lengthsnandm, respectively, asLCS(n,m)
•We can define a subproblem asLCS(i,j)which finds the longest common
subsequence of sequences ending atx
i
andy
j
i.e., betweenx
## 1
x
## 2
## ...x
i
and
y
## 1
y
## 2
## ...y
j
, for0≤i≤nand0≤j≤m
•It is clear thati= 0orj= 0represent an empty sequence (correspondingly)
•So, we know thatLCS(i,0) = 0as well asLCS(0,j) = 0for alliandj
## 7

## Longest Common Subsequence: Dynamic Programming
•We observe that there are two possible situations when comparingx
## 1
x
## 2
## ...x
i
and
y
## 1
y
## 2
## ...y
j
, that is eitherx
i
## =y
j
orx
i
## ̸=y
j
•Whenx
i
## =y
j
these two characters must be included in any common
subsequences that we may have found betweenx
## 1
x
## 2
## ...x
i−1
andy
## 1
y
## 2
## ...y
j−1
## ,
otherwise we need to check the longest common subsequences between
x
## 1
x
## 2
## ...x
i−1
andy
## 1
y
## 2
## ...y
j
and betweenx
## 1
x
## 2
## ...x
i
andy
## 1
y
## 2
## ...y
j−1
•Therefore,
LCS(i,j) =
## 
## 
## 
## 
## 
## 0ifi= 0orj= 0,
LCS(i−1,j−1) + 1ifi >0andj >0anda
i
## =b
j
## ,
max{LCS(i−1,j),LCS(i,j−1)}ifi >0andj >0anda
i
## ̸=b
j
## .
## 8

## Longest Common Subsequence: Dynamic Programming
Algorithm:TCS
Input:Two sequencesXandYof lengthsnandm, respectively
Output:The length of the longest common subsequence ofXandY
1.fori= 0ton:L(i,0) = 0
2.forj= 0tom:L(0,j) = 0
## 3.fori= 1ton
## 4.forj= 1tom
## 5.ifa
i
## =b
j
thenL(i,j) =L(i−1,j−1) + 1
6.elseL(i,j) = max{L(i,j−1),L(i−1,j)}
7.returnL(n,m)
## 9

## Longest Common Subsequence: Dynamic Programming
## Theorem
An optimal solution to the longest common subsequence problem can be found in
Θ(nm)time andΘ(min{n,m})space.
## 10

## Longest Common Subsequence: Example
•LetX=ABCBDABandY=BDCABAB
•The subsequenceBCBABis common to both
•We can create following table:
## -  B  D  C  A  B  A  B
## -0   0   0   0   0   0   0   0
## A
## 0   0   0   0   1   1   1   1
## B
## 0   1   1   1   1   2   2   2
## C0   1   1   2   2   2   2   2
## B0   1   1   2   2   3   3   3
## D0   1   2   2   2   3   3   3
## A0   1   2   2   3   3   4   4
## B0   1   2   2   3   4   45
## 11

## Matrix Chain Multiplication
•Let us consider matrices,A,B, andCof dimensionsn×1,1×n, andn×n,
respectively
•The dimensions of the productABisn×n
•So, the product(AB)Crequiresn
## 2
## +n
## 3
multiplications
•The dimensions of the productBCis1×n
•Therefore, the productA(BC)requiresn
## 2
## +n
## 2
## = 2n
## 2
multiplications
•Which clearly means computing(AB)Cis more expensive thanA(BC)
## 12

## Matrix Chain Multiplication
•Let us consider matricesA
## 1
## ,A
## 2
## ,...A
n
with dimensions,m
## 0
## ×m
## 1
## ,m
## 1
## ×m
## 2
## ,...,
m
n−1
## ×m
n
, respectively
•The problem is to find theoptimal parenthesizationof the productA
## 1
## A
## 2
## ···A
n
that minimizes the number of scalar multiplications
•The brute-force approach would require to enumerate all possible
parenthesizations and compute the number of scalar multiplications
•Fornmatrices, there are2
n−1
possible parenthesizations
•We will usedynamic programmingto solve this problem
## 13

## Matrix Chain Multiplication: Dyanmic Programming
•Let us define the subproblem as follows
•LetA
i
## A
i+1
## ···A
j
be a subsequence of matricesA
i
## A
i+1
## ···A
j
•LetB(i,j)denotes the subproblem of multiplying the matricesA
i
## A
i+1
## ···A
j
for
## 1≤i≤j≤n
•The problemB(1,n)represents the original problem
•Let us denoteC(i,j)as the number of scalar multiplications required to compute
the matrixA
i
## A
i+1
## ···A
j
## 14

## Matrix Chain Multiplication: Dyanmic Programming
•We can see thatC(i,j) = 0ifi=j
•Forj > i, we can see that
C(i,j) =  min
i≤k<j
{C(i,k) +C(k+ 1,j) +m
i−1
## ·m
k
## ·m
j
## }
•If the last operation of matrix multiplication divides the productA
i
## A
i+1
## ···A
j
into two subproducts(A
i
## A
i+1
## ···A
k
## )(A
k+1
## A
k+2
## ···A
j
)then to obtain the
minimum number of element multiplications in the both subproducts and
m
i−1
## ·m
k
## ···m
j
element multiplications to multiply the two subproducts
•We choose thekfor which it minimizes the number of scalar multiplications
•Since there areO(n
## 2
)subproblems and each requireO(n)time to solve, the total
time complexity isO(n
## 3
## )
## 15

## Edit Distance
•Suppose we two stringsXandYover some fixed and finite alphabetΣ
•A natural measure of a distance between these strings is the degree to which they
can be aligned, or matched up
•An alignment is a way of writing the strings one above the other.
•Let us consider two possible alignments of stringsSNOWYandSUNNY.
•The symbol‘‘
’’indicates a “gap”.  Any number of gaps can be added to each
string
•The cost of an alignment is the number of columns in which the letters differ.
The edit distance between two strings is the cost of the best alignment
## S
## N  O  W  YS  N  O  WY
## S  U  N  NY      S  U  NN  Y
## 16

## Edit Distance
•In the first alignment the cost is equal to3
•And in the second alignment the cost is equal to5
•In other words, the edit distance is the minimum number ofinsertions,deletions
andsubstitutionsof characters (letters) needed to transform the first string into
the second one
•In the first example we insertU, substituteO→Nand deleteW
## 17

## Edit Distance
•LetX=x
## 1
## ,...,x
m
andY=y
## 1
## ,...,y
n
•For eachi∈{0,1,...,m}andj∈{0,1,...,n}, we consider the problem of
finding the edit distance betweenx
## 1
## ,...,x
i
andy
## 1
## ,...,y
j
, and denote byE(i,j)
the considered distance
•Ifi= 0, the wordx
## 1
## ,...,x
i
is the empty wordε.  The same situation is for the
casej= 0.  It is clear thatE(i,0) =iandE(0,j) =jsince the edit distance
between the empty wordεand a nonempty wordαof the lengthtis equal tot
•Let us consider the best alignment forx
## 1
## ,...,x
i
andy
## 1
## ,...,y
j
wherei >0and
j >0.  It is clear that in the rightmost column we can have one of the following
three things:
x
i
x
i
y
j
y
j
## 18

## Edit Distance
•In the first case,E(i,j) = 1 +E(i−1,j).  In the second case,
E(i,j) = 1 +E(i,j−1), and in the third case,
E(i,j) = diff(i,j) +E(i−1,j−1), wherediff(i,j) = 0ifx
i
## =y
j
and
diff(i,j) = 1ifx
i
## ̸=y
j
## .  Therefore,
E(i,j) = min{1 +E(i−1,j),1 +E(i,j−1),diff(i,j) +E(i−1,j−1)}
•We have(m+ 1)×(n+ 1)subproblems.  If we knowE(i−1,j),E(i,j−1), and
E(i−1,j−1)then to compute the valueE(i,j)it is necessary to make3
operations of comparisons of numbers (1to find the valuediff(i,j), and2to find
min) and3operations of addition
•So, the considered algorithm makesO(mn)operations of addition and
comparison of numbers
## 19

## Edit Distance
•To find the valueE(m,n)we should fill the table withm+ 1rows labeled with
numbers0,1,...,m, andn+ 1columns labeled with numbers0,1,...n
•At the intersection ofi-th row andj-th column we should have the numberE(i,j)
•At the beginning, we can fill valuesE(i,0) =iandE(0,j) =j, and after that
row by row, from the left to the right we can fill out the table
•Note that it is not necessary to have the whole table in the memory:  to fill the
i-th row,i >0, it is enough to know values in the rowi−1
## 20

## Edit Distance
•Now we can find the optimal alignment if the considered table is filled
•IfE(m,n) = 1 +E(m−1,n), then in the optimal alignment the last column is
x
m
•IfE(m,n) = 1 +E(m,n−1), then in the optimal alignment the last column is
## −
y
n
•IfE(m,n) = diff(m,n) +E(m−1,n−1), then in the optimal alignment the last
column is
x
m
y
n
•To find the next column we should consider:  In the first case—the subproblem
E(m−1,n).  In the second case—the subproblemE(m,n−1)and in the third
case - the subproblemE(m−1,n−1), etc
## 21

## Edit Distance: Example
## SUNNY
## 012345
## S101234
## N211123
## O322223
## W433333
## Y544443
x
i
x
i
y
j
i−1,j−1i−1,j
i,j−1i,j
y
j
i,j−1i,j
## S  N  O  W  Y
## S  U  N  N  Y
## SN  O  W  Y
## S  U  N  NY
## SN  O  W  Y
## S  U  NN  Y
## 22

Shortest Path: Floyd-Warshall Algorithm
•LetGbe a complete directed graph withnverticesv
## 1
## ,v
## 2
## ,...,v
n
•Each edge(v
i
## ,v
j
)has a labeld
ij
## ∈R∪{+∞}
•We say thatd
ij
is thelengthof the edge(v
i
## ,v
j
## ).  Clearly,d
ii
## = 0fori= 1,...,n
•The length of a directed path fromv
i
tov
j
is equal to+∞if the length of at
least one edge in the path is equal to+∞
•It is possible to have negative lengths i.e.,d
ij
<0however there is no directed
cycle with negative length (no negative cycles)
## 23

Shortest Path: Floyd-Warshall Algorithm
•The minimum distanced
## ∗
ij
fromv
i
tov
j
is equal to the minimum length of a
directed path fromv
i
tov
j
•For a givenn×nmatrixD= [d
ij
]of lengths of edges, we should construct the
matrixD
## ∗
## = [d
## ∗
ij
]of minimal distances
•For anyi,j∈{1,...,n}andk∈{0,1,...,n}let us consider the following
subproblem to computed
## (k)
ij
which is the length of the shortest path fromv
i
tov
j
in which only verticesv
## 1
## ,...,v
k
can be used as intermediate vertices.  Ifk= 0
thend
## (0)
ij
## =d
ij
## 24

Shortest Path: Floyd-Warshall Algorithm
•LetD
## (k)
## = [d
## (k)
ij
].  ThenD
## (0)
=DandD
## (n)
## =D
## ∗
, we will sequentially compute
## D
## (1)
## ,D
## (2)
## ,...,D
## (n)
.  Let us prove that for everyi,jandk >0
d
## (k)
ij
= min
n
d
## (k−1)
ij
## ,d
## (k−1)
ik
## +d
## (k−1)
kj
o
## .
•All directed paths fromv
i
tov
j
that use onlyv
## 1
## ,...,v
k
as intermediate vertices
can be divided into two setsAandBwhich do not pass throughv
k
and which
pass throughv
k
, respectively
•The minimum length of path fromAis equal tod
## (k−1)
ij
.  Since there are no
negative cycles inG, there exists a shortest pathτfromBwhich passes through
v
k
exactly once.
## 25

Shortest Path: Floyd-Warshall Algorithm
•Soτcan be divided into two paths:  a path fromv
i
tov
k
which use only vertices
v
## 1
## ,...,v
k−1
(the minimum length of such a path is equal tod
## (k−1)
ik
and a path
fromv
k
tov
j
which uses only verticesv
## 1
## ,...,v
k−1
(the minimum length of such
a path is equal tod
## (k−1)
kj
•Therefore, the length ofτis equal tod
## (k−1)
ik
## +d
## (k−1)
kj
and the considered equality
holds
•If we knowD
## (k−1)
then to computeD
## (k)
it is enough to maken
## 2
operations of
additions andn
## 2
operations of comparisons of numbers
•Therefore, to computeD
## (n)
## =D
## ∗
it is enough to makeO(n
## 3
)operations of
addition and comparisons
## 26

Shortest Path: Floyd-Warshall Algorithm: Example
## 1
## 2
## 3
## +∞
## −1
## 4
## 21
## −2
## 27

Shortest Path: Floyd-Warshall Algorithm: Example
For this example we compute the shortest path as following:  for everyi,jandk >0,
d
## (k)
ij
= min
n
d
## (k−1)
ij
## ,d
## (k−1)
ik
## +d
## (k−1)
kj
o
.  Ifi=korj=k, thend
## (k)
ij
## =d
## (k−1)
ij
## .
## D
## (0)
## =
## 123
## 10   +∞ −2
## 220−1
## 3410
## ,D
## (1)
## =
## 123
## 10   +∞ −2
## 220-1
## 3410
## D
## (2)
## =
## 123
## 10   +∞-2
## 220−1
## 3310
## ,D
## (3)
## =
## 123
## 10-1−2
## 220−1
## 3310
## =D
## ∗
## 28