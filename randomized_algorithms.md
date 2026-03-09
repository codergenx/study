

CSE 317: Design and Analysis of Algorithms
## Randomized Algorithms
## Shahid Hussain
## Fall 2025
## 1

## Probability Theory

## Probability Theory
•We say the setSis thesample space(the certain event)
•The elements ofSare calledelementary events
•An event is a subset ofSand∅is called thenull event
•Two eventsAandBaredisjoint (mutually exclusive)ifA∩B=∅.
## 2

## Probability Theory: Distribution
•We say Pr : 2
## S
→Ris aprobability distributiononSif it satisfies the following
axioms:
-  Pr{A}≥0 for any eventA
-  Pr{S}= 1
-  Pr{A∪B}= Pr{A}+ Pr{B}for any two disjoint eventsAandB
More generally, for any (finite or countably infinite) sequence of events
## A
## 1
## ,A
## 2
,...that are pairwise disjoint,
## Pr
## (
## [
i
## A
i
## )
## =
## X
i
Pr{A
i
## }
•We have Pr{∅}= 0 and Pr{
A}= 1−Pr{A}whereA=S\A.  IfA⊆Bthen
Pr{A}≤Pr{B}.  For any two evensAandB,
Pr{A∪B}= Pr{A}+ Pr{B}−Pr{A∩B}.
## 3

## Probability Theory: Distribution
•Aprobability distributionis discrete ifSis a finite or countably infinite
•In this case for any eventA, Pr{A}=
## P
s∈A
## Pr{s}
•IfSis finite and Pr{s}= 1/|S|for anys∈Sthen we have theuniform
probability distributiononS
•Two events areindependentif Pr{A∩B}= Pr{A}Pr{B}
•A collection of eventsA
## 1
## ,...A
n
isindependentif, for every set of indices
I⊆{1,...,n}we have
## Pr
## (
## \
i∈I
## A
i
## )
## =
## Y
i∈I
Pr{A
i
## }
## 4

## Probability Theory: Random Variables
•Adiscrete random variableXis a function from a finite or countably infinite
sample spaceSto the real numbers
•For a random variableXand a real numberx, we define the eventX=xto
be{s∈S:X(s) =x}.  Thus,
Pr{X=x}=
## X
s∈S,X(s)=x
## Pr{s}
•The functionf(x) = Pr{X=x}is theprobability mass function(PMF) of the
random variableX
•From the probability axioms,f(x)≥0 and Σ
x
f(x) = 1
## 5

## Probability Theory: Expected Values
•Theexpected value(expectation or mean) of a discrete random variableXis
## E[X] =
## X
x
xPr{X=x},
which is well defined if the sum is finite or converges absolutely
•For any two random variablesXandY,E[X+Y] =E[X] +E[Y] or more
generally for random variablesX
## 1
## ,X
## 2
## ,...,X
n
and forα
## 1
## ,α
## 2
## ,...,α
n
where
α
i
∈Rfor each 1≤i≤n
## E[α
## 1
## X
## 1
## +α
## 2
## X
## 2
## +···+α
n
## X
n
## ] =α
## 1
## E[X
## 1
## ] +α
## 2
## E[X
## 2
## ] +···+α
n
## E[X
n
## ]
•This property is called thelinearity of expectation.  It also expands to
absolutely convergent summations of expectations.
## 6

Probability Theory: Bernoulli/Binomial Trial
## Lemma
If we repeatedly perform independent trials of an experiment, each of which
succeeds with probabilityp >0, then the expected number of trials we need to
perform until the first success is1/p.
## 7

Probability Theory: Bernoulli/Binomial Trial
Proof of the Lemma.
LetXbe the random variable equal to the number of trials.  Forj >0, we have
Pr{X=j}= (1−p)
j−1
p.  Then
## E[X]    =
## ∞
## X
j=1
j·Pr{X=j}=
## ∞
## X
j=1
j·(1−p)
j−1
p
## =p
## ∞
## X
j=1
j·(1−p)
j−1
## =
p
p
## 2
## =
## 1
p
## .
[We know that
## P
## ∞
j=1
q
j
= 1/(1−q) for|q|<1.  Differentiating both sides with respect toqwe get:
d
dq

## ∞
## X
j=1
q
j
## !
## =
## ∞
## X
j=1
d
dq
## (q
j
## ) =
## ∞
## X
j=1
jq
j−1
## =
d
dq
## 
## 1
## 1−q
## 
## =
## 1
## (1−q)
## 2
## .]
## 8

## Randomized Algorithms

## Randomized Algorithms
•We will consider examples of randomized algorithms which can make random
decisions during their work
•Randomized algorithms are often conceptually much simpler than the
deterministic ones
•Randomized algorithms can be generally categorized in two ways:Las Vegas
algorithmsandMonte Carlo algorithms
•Las Vegas algorithms always give the correct answer (whenever they produce
an answer), but they may take a long time to do so
•On the other hand Monte Carlo algorithms may give the wrong answer, but
they are guaranteed to give the correct answer with high probability
## 9

## Randomized Algorithms
•Let us consider one problem and two randomized algorithms for this problem
one Las Vegas and one Monte Carlo
•Consider an arrayAofnelements
•Such that each half of the array contains 0’s and half of the array contains 1’s
•We need to find the indexjsuch thatA[j] = 1
## 10

## Randomized Algorithms: Las Vegas Algorithm
Algorithm:find-one-LasVegas
Input:An arrayAofnelements, s.t.  half ofAis 1’s and half is 0’s
Output:The indexjsuch thatA[j] = 1
## 1.whiletrue
## 2.j←random(1,n)
3.ifA[j] = 1returnj
•Above algorithm will ultimately find an indexjsuch thatA[j] = 1 if the
random number generator used in Line 2 is does not repeatedly select the
same element again and again.
## 11

## Randomized Algorithms: Monte Carlo Algorithm
Algorithm:find-one-MonteCarlo
Input:An arrayAofnelements, s.t.  half ofAis 1’s and half is 0’s andk >0
Output:An indexjs.t.A[j] = 1 (success), otherwisenilwithp= (1/2)
k
## (failure)
## 1.i= 0
2.whilei < k
## 3.j←random(1,n)
## 4.i←i+ 1
5.ifA[j] = 1returnj
## 6.returnnil
•This algorithm does not guarantee to give correct answer all the times
•When successful it returns the indexjs.t.A[j] = 1, otherwise fails with probability (1/2)
k
•Ifkis sufficiently large then the probability of failure is very small
## 12

## Selection Problem
•LetS=⟨a
## 1
## ,a
## 2
## ,...,a
n
⟩be a sequence ofndistinct numbers
•It is convenient to assumeSis a set
•For a givenk, 1≤k≤n, theselection problemis to find thek-th smallest
element ofS
•This is a generalization of the median finding problem wherek= (n+ 1)/2 if
nis odd andk=n/2 ifnis even
## 13

## Randomized Selection Algorithm
•We will consider the following recursive algorithmselect(S,k)
•We choose an elementa
i
∈Sat random, call itsplitter
•We partitionSinto two setsS
## −
={a∈S:a < a
i
}, and
## S
## +
={a∈S:a > a
i
## }
•If|S
## −
|=k−1, then thek-th smallest element isa
i
•If|S
## −
|> k−1, then we thek-th smallest element inS
## −
,select(S
## −
## ,k)
•If|S
## −
|< k−1, then thek-th smallest element inS
## +
,select(S
## +
,k−|S
## −
## |−1)
Independent of the choice of the splitter this algorithm finds thek-th smallest
element ofS
## 14

## Example
•Letn= 7,k= 5, andS={4,8,3,9,15,11,2}
•We choosea
i
= 4 as the splitter we get:
## •S
## −
## ={3,2},S
## +
## ={8,9,15,11}
•Since|S
## −
|= 2< k−1 = 4, we need to find the 2-nd smallest element inS
## +
## ,
k= 2
•We choosea
i
= 11 as the splitter we get:
## •S
## −
## ={8,9},S
## +
## ={15}
•Since|S
## −
|= 2> k−1 = 4, we need to find the 2-nd smallest element inS
## −
•We choosea
i
= 9 as the splitter we get:
## •S
## −
## ={8},S
## +
## =∅
•Since|S
## −
|= 1 =k−1 = 1, the 5-th smallest element is  9
## 15

Analysis of Selection Algorithm: Worst-Case
•During the construction ofS
## −
andS
## +
•Theselectalgorithm makesn−1 comparisons fromSwitha
i
(the splitter)
•In the worst-case, the algorithm chooses the maximal number inSas the
splitter
•Therefore, the number of comparisons in the worst-case will be:
## (n−1) + (n−2) +···+ 1 =
n(n−1)
## 2
## = Ω(n
## 2
## )
## 16

Analyis of Selection Algorithm: Average-Case
•We will analyze the expected number of comparisons made by theselect
algorithm
•We will assume that the splitter is chosen uniformly at random fromS
•LetXbe the random variable equal to the number of comparisons made by
the algorithm
•LetX
i
be the random variable equal to the number of comparisons made by
the algorithm when the splitter isa
i
•We haveX=X
## 1
## +X
## 2
## +···
•We will analyze the expected value ofX
i
and then use the linearity of
expectation to find the expected value ofX
•We will show that the expected number of comparisons isO(n)
## 17

Analyis of Selection Algorithm: Average-Case
•We say that the algorithm is in phasejwhen the size of the set under
consideration (denoted asm) satisfies the following inequality:
n
## 
## 3
## 4
## 
j+1
< m≤n
## 
## 3
## 4
## 
j
•In a given iteration we say that an element iscentralif there are at least
⌊m/4⌋elements which are smaller than it and at least⌊m/4⌋elements which
are larger than it
•If a central element is chosen as the splitter than the number of elements the
algorithm has to work with will be at mostm−⌊m/4⌋−1, and clearly
k−
j
m
## 4
k
## −1≤m
## 
## 3
## 4
## 
## ≤n
## 
## 3
## 4
## 
j+1
•Now the algorithm is in phasej+ 1
## 18

Analyis of Selection Algorithm: Average-Case
•It is clear that the number of central elements is at leastm−2⌊m/4⌋≥m/2
•Therefore, the probability that the algorithm chooses a central element is at
least 1/2
•Therefore, the expected number of iterations before a central element is found
is at most 2
•Therefore, the expected number of comparisons made by the algorithm in
phasejis at most 2n
## 
## 3
## 4
## 
j
, now
## E[X] =E
## 
## 
## X
j
## E[X
j
## ]
## 
## 
## ≤
## X
j
## E[X
j
## ] = 2n
## X
j
## 
## 3
## 4
## 
j
= 8n=O(n)
## 19

QuickSort
•QuickSort is a sorting algorithm which is based on the divide-and-conquer
paradigm
•The algorithm works as follows:
-  Choose an elementa
i
from the arrayAat random, call it thepivot
-  Partition the array into two setsA
## −
={a∈A:a < a
i
## }and
## A
## +
={a∈A:a > a
i
## }
-  Recursively sortA
## −
andA
## +
and concatenate the sorted arrays
•The algorithm is in-place and has a space complexity ofO(logn)
•The worst-case time complexity of the algorithm isO(n
## 2
## )
•The average-case time complexity of the algorithm isO(nlogn)
## 20

Analysis of QuickSort
•Worst-case:During each iteration QuickSort makesn−1 comparisons,
therefore the total number of comparisons in the worst-case would be:
## (n−1) + (n−2) +···+ 1 =
n(n−1)
## 2
## = Ω(n
## 2
## )
## 21

Average Case Analysis of QuickSort
•Letz
i
be thei-th smallest element ofA
•LetXbe the random variable equal to the number of comparisons made by
QuickSort
•For 1≤i < j≤n, letX
ij
be the indicator random variable if the elementsz
i
andz
j
are compared
•We can conclude that:
## X=
n−1
## X
i=1
n
## X
j=i+1
## X
ij
•Since eachX
ij
is independent and identically distributed, we have:
## E[X] =
n−1
## X
i=1
n
## X
j=i+1
## E[X
ij
## ] =
n−1
## X
i=1
n
## X
j=i+1
## Pr{z
i
andz
j
are compared}
## 22

Average Case Analysis of QuickSort (cont.)
•LetZ
ij
## ={z
i
## ,z
i+1
## ,...,z
j
}be the set of elements betweenz
i
andz
j
in the
sorted array
•In order forz
i
andz
j
to be compared, the pivot must be chosen fromZ
ij
•The probability that the pivot is chosen fromZ
ij
is 2/|Z
ij
## |= 2/(j−i+ 1)
•We get:
## E[X] =
n−1
## X
i=1
n
## X
j=i+1
## 2
j−i+ 1
## = 2
n−1
## X
i=1
n
## X
j=i+1
## 1
j−i+ 1
## ≤2
n−1
## X
i=1
n
## X
k=2
## 1
k
## ≤2nlnn
•Here lnk≤H(k)≤lnk+ 1, whereH(k) = 1 + 1/2 +···+ 1/k
•Therefore, the average-case time complexity of QuickSort isO(nlogn)
## 23

String Equality Testing with Randomized Algorithms
•Problem:  Alice and Bob want to check if their stringsxandyare equal.
•Solution:  Use a fingerprint (hash) to represent each string.
## Algorithm
-  Alice selects a primepfrom the set of primes less thanM
-  Alice computesf
p
## (x).
-  Alice sendspandf
p
(x) to Bob.
-  Bob comparesf
p
(x) withf
p
(y) to check equality.
## 24

Probability of False Positives in String Equality
•Letnbe the no.  of bits in the stringsx
•Ifyrequires more or less thann-bits then clearlyx̸=y
•Letπ(n) be the no.  of primes less thann,
π(n)≃
n
lnn
•Fork <2
n
the no.  of distinct primes that dividekis less thanπ(n) (except
whenkis very small)
## 25

Probability of False Positives in String Equality
•False positives occur ifx̸=ybutf
p
## (x) =f
p
## (y)
•This is only possible ifpdividesf(x)−f(y)
•LetN(p,n) denote the no.  of primes less than 2
n
s.t., each prime divides
f(x)−f(y)
•We know thatN(p,n)≤π(n) therefore,
## N(p,n)
π(n)
## ≤
π(n)
π(M)
•Now lettingM= 2n
## 2
we obtain:
## Pr{failure}≤
π(n)
π(M)
## ≃
n/lnn
## 2n
## 2
## /ln 2n
## 2
## =
n
lnn
## ·
ln 2n
## 2
## 2n
## 2
## ≈
## 1
n
•If we letk=⌈log logn⌉then we have:
## Pr{failure}≤
## 1
n
k
## 26

## Example
•Letn= 10
## 6
, thenM= 2n
## 2
## = 2×10
## 12
## = 2
## 40.8631
•The no.  of bits required to transmitpis⌊M⌋+ 1 = 40 + 1 = 41
•Similarly the no.  of bits required to transmit
⌊log(p−1)⌋+ 1≤⌊logM⌋+ 1 = 41
•Thus, the total no.  of bits required to transmitpandf
p
(x) is 82
•The probability of failure in one transmission is at most 1/n= 1/10
## 6
•Since,⌈log logn⌉= 5, repeating the algorithm five times reduces the
probability of false positive to
n
−⌈log logn⌉
## = (10
## 6
## )
## −5
## = 10
## −30
•Which is negligible
## 27

## Pattern Matching
•Given a textT(of lengthn) and a patternP(of lengthm) (m≤nand
## T,P∈{0,1}
## ∗
## )
•We need to determine ifPappears inT
•A simple solution is to move the pattern across the text
•This solution has a time complexity ofO(mn)
•We can design and Monte Carlo algorithm to solve it inO(m+n)
•This Monte Carlo algorithm can easily be turned into a Las Vegas algorithm
with the same complexity bound ofO(m+n)
## 28

## Pattern Matching
•LetT=t
## 1
t
## 2
## ···t
n
be the text andP=p
## 1
p
## 2
## ···p
m
be the pattern
•The Monte Carlo algorithm works similarly to the brute-force algorithm by
sliding the pattern across the text
•However, rather than comparing the pattern with the text at each position,
we compare the fingerprint of the pattern with the fingerprint of the text at
each position (block of text)
•LetT(j) =t
j
t
j+1
## ···t
j+m−1
be the block of text of lengthmstarting at
positionjin the textT
•We will compare the fingerprintI
q
(P) of the pattern moduloqwith the
fingerprintI
q
(T(j)) of the block of textT(j) moduloq
•TheseO(n) fingerprints can be easily computed
## 29

## Pattern Matching
•LetI
q
(T(j)) represents the fingerprint of the block of textT(j) moduloq
•Then the fingerprint of the block of textT(j+ 1) can be computed as:
## I
q
(T(j+ 1)) = (2I
q
(T(j))−2
m
t
j
## +t
j+m
)    modq
•If we letW= 2
m
modqthen we have:
## I
q
(T(j+ 1)) = (2I
q
(T(j))−Wt
j
## +t
j+m
)    modq
## 30

## Pattern Matching
## Algorithm:pattern-matching
Input:A textTof lengthnand a patternPof lengthm
Output:The 1-st indexjsuch thatt
j
## =p
## 1
## ,...,t
j+m−1
## =p
m
or 0 otherwise
1.q←random(1,M)
## 2.j←1
## 3.W
q
## ←2
m
modq
-  ComputeI
q
(P) andI
q
(T(j))
## 5.whilej≤n−m+ 1
6.ifI
q
## (P) =I
q
(T(j))returnj
## 7.I
q
(T(j+ 1))←(2I
q
(T(j))−W
q
t
j
## +t
j+m
)  modq
## 8.j←j+ 1
## 9.return0
## 31

Analysis of Pattern Matching Algorithm
•The computation of each ofI
q
(P) andI
q
(T(1)) requiresO(m) operations
## •I
q
(T(j+ 1)) requiresO(1) operations for 2≤j≤n−m+ 1, total =O(n)
•Therefore, the running time isO(n+m)
•A false match occurs ifI
q
## (P) =I
q
(T(j)) butP̸=T(j)
•This is possible if the chose primepdivides
ζ=
## Y
{j:P̸=T(j)}
|I(P)−I(T(j))|
## •ζ≤(2
m
## )n= 2
mn
•Therefore, the no.  of primes that divide it cannot exceedπ(mn)
## 32

Analysis of Pattern Matching Algorithm
•If we letM= 2mn
## 2
then the probability of a false match cannot exceed:
π(mn)
π(M)
## ≈
mn/ln(mn)
## 2mn
## 2
## /ln(mn
## 2
## )
## <
## 1
n
•This probability is independent ofm(size of the pattern)
•Whenm=n, the problem reduces to string equality testing
## 33

Converting Monte Carol to Las Vegas
•Whenever the two fingerprintsI
q
## (P) =I
q
(T(j)) we can test the corresponding
blocks of text and pattern
•If they are equal then we have found a match
•If not then we have a false match and we repeat
•The expected running time of this Las Vegas algorithms becomes
## O(m+n)·
## 
## 1−
## 1
n
## 
## +mn
## 
## 1
n
## 
=O(m+n)
•That is, the Las Vegas algorithm has the same expected running time as the
Monte Carlo algorithm
## 34

## Random Sampling
•Given a setSofnelements
•We want to select a random sample ofkelements fromS,k < n
•Assume without loss of generality thatS={1,2,...,n}
•We can use the following Θ(n) Las Vegas algorithm
## 35

## Random Sampling
## Algorithm:random-sampling
Input:Two positive integersnandksuch thatk < n
Output:An arrayA[1..k] ofkdistinct elements from{1,2,...,n}
## 1.B=⟨0⟩
n
//BXis ann-bit vector of0’s
## 2.j←0
3.whilej < k
## 4.r=random(1,n)
5.ifB
i
## = 0
## 6.j←j+ 1
7.A[j]←r
## 8.B
r
## ←1
9.returnA
## 36

Analys of Random Sampling Algorithm
•Ifk≈ni.e., much larger thann/2 in that case we can discardn−kelements
and return the rest, so, assumingk≤n/2
•Letp
j
be the probability that thej−1 elements have already been selected
1≤j≤k, clearly
p
k
## =
n−j+ 1
n
•LetX
j
be the indicator random variable that thej-th element is selected
•Then the expected value ofX
j
is
## E[X
j
## ] =
## 1
p
k
## =
n
n−j+ 1
•LetX=X
## 1
## +X
## 2
## +···+X
k
then the expected value ofXis
## E[X] =
k
## X
j=1
## E[X
j
## ] =n
k
## X
j=1
## 1
n−j+ 1
## =n
k
## X
j=1
## 1
n
## −n
n−k
## X
j=1
## 1
n
## 37

Analys of Random Sampling Algorithm
•We known
## P
n
j=1
1/j≤lnn+O(1), therefore
E[X]≤n(lnn+ 1)−n(ln(n−k+ 1))
## =n(lnn+ 1−ln(n−k+ 1))
## ≤n(lnn+ 1−ln(n/2))sincek≤n/2
## =n(ln 2 + 1)
## =nln(2e)
## ≈1.69n
•The expected running time of this algorithm is Θ(n)
## 38