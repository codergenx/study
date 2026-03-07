<!-- Slide number: 1 -->

![](Picture2.jpg)

# Introduction to BlockchainCSE-355

Ahmed Akhtar
Department of Computer Science
SMCS, IBA Karachi
Spring 2026

### Notes:

<!-- Slide number: 2 -->
# Lecture 03Tuesday, Jan 27, 2026
2

<!-- Slide number: 3 -->
# Building consensus: step by step
If Alia wants to pay Babar, typically Alia will launch the transaction
Validators will put unconfirmed transactions in their LOG after validation
A miner or record producer will create the “potential” next block
The potential next block will be verified and made part of the journal
The effort to synchronize all individual journals results in the LEDGER

![Timeline Description automatically generated](ContentPlaceholder5.jpg)
3

<!-- Slide number: 4 -->
# How is a block added to the blockchain?

![Bitcoin, blockchain, cryptocurrency, transaction icon - Download on Iconfinder](Picture6.jpg)

![](Picture35.jpg)

![Proof, work, bitcoin, bitcoin mining, miner, mining, proof of work icon - Download on Iconfinder](Picture4.jpg)
Miner

![](Picture2.jpg)

![](Picture34.jpg)

![](Picture39.jpg)
Mining
Transaction
collects new transactions
User A
H(prev hash, Tx, nonce) < Target
block is added to chain

![](Picture37.jpg)

![](Picture51.jpg)

![](Picture60.jpg)

![](Picture53.jpg)
H(prev hash, nonce,  Tx) < Target
new blocks  added to chain using the hash of previously accepted block

![](Picture1.jpg)
Adding a subsequent block is implicit consent
4

<!-- Slide number: 5 -->
# Data Lifecycle: Stages to Consensus
Transaction – initiated and propagated by end users
Any proposed change to the ledger (broadcasted to the network)
LOG – created by auditors (or validating nodes)
Set of valid yet unconfirmed transactions put in LOG
Each auditor has their own log/mempool
Record – created by special nodes (miners or record producers)
Arbitrarily select a set of transactions from their log
Put the selected transactions into a candidate record and broadcast that candidate record to all nodes they are connected to
Journal – locally created by each node that receives the record
If the candidate record complies with protocol rules
Ledger emerges from the set of journals
5

<!-- Slide number: 6 -->
# Recap: building consensus

![](ContentPlaceholder5.jpg)

6

<!-- Slide number: 7 -->
# Characteristics of an ideal blockchain / DLT
Shared recordkeeping
Multiple entities writing data
Multi-party consensus
All parties must come to an agreement
Independent validation
Every auditor (fully validating node) should be able to recompute (and thus verify) the entire state of the system
Tamper evidence
Participants can trivially detect non-consensual changes to records
Example of such changes? How detected?
Tamper resistance
Hard for a single entity to tamper past records (transaction history)
7

<!-- Slide number: 8 -->
# History: Byzantine Generals Problem
Several divisions of the Byzantine army
Camped outside an enemy city
Each division commanded by its own general
Generals must agree upon
A common battle plan

![](Picture4.jpg)

![](Picture2.jpg)
Some of them may be traitors – will prevent loyal generals from reaching an agreement
8

<!-- Slide number: 9 -->
# History: Byzantine Generals Problem
Battalions of Byzantine army, each led by their own General
If Generals attack collectively: they will win, else will lose (likely)
Need: consensus between the Generals (multi-party consensus)
What may hinder this? (the challenges)
The Messengers sent among the Generals, may:
Be intercepted by the enemy
Only reach some generals but not all
Accidentally relay incorrect message
Forge a message maliciously
Be told a wrong message by a malicious General
Consensus building is hard. What options do we have?
9

### Notes:

<!-- Slide number: 10 -->
# How this situation relates to computing systems?
Decentralized computing systems may encounter byzantine faults
Broken hardware
Congested network
Disconnected nodes
Incorrect processing of requests
Corrupted local states
Nodes producing inconsistent output
A set of nodes launching a malicious attack
Similar issues as faced by the Byzantine Generals Problem
Byzantine fault tolerance
A measure of the capability to prevent/tolerate byzantine failures
Bitcoin blockchain: first to solve for unknown number of Generals
10

<!-- Slide number: 11 -->
# Techniques used in Bitcoin Blockchain
Public-key cryptography
Used for unforgeable digital signatures from authenticated sources
Authenticates Generals and Prevents messengers from forging

Atomic broadcast of all transactions
No General missed from receiving the transaction

Proof of Work (PoW)
Malicious Generals will have to pay a hefty price for deceiving

Tampering of a block becomes harder and harder – Chaining
Every new block further cements the past transactions
11

<!-- Slide number: 12 -->
# Blockchain: How does it get built up?
The longest chain is picked
Is there a situation when one has to “pick” from a choice of chains?

Forks
Temporarily different views of journals

Finality
A transaction becomes “final” only after multiple confirmations
Why?
Since forks can temporarily reorder or exclude it
12

<!-- Slide number: 13 -->
# Types of blockchain
Permissionless (must be public)
Examples: Bitcoin and Ethereum
Anyone can join/leave at will at any time
No central entity managing the membership
Globally readable (anyone can be a reader)

What about privacy and anonymity?
Privacy? Compromised by design (need auditability)
Anonymity? Feasible with cryptographic procedures
13

### Notes:

<!-- Slide number: 14 -->
# Permissionless vs. Permissioned
|  | Public | Private |
| --- | --- | --- |
| Permissionless | Anyone can read or write (i.e., update the ledger) |  |
| Permissioned | Anyone can read but only authorized nodes can write | Nodes can read or write based on their authorization |

14

<!-- Slide number: 15 -->
# When (not) to use a Blockchain?
Need to store state?
Multiple writers?
Online TTP Always available?
All writers known?

Permissionless Blockchain
YES
YES
NO
NO
NO
NO
YES
YES
All writers trusted?

Public verifiability needed?

YES
Public Permissioned
NO
YES
NO

Private Permissioned
DO NOT USE Blockchain!
15

### Notes:
TTP == Trusted Third Party
Permissionless: Bitcoin, Ethereum, BASE
Public Permissioned: Hedera Hashgraph, Ripple (governing council: Google, IBM, LG, etc.)
Private Permissioned: JPMorgan

<!-- Slide number: 16 -->
# Cryptocurrencies: A blockchain use case
The relation between Bitcoin and Blockchain?
What do miners “mine”? – (Is it like GOLD mining?)
Miners mine (i.e.,  create and add) blocks in a blockchain
What is a bitcoin (BTC), then?
It is a digital (crypto)currency – tradeable on its own blockchain
Via transactions recorded on that blockchain
The Bitcoin blockchain rewards miners with Bitcoins
When they create a new block that is accepted via consensus
Where do those new Bitcoins come from? – the protocol
The system simply writes a transaction on the blockchain
16

<!-- Slide number: 17 -->
# Lecture 04Thursday, Jan 29, 2026
17

<!-- Slide number: 18 -->
# Bitcoin Transaction: Step by Step
User initiates the transaction
Typically, from their wallet or crypto exchange application

Transaction broadcast for “execution”

Placed in a pool of “unconfirmed transactions”
Multiple local pools rather than one giant pool
Waiting to be picked up by “Miners” / nodes

Why will miners pick up? Incentive?
Reward for mining (Subsidy rewards + Transaction fees)
18

<!-- Slide number: 19 -->
# Bitcoin Transaction: Step by Step
Miner(s) pick up unconfirmed transaction(s)
Many-to-many paradigm
One transaction may be picked by multiple miners
A miner may pick multiple transactions to put those in one “block”(max ~1MB on the Bitcoin blockchain)
Blocks are created and stored by the miners/nodes

Miners solve the block for an eligible hash (candidate record)
Search over the nonce space
An eligible hash (hard to find, easy to verify)
A correct hash is the Proof of work
19

<!-- Slide number: 20 -->
# Bitcoin Transaction: Step by Step
Broadcasting the solution
A successful miner broadcasts the solution (block+hash)
Signature verification
Other miners verify the hash (easy!)
Consensus algorithm to agree
Block added to the blockchain (to their own journal, in fact)
Confirmation
Additional blocks added after this one
Subsidy rewards – available to spend after 100 confirmations
On receiving a block, Miners must start afresh on a new block using the hash of the latest-found block as part of the data. Why?
20

### Notes:
Last point: On receiving a block, Miners must start afresh on a new block using the hash of the latest-found block as part of the data [instead of continuing with what block number they were working on]. Why?
Answer: Because if you received block 53 and continue to mine 53, many others will be creating block 54 and someone might create block 54 before you create your own version of block 53. Effort wasted!

<!-- Slide number: 21 -->
# Bitcoin: Ownership and Transactions
The cryptocurrency (BTC) is always locked
To the owner

Transaction
payer unlocks (only they can!) and
then locks again for the payee (only they will be able to unlock!)

Minting of new BTC
Happens only at block creation (and at no other times)
Gets locked to the creator of the block
21

<!-- Slide number: 22 -->
# BTC and Fiat
How did BTC get related to Fiat currency?

Historical Fact: The New Liberty Standard Exchange recorded the first exchange of BTC for fiat (dollars) in late 2009

What was the transaction?
Users (on the BitcoinTalk forum) traded 5,050 bitcoins
For how much?
Total value: $5.02 (sent via PayPal) @ $0.00099 per BTC
The average per BTC price last month ~ $89,000 (Jan 2026)
22

<!-- Slide number: 23 -->
# Understanding Blockchains
Cryptographic Hashing
Digital Signatures
Consensus
23

<!-- Slide number: 24 -->
# Hash Function: Properties
Input: arbitrary size plain text
Output: fixed size message digest
Output is “random” looking
Not random (actually, deterministic)
About half ones and half zeros
Avalanche effect
Change one bit in the input; about half the output bits change
Preimage resistance
Given Y, can’t find X such that Hash(X) = Y
Collision resistance
Can’t find X, Z such that X ≠ Z and Hash(X) = Hash(Z)

Online tools or your OS can quickly compute Hash functions
This could be some text of any length
A94D539C1
Cryptographic Hash Function
input
text
Fixed-length hash output
24

<!-- Slide number: 25 -->
# What is needed for a transaction?

![](Picture3.jpg)
Compare with a check

Payer
Payee
Amount
Authorization

Can this check be honored?
Does the account have this much?
Account balance is checked offline

![](Picture2.jpg)
Public key 0xc7b2f68...
Public key 0xa8fc93875a972ea
Signature 0xa87g14632d452cd
What is needed for a blockchain transaction?
25

### Notes:
Before talking about digital signatures –

For Blockchain transactions: Amounts are ALWAYS locked. Payer can unlock their amount and send it to the payee by LOCKING it to the payee public address

<!-- Slide number: 26 -->
# Digital Signatures
What are they?
Like manual signatures, but different for each occurrence
Why are they needed [in blockchains]?
Authenticate the sender (end user who broadcasts transactions)
Avoid forgery in the message sent to the receiver (transactions)
In a transaction, we also need to:
Identify the receiver (or at least the address of the receiver)

How do digital signatures work?
Using public key cryptography infrastructure
26

### Notes:
FIX

<!-- Slide number: 27 -->
# What is Cryptography?
GOAL: Send message that a spy is unable to make sense of!

![Timeline Description automatically generated](Picture4.jpg)
Symmetric Key Cryptography
Big Challenge:

key sharing
Alice
(sender)
Bob
(receiver)

Encode
Decode
Garbage
for a spy
Thought Question:
If Bob receives some data

Can he be sure it came from Alice?
Symmetric: same shared key for encryption and for decryption
27

### Notes:
The answer to the thought question is NO. Kevin does not know the symmetric key but he can send some garbage data  Bob will decode/decrypt and will get something that will also be garbage  Bob has no way of knowing it did not come from Alice

<!-- Slide number: 28 -->
# Public Key Infrastructure and Digital Signatures
Governed by three functions

Generate Keys() – a publicKey, privateKey pair is generated
A key is nothing more than a sequence of bits

Sign(message, privateKey) – sender will do it
Function output is the signature
Signature along with message is sent (sent where?)

Verify(message, signature, publicKey) – receiver will do it
Function output is Boolean (Verified or Not)

28

### Notes:
Signature along with message is sent (sent where?)

Sent to the receiver in general – or to the pool of unconfirmed transactions in blockchain