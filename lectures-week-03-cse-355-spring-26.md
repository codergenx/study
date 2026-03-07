<!-- Slide number: 1 -->

![](Picture2.jpg)

# Introduction to BlockchainCSE-355

Ahmed Akhtar
Department of Computer Science
SMCS, IBA Karachi
Spring 2026

### Notes:

<!-- Slide number: 2 -->
# Lecture 05Tuesday, Feb 03, 2026
2

<!-- Slide number: 3 -->
# Public Key Cryptography
Each user generates a public-private key pair
Public keys: very public	Private keys: very private

![Timeline Description automatically generated](ContentPlaceholder5.jpg)

Alice
(sender)
Bob
(receiver)

May the force be with you
May the force be with you
Thought Question:
Bob receives some data

Can he now be sure it
came from Alice?

Alice’s Private key
Alice’s Public key
Alice (encrypts) or locks the transaction
1) Using her private key – Only her public key can unlock
In addition, Alice can ALSO OPTIONALLY (why?)
2) Use Bob’s public key – Only Bob’s private key can unlock

3

### Notes:
AND CAN ALSO OPTIONALLY (why?): If Alice does not want anyone else, other than Bob, to read the message!

Is Bob now sure about a message that he may receive as coming from Alice? Still NO!

<!-- Slide number: 4 -->
# Digital Signatures: A simple-minded approach
Alice “signs” with her own private key
Signing is the same process as encrypting/encoding
Alice sends to Bob – a signed document
The original document
The signatures
Bob uses Alice’s public key to decode the signature and compares
If comparison works, this [probably?] verifies:
It was Alice who sent the message (authentication/non-repudiation)
The message was not forged (integrity)
Anyone else can also decode the message
And that may also be ok
What if we don’t want anyone else to decode the message?
4

<!-- Slide number: 5 -->
# PKI and Transactions on Bitcoin Blockchain
Cryptocurrency owned by Alice
From a previous transaction [by someone who paid her]
Value locked [previously] to Alice’s PUBLIC key
Alice unlocks the entire value in the transaction
Using her PRIVATE key
No one else can do it
Alice makes the transaction
Locks some value to Bob’s PUBLIC key (pays to public key!)
Only Bob will be able to unlock using his PRIVATE key
Important: Alice locks the remaining value to her own PUBLIC key
Important: Alice can’t deny making the transaction later on. Why?
5

<!-- Slide number: 6 -->
# Digital Signatures: Integrity + Authentication

GOAL: Check for Message integrity and Sender’s Authenticity
Message M
Signature Y
Received Y
M
Alice
Processes
Bob
Processes
Same?
Transfer Y and M
Claim: I am Alice and
I made signature Y from M
Alice’s
Private key
Alice’s
Public key

If what Bob decodes (M) matches,
then it’s legit (integrity) and Y is also fine (authenticity)…
			authentication and integrity verified?
Thought Question:  Bob receives “some” data
Can he now be sure it came from Alice?
6

### Notes:

<!-- Slide number: 7 -->
# Kevin can claim to be Alice

Kevin has no access to Alice’s private key – can still cause trouble!
Text K
Text L
Text K
L
Kevin
Processes
Bob
Processes
Same?
Transfer K and L
(False) Claim: I am Alice and
I made signature K from L
Alice’s
Public key
Alice’s
Public key

Since L matches, Bob thinks L is a legit message and… sender is Alice

(A little bit of) Good News: Kevin can control K but not L
(Still some) Bad News: It’s an injection of garbage data

How to avoid this? Try hashing before signing
7

### Notes:

<!-- Slide number: 8 -->
# Public Key Cryptography
May the force be with you
Create a message digest (using cryptographic hashing)
Encrypt the message digest with your private key
Send the signatures along with the message
Message
Hashing
At the receiver
Decrypt the hash value [using public key]
Compute message hash value
Compare!
Brings about:
Sender authentication
Message integrity
Hash Value
Private
Key
Signature
Message + Digital Signatures
= Signed Message

Public
Key
Hashing
Decrypt
Kevin (or anyone else) can’t insert garbage
Because the hash function is one-way
Comapre the two?
8

### Notes:

<!-- Slide number: 9 -->
# Blockchain Security
With all the security, authentication, verification, etc., can we still break a blockchain?
Before answering this, we need to understand/consider a fork

Two miners can almost simultaneously create candidate blocks
Broadcasted to all connected nodes – both blocks valid!
Added to journals, causing a fork – an accidental or natural fork

Over time, one will become part of the ledger (longest chain)
Naturally occurring forks are frequent and automatically resolved
When we talk of forks, we don’t talk of natural/accidental ones
9

<!-- Slide number: 10 -->
# Forks with a Purpose: Hard Fork
Loosens the rules for newly created blocks (more liberal rules)
Ex: increase mining reward, increase the max block size
A block invalid under old rules may be valid under new rules
Only nodes that have upgraded will accept the new blocks
All nodes MUST upgrade to avoid a “split” (often, they don’t)

![Diagram Description automatically generated](Picture4.jpg)
10

<!-- Slide number: 11 -->
# Forks with a Purpose: Soft Fork
Tightens the rules for newly created blocks
Ex: decreasing mining reward, decrease the max block size
A block valid under old rules may be invalid under new rules
All nodes (upgraded or not) will accept the new blocks
If majority nodes upgraded, old nodes don’t need to upgrade
Blockchain is unlikely to “split”
This block will become stale by the upgraded nodes (majority)

![Diagram Description automatically generated](Picture4.jpg)
11

<!-- Slide number: 12 -->
# Lecture 06Thursday, Feb 5, 2026
12

<!-- Slide number: 13 -->
# The 51% Attack
Truthful miners are adding blocks to the public chain by broadcasting them
Block 42

![A red person with black background AI-generated content may be incorrect.](Picture33.jpg)

![A red person with black background AI-generated content may be incorrect.](Picture32.jpg)
Truthful Miners
Block 38
Block 39
Block 40
Block 41

![A red person with black background AI-generated content may be incorrect.](Picture31.jpg)

Block 39
Block 40
Block 41

![A red person with black background AI-generated content may be incorrect.](Picture30.jpg)
Malicious Miner

Malicious miner: adding blocks to the private chain but not broadcasting to the public chain
13

<!-- Slide number: 14 -->
# The 51% Attack
Malicious miner: spends BTC (for buying items) and records on the truthful public chain

![A red person with black background AI-generated content may be incorrect.](Picture4.jpg)

![A red person with black background AI-generated content may be incorrect.](Picture27.jpg)

![A red person with black background AI-generated content may be incorrect.](Picture18.jpg)
Block 38
Block 39
Block 40 -16 BTC
Block 41
Block 42

![A red person with black background AI-generated content may be incorrect.](Picture17.jpg)

Block 39
Block 40
Block 41

![A red person with black background AI-generated content may be incorrect.](Picture30.jpg)

Malicious miner: excludes these transactions from his private chain – still owns BTC there!
14

<!-- Slide number: 15 -->
# The 51% Attack
Truthful miners: adding the blocks to the public truthful chain at their own rate
Hashing
Power

![A computer with a green screen AI-generated content may be incorrect.](Picture4.jpg)

![A red person with black background AI-generated content may be incorrect.](Picture33.jpg)

![A red person with black background AI-generated content may be incorrect.](Picture32.jpg)
Block 38
Block 39
Block 40
Block 41
Block 42

![A red person with black background AI-generated content may be incorrect.](Picture31.jpg)

Block 43
Block 39
Block 40
Block 41
Block 42

![A red person with black background AI-generated content may be incorrect.](Picture30.jpg)

Higher Hashing
Power
Malicious miner: adding blocks to the private chain faster owing to higher compute power

![A computer with a green screen AI-generated content may be incorrect.](Picture15.jpg)

![A computer with a green screen AI-generated content may be incorrect.](Picture16.jpg)
15

<!-- Slide number: 16 -->
# The 51% Attack
Truthful miners: they must accept the longest chain (following the protocol)

![A computer with a green screen AI-generated content may be incorrect.](Picture4.jpg)

![A red person with black background AI-generated content may be incorrect.](Picture33.jpg)

![A red person with black background AI-generated content may be incorrect.](Picture32.jpg)
Block 38
Block 39
Block 40
Block 41
Block 42

![A red person with black background AI-generated content may be incorrect.](Picture31.jpg)

![A black background with a black square AI-generated content may be incorrect.](Picture34.jpg)
Block 43
Block 39
Block 40
Block 41
Block 42

![A red person with black background AI-generated content may be incorrect.](Picture30.jpg)

Broadcast
Malicious miner: broadcasts his chain once it is longer than the public one

![A computer with a green screen AI-generated content may be incorrect.](Picture15.jpg)

![A computer with a green screen AI-generated content may be incorrect.](Picture16.jpg)
16

<!-- Slide number: 17 -->
# The 51% Attack
The old public chain is abandoned (including the spending record of the malicious miner)
Block 38
Block 39
Block 40
Block 41
Block 42

Everyone agrees on the longest chain

Block 43

![A red person with black background AI-generated content may be incorrect.](Picture33.jpg)

![A red person with black background AI-generated content may be incorrect.](Picture32.jpg)

![A red person with black background AI-generated content may be incorrect.](Picture30.jpg)

![A red person with black background AI-generated content may be incorrect.](Picture31.jpg)
Block 39
Block 40
Block 41
Block 42

What happens to the transaction in which the malicious miner had spent? Does it go back to the mempool?
Malicious miner: Can “double” spend the BTC that he already spent on the other chain
17

### Notes:
What happens to the transaction in which the malicious miner had spent? Does it go back to the mempool?
Multiple possibilities:
Malicious miner had only kept it in his mempool (not broadcasted) and had mined that block himself. After that block becomes RED (not part of the longest chain), the transaction goes back to the mempool of the malicious miner who simply removes the transaction from the mempool
If the said transaction was broadcasted and added in a block mined by someone else, it would go back to the pool and potentially could be mined again – the malicious guy can just repeat the same stuff
Immediately after the block with said transaction turns RED, the malicious miner spends that money (and may well choose to pay himself)

<!-- Slide number: 18 -->
# Evolution of Money
18

<!-- Slide number: 19 -->
# The Evolution of Money
Before the Money
Barter System

Can Make it work 3-way

![Guide to the Barter Economy &amp; the Barter System History - MindGroomers](Picture2.jpg)

![A picture containing mammal, sheep, standing, outdoor Description automatically generated](Picture5.jpg)

![](Picture6.jpg)
19

<!-- Slide number: 20 -->
# The Evolution of Money: Commodity Money
Divisible
Stable Value
Scarcity is the key

Inherently works peer-to-peer but …
Cumbersome to use for large purchases
How many silver coins are needed to buy an expensive item?

![Commodity Money Definition (9 Examples) - BoyceWire](Picture2.jpg)

![A picture containing gear Description automatically generated](Picture8.jpg)
Precious Stones
Commodity of Intrinsic Value
20

<!-- Slide number: 21 -->
# The Evolution of Money: Representative Money
Government-produced money
Backed by some precious commodity
Has little to no intrinsic value of its own
But can be exchanged for a commodity that has some intrinsic value
Easier to transact, enforced unforgeability

Value based on the backing instrument
But NOT just “some common value” that everyone agrees upon

![Text Description automatically generated](Picture4.jpg)
Often backed by Gold or Silver
21

<!-- Slide number: 22 -->
# The US Gold Reserve (Fort Knox, KY)
4583 Metric tons (about 56% of US Gold Reserves)
Federal Reserve Bank building in New York vault
Over 6000 Metric tons of Gold
More than 95% belongs to other countries

![](Picture2.jpg)

![fort knox gold reserve | How They Built Fort Knox Gold Bullion Depository #GoldBullion #GoldInvesting | Fort knox gold, Fort knox, Fort knox kentucky](Picture2.jpg)
22

<!-- Slide number: 23 -->
# The US Gold Reserve (Fort Knox, KY)
What’s inside?

![](Picture2.jpg)
23

<!-- Slide number: 24 -->
# Fort Knox Gold Reserve Value
Total reserves in USD: $541B (@ $118M per Metric ton)
About 1/8th of NVIDIA’s Market Cap (16 Sep 2025)

![ratios_chart_gold](Picture2.jpg)
Last 10 years
Gold Price: slightly < 3x
NVDA stock: slightly > 300x
24

### Notes:
In the last 10 years (Preceding Sept 16, 2025)
Slightly less than 3x increase in Gold Price
Slightly more than 300x increase in NVDA stock price

<!-- Slide number: 25 -->
# The evolution of money: Fiat money
Government-produced money (USD, Euro, PKR)
Has little to no intrinsic value of its own
It may not even be backed by some precious commodity
Value is based on what is set by the government
Money that the government guarantees as legal tender
In 1971, the US severed ties with the Gold Standard

![What is FIAT currency? - Welcome to BITCOINZ](Picture4.jpg)

![What Is Fiat Currency? - TheStreet](Picture2.jpg)
25