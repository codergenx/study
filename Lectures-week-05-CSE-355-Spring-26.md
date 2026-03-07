<!-- Slide number: 1 -->

![](Picture2.jpg)

# Introduction to BlockchainCSE-355

Ahmed Akhtar
Department of Computer Science
SMCS, IBA Karachi
Spring 2026

### Notes:

<!-- Slide number: 2 -->
# Lecture 09Tuesday, Feb 17, 2026
2

<!-- Slide number: 3 -->
# What Is a Token?
Simple Definition
A token is a digital unit of value recorded on a blockchain.

It is:
Not a coin with its own blockchain
But a programmable asset that lives on top of an existing blockchain
3

<!-- Slide number: 4 -->
# Coins vs Tokens
Coin
Has its own blockchain

Used to pay transaction fees

Example: Bitcoin, Ether

Token
Built on top of another blockchain
Uses that blockchain for security
Created via smart contracts

4

<!-- Slide number: 5 -->
# What Does a Token Represent?
A token can represent:
Money (stablecoins)
Voting rights
Access rights
Ownership shares
Loyalty points
Real-world assets
It’s just:
A programmable entry in a distributed ledger.

5

<!-- Slide number: 6 -->
# How does a token work?
On blockchains that support smart contracts like Ethereum:
A smart contract defines the token rules
The ledger records balances
Transfers are just state updates

Stablecoins are simply tokens that are designed to represent fiat money.
6

<!-- Slide number: 7 -->
# Stablecoins
The alternative use case for blockchain

Transactions involving stablecoins: on which blockchain?

Must write transactions in a ledger (to have any record)
7

### Notes:
Bitcoin tried to become money itself. Stablecoins take a different approach — they keep traditional money, but put it on a blockchain.

Stablecoins do not have their own blockchain. They are: Tokens issued on top of existing blockchains.

Even though stablecoins represent dollars: They are still digital tokens Ownership must be recorded somewhere That “somewhere” is: The blockchain ledger. Without writing to the ledger: No  proof of ownership No transfer No transaction history So the blockchain provides: Record Verification Transfer mechanism Not monetary policy.

<!-- Slide number: 8 -->
# USDC(Circle)/USDT(Tether Limited)
A stablecoin is mapped to USD because the issuer promises that 1 token = 1 USD, and backs that promise with reserves.

Step 1 — Issuance
You send $1 to the issuer
The issuer mints 1 stablecoin
That $1 is held in reserves (bank deposits, T-bills, etc.)
So now:
1 token is backed by $1 held somewhere.
Step 2 — Redemption
You return 1 stablecoin to the issuer
The issuer burns (destroys) it
You receive $1
This convertibility keeps the price anchored.
8

<!-- Slide number: 9 -->
# Arbitrage
Why market price stays near $1?

If the stablecoin trades:
Above $1 (e.g., $1.02)Traders buy from issuer for $1 and sell for $1.02 → price pushed down.
Below $1 (e.g., $0.98)Traders buy cheap and redeem for $1 → price pushed up.

This arbitrage keeps it close to $1.
9

<!-- Slide number: 10 -->
# ARTs versus EMTs

![](Picture2.jpg)
10

<!-- Slide number: 11 -->
# Bitcoin Transactions

### Notes:

<!-- Slide number: 12 -->
# Outline
Introduction
Replay attacks
UTXO Model
Bitcoin transaction format
Stack based transaction execution
Legacy transactions
Transaction malleability
Segregated witness (segwit) transactions
Merkle trees

12

<!-- Slide number: 13 -->
# Financial Transactions
What information needs to be included in a transaction?
Payer
Payee
Amount
Authorization

Payer: Alia
Payee: Babar
Amount: PKR 50,000
Authorization: SigAlia(Payer||Payee||Amount)
13

<!-- Slide number: 14 -->
# Financial Transactions
What information needs to be included in a transaction?
Payer
Payee
Amount
Authorization

Payer: Alia
Payee: Babar
Amount: PKR 50,000
Authorization: SigAlia(Hash(Payer||Payee||Amount))
14

<!-- Slide number: 15 -->
# Financial Transactions
Account-based model
Payer: Alia
Payee: Babar
Amount: PKR 50,000
Authorization: SigAlia(Hash(Payer||Payee||Amount))
Alia: PKR 100,000

Babar: PKR 0
Alia: PKR 50,000
Babar: PKR 50,000
15

<!-- Slide number: 16 -->
# Financial Transactions
Account-based model
Store list of accounts and balances
A transaction is valid if there is enough balance in the account
Payer debited, payee credited

Ethereum uses account-based model

16

<!-- Slide number: 17 -->
# Replay Attack
Account-based model

![Hacker Anonymous - Free image on Pixabay](Picture2.jpg)
Payer: Alia
Payee: Babar
Amount: PKR 50,000
Authorization: SigAlia(Hash(Payer||Payee||Amount))
Alia: PKR 100,000

Babar: PKR 0
Payer: Alia
Payee: Babar
Amount: PKR 50,000
Authorization: SigAlia(Hash(Payer||Payee||Amount))
Alia: PKR 50,000
Babar: PKR 50,000
Alia: PKR 0
Babar: PKR 100,000
17

<!-- Slide number: 18 -->
# Replay Attacks
Replay attacks can be prevented by associating  unique Identifier (SEQ) with each transaction
This number is randomly generated whenever a transaction is generated
Payer signs, m = (SEQ || Payer || Payee || Amount)
 Can check if there are multiple entries of the same SEQ Number on the block chain
Ethereum prevents replay attacks this way!!
Keeps track of the SEQ for each user and ensures that it is not reused
Bitcoin uses a different model to prevent replay attacks or double spending
Unspent Transaction Output (UTXO) model

18

<!-- Slide number: 19 -->
# Bitcoin Transaction
Unspent Transaction output (UTXO) Model
A bitcoin can only be spent once
Whenever a bit coin is spent, new coins are generated
A transaction on Bitcoin blockchain consumes an unspent coin and generates new unspent coins

19

<!-- Slide number: 20 -->
# Bitcoin Transaction
Transaction Format (legacy)
Alia paying to Babar
| INPUT Prev. Trans. ID Index ScriptSig | OUTPUT Value scriptPubKey |
| --- | --- |
| Lock\_time |  |
108 satoshis = 1 bitcoin
Unspent amount of Alia

![](Picture13.jpg)
A new coin
Alia
Babar
Set to 0 (ignored) or current block#
Alia received payment
20

<!-- Slide number: 21 -->
# Bitcoin Transaction
Transaction Format (legacy)
Alia paying to Babar
| INPUT Prev. Trans. ID Index ScriptSig | OUTPUT |
| --- | --- |
|  | Index = 0 Value scriptPubKey |
|  |  |
| Lock\_time |  |
Unspent amount of Alia

![](Picture24.jpg)
Alia
Babar
Index = 1
Value scriptPubKey
Alia

![](Picture23.jpg)

![](Picture25.jpg)

![](Picture27.jpg)
https://btcscan.org/
21

<!-- Slide number: 22 -->
# ScriptSig and ScriptPubkey

If ScriptPubKey(ScriptSig)
	then create an output

Output – make payment to payee
	lock payment to
      Hash(public key of payee)
      Pay to PubKey Hash

ScriptSig
Encodes the signature and public key of the payer

ScriptPubkey
Sequence of instructions implementing a predicate (Boolean function)
Takes ScriptSig as input
returns True if input corresponds to legitimate owner of the bitcoin, otherwise returns False

https://btcscan.org/
22

<!-- Slide number: 23 -->
# Lecture 10Thursday, Feb 19, 2026
23

<!-- Slide number: 24 -->
# ScriptSig and ScriptPubkey
ScriptSig
Encodes the signature and public key of the payer

ScriptPubkey
Sequence of instructions implementing a predicate (Boolean function)
Takes ScriptSig as input
returns True if input corresponds to legitimate owner of the bitcoin, otherwise returns False

<signature>
<public key>

OP_DUP
OP_HASH160
<H(pubkey)>
OP_EQUAVERIFY
OP_CHECKSIG

https://btcscan.org/
24

<!-- Slide number: 25 -->
# Bitcoin Transaction (legacy)
OP_DUP
OP_HASH160
<H(pubkey)>
OP_EQUAVERIFY
OP_CHECKSIG

Pay to PubkeyHash (P2PKH)
Payment is made to a public key
Pubkeys are big in size (64 bytes), a hash of pubkey is only 20 bytes
In the scriptPubKey, output (unspent bit coin) is locked to Hash of a Public key
Only payee can unlock the  unspent bit coin

https://btcscan.org/
25

<!-- Slide number: 26 -->
# Bitcoin Transaction

| Txid: 054438A Index: 1 scriptSig | Value: scriptPubkey |
| --- | --- |
| Txid: 0ABD389 Index: 3 scriptSig | Value: scriptPubkey |
Txid: 054438A

Txid: 0ABD389
26

<!-- Slide number: 27 -->
# Bitcoin Transaction Format (legacy)

![](Picture5.jpg)
27

<!-- Slide number: 28 -->
# Bitcoin Transaction
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
| INPUT Prev. Trans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c Index: 0 ScriptSig 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 | OUTPUT Index 0 Value: 0.00025302 BTC scriptPubKey: OP\_DUP OP\_HASH160 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 OP\_EQUALVERIFY OP\_CHECKSIG Index 1 Value: 0.01094000 BTC scriptPubKey: OP\_DUP OP\_HASH160 9772ba84d827ac93d719a2a40f3f5dcb8963b8ad OP\_EQUALVERIFY OP\_CHECKSIG |
| --- | --- |
Babar
Alia
Alia
Total Input:
0.00025302 +  0.01094000 + 0.00003616
= 0.01122918
Fees: 0.00003616 BTC
28

<!-- Slide number: 29 -->
# Execution
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
| INPUT Prev. Trans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c Index: 0 ScriptSig: 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 | ScriptPubKey (from Prev. Transaction) OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG Value: 0.01122918 BTC |
| --- | --- |
Alia
We need to check that the locked bitcoin in the previous transaction belong to Alia
29

<!-- Slide number: 30 -->
# Execution
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
| ScriptSig: < 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 > Alia’s Signatures < 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 > Alia’s public key ScriptPubKey: (Prev. Trans.) OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
|  |
|  |
|  |
30

### Notes:

<!-- Slide number: 31 -->
# Execution
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
| ScriptSig: < 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 > Alia’s Signatures < 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 > Alia’s public key ScriptPubKey: (Prev. Trans.) OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
|  |
|  |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
31

<!-- Slide number: 32 -->
# Execution
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
| ScriptSig: < 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 > Alia’s Signatures < 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 > Alia’s public key ScriptPubKey: (Prev. Trans.) OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
|  |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
32

<!-- Slide number: 33 -->
# Execution
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
| ScriptSig: < 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 > Alia’s Signatures < 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 > Alia’s public key ScriptPubKey: (Prev. Trans.) OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
33

<!-- Slide number: 34 -->
# Execution
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
| ScriptSig: < 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 > Alia’s Signatures < 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 > Alia’s public key ScriptPubKey: (Prev. Trans.) OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
34

<!-- Slide number: 35 -->
# Execution
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
| ScriptSig: < 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 > Alia’s Signatures < 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 > Alia’s public key ScriptPubKey: (Prev. Trans.) OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
| 76960c3d0cdf8076ecd0cc220022384475aff76e |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
35

<!-- Slide number: 36 -->
# Execution
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
| ScriptSig: < 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 > Alia’s Signatures < 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 > Alia’s public key ScriptPubKey: (Prev. Trans.) OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
| 76960c3d0cdf8076ecd0cc220022384475aff76e |
| --- |
| 76960c3d0cdf8076ecd0cc220022384475aff76e |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
36

<!-- Slide number: 37 -->
# Execution
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
| ScriptSig: < 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 > Alia’s Signatures < 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 > Alia’s public key ScriptPubKey: (Prev. Trans.) OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
| 76960c3d0cdf8076ecd0cc220022384475aff76e |
| --- |
| 76960c3d0cdf8076ecd0cc220022384475aff76e |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
37

<!-- Slide number: 38 -->
# Execution
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
| ScriptSig: < 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 > Alia’s Signatures < 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 > Alia’s public key ScriptPubKey: (Prev. Trans.) OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
|  |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
38

<!-- Slide number: 39 -->
# Execution
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
| ScriptSig: < 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 > Alia’s Signatures < 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 > Alia’s public key ScriptPubKey: (Prev. Trans.) OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
|  |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
39

<!-- Slide number: 40 -->
# Execution

![verify Digital signature](Picture2.jpg)
Tran. excluding signature
= Payer||Payee||Value
SigAlia(H(Payer||Payee||Value))
Source: https://signyourdoc.com/verify-digital-signature/
40

<!-- Slide number: 41 -->
# Execution
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
| ScriptSig: < 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 > Alia’s Signatures < 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 > Alia’s public key ScriptPubKey: (Prev. Trans.) OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
|  |
|  |
| True |
41

<!-- Slide number: 42 -->
# Bitcoin Transaction (legacy)
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
| INPUT Prev. Trans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c Index: 0 ScriptSig 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 | OUTPUT Index 0 Value: 0.00025302 BTC scriptPubKey: OP\_DUP OP\_HASH160 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 OP\_EQUALVERIFY OP\_CHECKSIG Index 1 Value: 0.01094000 BTC scriptPubKey: OP\_DUP OP\_HASH160 9772ba84d827ac93d719a2a40f3f5dcb8963b8ad OP\_EQUALVERIFY OP\_CHECKSIG |
| --- | --- |
Babar
Alia
Alia
Total Input:
0.00025302 +  0.01094000 + 0.00003616
= 0.01122918
Fees: 0.00003616 BTC
42

<!-- Slide number: 43 -->
# Bitcoin Transaction (legacy)
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
|  | OUTPUT Index 0 Value: 0.00025302 BTC scriptPubKey: OP\_DUP OP\_HASH160 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 OP\_EQUALVERIFY OP\_CHECKSIG Index 1 Value: 0.01094000 BTC scriptPubKey: OP\_DUP OP\_HASH160 9772ba84d827ac93d719a2a40f3f5dcb8963b8ad OP\_EQUALVERIFY OP\_CHECKSIG |
| --- | --- |

If ScriptPubKey(ScriptSig)
	then create output
Lock to Babar’s PubKey Hash
If transaction inputs are valid then
Lock to Alia’s PubKey Hash
43