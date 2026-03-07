<!-- Slide number: 1 -->

![](Picture2.jpg)

# Introduction to BlockchainCSE-355

Ahmed Akhtar
Department of Computer Science
SMCS, IBA Karachi
Spring 2026

### Notes:

<!-- Slide number: 2 -->
# Lecture 01Tuesday, Jan 20, 2026
2

<!-- Slide number: 3 -->
# Bitcoin Statistics: Jan 22, 2026
Bitcoins in circulation: 19.98 Million (over $2T market cap)
Total will be 21 Million (last will be mined about in the year 2140)
Bitcoins left to be mined: 1.02 Million (Total issued: 95.1%)
Mined Bitcoin Blocks: 933,250 yesterday; 933, 390 (this morning)
Blockchain Size: 715 GB
New Bitcoin Blocks per day (presently): 144 (on average)
New Bitcoins per day (presently): 450 (144 x 3.125)
About 4 Million Bitcoins were lost forever (estimate)
Transactions per second: 7 (VISA has about 24k)

Yet, Bitcoin is only one of the many cryptocurrencies around
3

<!-- Slide number: 4 -->
# The Cryptocurrency Avalanche
Cryptocurrencies today: 18000+ active (lot more inactive)
250+ on Coinbase and 400+ on Binance
Cryptocurrency users: (500-600)+ Million
Businesses accepting crypto payments: ~250+ listed + Paypal access
Crypto exchanges: 1000+ (some failed, some big failures!!!)

Despite the humongous growth in cryptocurrencies:
We will not cover crypto for the reasons they are famous for

Our focus: Blockchain Technology (concepts around for 30 years)
Or, more broadly, distributed ledger technology (DLT)
Around for about 40 years
4

<!-- Slide number: 5 -->
# What is a Blockchain?
Blockchain does not always mean Bitcoin
A practical introduction to the basics of blockchain
Get familiar with the common terminology and mechanisms
5

<!-- Slide number: 6 -->
# About this course
What will this course teach you?
Underlying Technologies to Construct a Blockchain
Blockchains: Properties and Pitfalls
Programmability in Blockchains: Smart Contracts
Cryptocurrencies – as a Use Case for Blockchain
Financial Applications: Stablecoins and Asset Tokenization
What it won’t?
Steps to open a crypto account in a given regime
Investment strategies [on your own or with an exchange]
What kind of regulations should be adopted
Why should one take this course?
6

### Notes:

<!-- Slide number: 7 -->
# Motivation for creating Blockchain
The growing need for digital payments led to challenges

Requiring intermediaries
Which can prohibit or reverse payment
May not always be online
The matter of double-spending
Discussion: Can you double-spend physical currency notes?
Inherent problem in payments that are both: P2P AND digital
Missing financial freedom (the bailouts of 2008)
Complicated global transactions (we need: fast and cheap)
Needed direct
P2P payments
Satoshi Nakamoto created blockchain technology in 2009
7

### Notes:
Why? Because intermediaries (banks) can censor transactions, reverse (charge back) transactions, and may not always be online
Digital P2P payments inherently suffer from double-spending – a centralized ledger works (requires a trusted 3rd party)
Satoshi witnessed failures in government-controlled monetary systems (bailouts of the 2008 financial crisis resulting from sub-prime mortgages)
Traditional banking is SLOW, EXPENSIVE, and FRAGMENTED across countries – we need: NO SWIFT, NO currency conversion delays

This was the Bitcoin blockchain – we will talk about bitcoin later

<!-- Slide number: 8 -->
# What is Blockchain?

![An open notebook with writing on it AI-generated content may be incorrect.](Picture4.jpg)
A ledger for recording data, just like databases
Used to record transactions (often financial!)
Across a network of computers (nodes)

Who initiates/generates those transactions?
Any node (a computer running software) in the blockchain network
An end user or an organization (e.g., an exchange) on their behalf

Who maintains/stores the distributed ledger?
Most nodes keep a part of the ledger
Some nodes keep a full ledger
The distributed ledger
8

### Notes:
Old-fashioned ledger is neither distributed NOR digital

<!-- Slide number: 9 -->
# Why is it called a Blockchain?
Because of its structure
Transactions are written in blocks of data
Which are somehow chained together
Through cryptographic hashing
And what is that?
Block 55
Transaction 01
Transaction 02
…
Transaction 76
Block 56
Transaction 01
Transaction 02
…
Transaction 43
Block 57
Transaction 01
Transaction 02
…
Transaction 89
9

<!-- Slide number: 10 -->
# Cryptographic Hashing
Maps an input text to a fixed-length, random-looking output
A complicated mathematical function – almost black magic
How is hash computed?
Well-known software (e.g., sha256)
Any change in input text (block data)
Significant change in hashed output
This could be some text of any length
A94D539C1
Cryptographic Hash Function
input
text
Fixed-length hash output

![A screenshot of a computer AI-generated content may be incorrect.](Picture3.jpg)

![A screenshot of a computer AI-generated content may be incorrect.](Picture4.jpg)

![A screenshot of a computer AI-generated content may be incorrect.](Picture5.jpg)
10

### Notes:
Online tools:
https://emn178.github.io/online-tools/sha256.html
https://academo.org/demos/SHA-256-hash-generator/
https://passwordsgenerator.net/sha256-hash-generator/

<!-- Slide number: 11 -->
# Chaining Blocks using Hashes
Each block contains a hash (or digest) of the previous block
Block 55
Transaction 01
Transaction 02
…
Transaction 76
<prev-hash>
Block 56
Transaction 01
Transaction 02
…
Transaction 43
B6349C62
Block 57
Transaction 01
Transaction 02
…
Transaction 89
7E9253AB
Compute the hash
B6349C62
7E9253AB
11

<!-- Slide number: 12 -->
# Hashes in a Practical Blockchain
Hashes need to meet some criteria
For example, a hash must start with 3 zeros
What if it does not meet the criteria?
The block will not be allowed

Change something in the block data
But block data is fixed (Transactions)
Include a fictitious number (NONCE)
What if the hash value still does not meet the criteria?
Block 56
Transaction 01
Transaction 02
…
Transaction 43
<prev hash>

<NONCE>
Block 56
Transaction 01
Transaction 02
…
Transaction 43
B6349C62
What to do?
7E9253AB
Hash
Keep changing NONCE until criteria met
MINING!

12

### Notes:
Explain that finding a good NONCE requires effort, hence computation and hence energy

<!-- Slide number: 13 -->
# Lecture 02Thursday, Jan 22, 2025
13

<!-- Slide number: 14 -->
# Recap: Transactions, Blocks, Hashes
Each block in a typical blockchain contains:
1) Transactions, 2) hash of previous block, and 3) NONCE

Block 57
Transaction 01
Transaction 02
…
Transaction 89
7E9253AB

<NONCE>
Block 55
Transaction 01
Transaction 02
…
Transaction 76
<prev hash>

<NONCE>
Block 56
Transaction 01
Transaction 02
…
Transaction 43
B6349C62

<NONCE>
Compute the hash
B6349C62
7E9253AB
Mining: Cycle through the NONCE to meet some hash criteria
14

<!-- Slide number: 15 -->
# What does Blockchain bring to the table?
Immutability / tamper-proof
Nearly impossible to change or roll back transactions
Ensured by hashes – we make it very hard to (re)compute the hash
Change a transaction: recompute hash (this block AND all subsequent ones)

Auditability
All transactions can be tracked and verified
All historical transactions are around and available

Decentralization
Enables autonomy and censorship resistance
Transactions without needing a central authority (such as banks!)
Reduced risk of single points of failure
What if someone actually does that?
Privacy?
Anonymity?
15

### Notes:
Who saves if someone actually does that? Decentralization comes to rescue

Transactions [verification and execution] without needing a central authority – anyone can validate

Privacy – typical blockchain (GONE!) – but ZK-based blockchain can provide privacy

<!-- Slide number: 16 -->
# Securing + Chaining of Blocks
What if the data in a block is tampered with?
Hash value changes:  leads to Unchaining
Block 57
Transaction 01
Transaction 02
…
Transaction 89
7E9253AB

9E4221DD5
Block 55
Transaction 01
Asim  Arif: $20
…
Transaction 76
<prev hash>

7A39D4F32
Block 56
Transaction 01
Transaction 02
…
Transaction 43
B6349C62

D8F4C0319
Asim  Arif: $50
Compute the hash
B6349C62
A634B331
7E9253AB
Any change in the block data can be easily detected
16

<!-- Slide number: 17 -->
# Security and Efficiency in blockchain
Can the data written on blockchain be permanently tampered?
Possible, but requires more than 50% of control
Security of financial transactions:
Has the payer authorized the transaction?
Is the payee the right person?
Can we verify transactions before writing them in a block?
Is someone trying to spend more than what they have?
How do we check this in current banking?

Can this verification be done efficiently?
Simplified Payment Verification
Digital Signatures and Public Key Cryptography
Transactions are all there
17

### Notes:
https://www.nervos.org/knowledge-base/what_is_SPV_(explainCKBot)

<!-- Slide number: 18 -->
# When to use a Blockchain?
When there is a multitude of transactions that:
Are generated (and potentially consumed) by multiple parties
Have a common interest
Need to avoid a central control (decentralization)
Discussion: How can you do financial transactions without a bank?
Consider a tribe on an island a couple of thousand years ago!

Boils down to a Multi-party consensus system
Everyone agrees that Muneeb has transferred PKR 70k to Zain
Or that food at a restaurant now ranks 3.1 out of 5
Agreement over a shared set of data
18

### Notes:
Financial transactions without a bank: a tribe on an island announces that each individual possesses 10 units of something (maybe precious stones – that we call currency) to begin with. Any transaction (for example, one stone in exchange for food) is publicly announced. This is a decentralized system. Thought: Do we really need the stones physically? Why not just agree that everyone begins with 10 precious stones that only exist virtually? AND KEEP RECORDING ALL THE TRANSACTIONS – A poor man’s blockchain

<!-- Slide number: 19 -->
# Consensus Options
Recap: Why is consensus needed?
To develop a ledger (single converged view of blockchain)

First popular consensus option: Proof of work (PoW)
Block creators purchase (and spend) energy to create blocks
In exchange, they get some reward
Block creators are called miners

Second popular consensus option: Proof of stake (PoS)
Block creators purchase (and stake) cryptocurrency
In exchange, they get a fee
Block creators are called validators
Bitcoin Blockchain
Ethereum Blockchain
19

### Notes:

<!-- Slide number: 20 -->
# Validity of a blockchain
When is a blockchain legit?
When all the blocks are valid

How do we ensure that a block is valid?
A correct hash of the previous block is present
Hash of this block meets the criteria (PoW blockchain)
All transactions in the block are valid

How do we ensure a transaction is valid?
Cryptocurrency example: Alice gives 0.3 BTC to Bob
Did Alice have the currency?
Did Alice agree?
How do we indicate that Alice agreed?
We will answer these questions soon!
20

<!-- Slide number: 21 -->
# Process: Blockchain Formation
21

<!-- Slide number: 22 -->
# Centralized Database vs Distributed Ledger

![Chart Description automatically generated](ContentPlaceholder5.jpg)

Legend:
22

<!-- Slide number: 23 -->
# DLT: An Accurate Description

![Radar chart Description automatically generated with low confidence](Picture3.jpg)
Consider four entities/nodes distributed in the network
Transaction data is generated by these nodes (and shared)
Each node builds a journal
its own version of the database
For this example: 4 journals
Journals could be different; why?

The blockchain is the unified view of individual journals

23

<!-- Slide number: 24 -->
# DLT: An Accurate Description

![Diagram Description automatically generated](Picture5.jpg)
GOAL: Different journals are in sync most of the time
Offer a shared view
Sync effort must be without a central party
What is the LEDGER?
Not the database
Mechanism of syncing different journals

![Radar chart Description automatically generated with low confidence](Picture4.jpg)
24

### Notes:

<!-- Slide number: 25 -->
# Syncing: Building consensus
Set of journals
Individual views of shared data
Convergence to a single shared view
That everyone agrees with – The distributed ledger
A ledger isn’t quite a tangible thing
Just emerges from the efforts of synchronizing individual journals

Distributed consensus (Syncing): How does that work?
Five-step process, but before that:
Building distributed consensus is HARD!
25