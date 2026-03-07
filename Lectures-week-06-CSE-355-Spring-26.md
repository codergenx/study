<!-- Slide number: 1 -->

![](Picture2.jpg)

# Introduction to BlockchainCSE-355

Ahmed Akhtar
Department of Computer Science
SMCS, IBA Karachi
Spring 2026

### Notes:

<!-- Slide number: 2 -->
# Lecture 11Tuesday, Feb 24, 2026
2

<!-- Slide number: 3 -->
# Bitcoin Transaction (legacy)
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
|  | OUTPUT Index 0 Value: 0.00025302 BTC scriptPubKey: OP\_DUP OP\_HASH160 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 OP\_EQUALVERIFY OP\_CHECKSIG Index 1 Value: 0.01094000 BTC scriptPubKey: OP\_DUP OP\_HASH160 9772ba84d827ac93d719a2a40f3f5dcb8963b8ad OP\_EQUALVERIFY OP\_CHECKSIG |
| --- | --- |

If ScriptPubKey(ScriptSig)
	then create output
Lock to Babar’s PubKey Hash
If transaction inputs are valid then
Lock to Alia’s PubKey Hash
3

<!-- Slide number: 4 -->
# Bitcoin Transaction (legacy)
Multiple inputs and outputs

![](Picture4.jpg)
Alia’s output
Babar’s output
4

<!-- Slide number: 5 -->
# Bitcoin Transaction (legacy)
Unspendable Output
| INPUT Prev. Trans. ID: Index: 0 ScriptSig | OUTPUT |
| --- | --- |
|  | Index 0 Value: 0 BTC scriptPubKey: OP\_Return <any thing> |
|  | Index 1 Value: 0.00025302 BTC scriptPubKey: OP\_DUP OP\_HASH160 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 OP\_EQUALVERIFY OP\_CHECKSIG |

Unspendable Output

5

<!-- Slide number: 6 -->
# Bitcoin Transaction (legacy)
| INPUT Prev. Trans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c Index: 0 ScriptSig 304402208a09e17ddf7f3e7d1d6e18b3b42f9e445c8c6f5f2e93f993b6f6b9c5b1f3a2d702202f7d8b03c2f1763e8c5ff0b8a0b6c80b7d41d6e2a2b9df62d4a056c6bb6f23ef01 (Signature) 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 (Public Key) | OUTPUT Index 0 Value: 0.00025302 BTC scriptPubKey: OP\_DUP OP\_HASH160 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 OP\_EQUALVERIFY OP\_CHECKSIG Index 1 Value: 0.01094000 BTC scriptPubKey: OP\_DUP OP\_HASH160 9772ba84d827ac93d719 a2a40f3f5dcb8963b8ad OP\_EQUALVERIFY OP\_CHECKSIG |
| --- | --- |
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
6

### Notes:

<!-- Slide number: 7 -->
# Bitcoin Transaction (legacy)
7

<!-- Slide number: 8 -->
# Bitcoin Transaction (legacy)
8

<!-- Slide number: 9 -->
# Bitcoin Transaction (legacy)
9

<!-- Slide number: 10 -->
# Bitcoin Transaction (legacy)
10

<!-- Slide number: 11 -->
# Bitcoin Transaction (legacy)
| INPUT Prev. Trans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c Index: 0 ScriptSig 304402208a09e17ddf7f3e7d1d6e18b3b42f9e445c8c6f5f2e93f993b6f6b9c5b1f3a2d702202f7d8b03c2f1763e8c5ff0b8a0b6c80b7d41d6e2a2b9df62d4a056c6bb6f23ef01 (Signature) 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 (Public Key) | OUTPUT Index 0 Value: 0.00025302 BTC scriptPubKey: OP\_DUP OP\_HASH160 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 OP\_EQUALVERIFY OP\_CHECKSIG Index 1 Value: 0.01094000 BTC scriptPubKey: OP\_DUP OP\_HASH160 9772ba84d827ac93d719a2a40f3f5dcb8963b8ad OP\_EQUALVERIFY OP\_CHECKSIG |
| --- | --- |
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
11

<!-- Slide number: 12 -->
# Bitcoin Transaction (legacy)
| INPUT Prev. Trans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c Index: 0 ScriptSig 30450221008a09e17ddf7f3e7d1d6e18b3b42f9e445c8c6f5f2e93f993b6f6b9c5b1f3a2d702202f7d8b03c2f1763e8c5ff0b8a0b6c80b7d41d6e2a2b9df62d4a056c6bb6f23ef01 (Signature) 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 (Public Key) | OUTPUT Index 0 Value: 0.00025302 BTC scriptPubKey: OP\_DUP OP\_HASH160 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 OP\_EQUALVERIFY OP\_CHECKSIG Index 1 Value: 0.01094000 BTC scriptPubKey: OP\_DUP OP\_HASH160 9772ba84d827ac93d719a2a40f3f5dcb8963b8ad OP\_EQUALVERIFY OP\_CHECKSIG |
| --- | --- |
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c9
12

### Notes:

<!-- Slide number: 13 -->
# Bitcoin Transaction (legacy)
| INPUT Prev. Trans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c Index: 0 ScriptSig 30450221008a09e17ddf7f3e7d1d6e18b3b42f9e445c8c6f5f2e93f993b6f6b9c5b1f3a2d702202f7d8b03c2f1763e8c5ff0b8a0b6c80b7d41d6e2a2b9df62d4a056c6bb6f23ef01 (Signature) 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 (Public Key) | OUTPUT Index 0 Value: 0.00025302 BTC scriptPubKey: OP\_DUP OP\_HASH160 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 OP\_EQUALVERIFY OP\_CHECKSIG Index 1 Value: 0.01094000 BTC scriptPubKey: OP\_DUP OP\_HASH160 9772ba84d827ac93d719a2a40f3f5dcb8963b8ad OP\_EQUALVERIFY OP\_CHECKSIG |
| --- | --- |
Transaction ID: 7cc90809ea6c90899086ed8607eea8dcc1bbe2ee3fbaa662f3f597888575c4c97b9ab087c86818551aa77f59bb2c35bd774abed7fcb19c7e840b502b2604271c
13

<!-- Slide number: 14 -->
# Bitcoin Transaction (legacy)
14

<!-- Slide number: 15 -->
# Why Transaction Malleability is an issue?
Unreliable Transaction IDs
Wallets track transactions by txid
If the txid can be changed, wallets may not recognize that a confirmed transaction is the same one they sent
Double-Spend Risks
Attackers can alter a pending transaction’s signature, rebroadcast it, and miners might confirm the modified version instead of the original
Network Confusion
Nodes and users may see multiple versions of the same transaction with different IDs, creating uncertainty until one is mined

15

<!-- Slide number: 16 -->
# Why Transaction Malleability is an issue?
Breaks Layer-2 Protocols
Off-chain protocols (e.g., early payment channels, Lightning prototypes) depend on knowing exact txids
Malleability makes it impossible to pre-build transactions that rely on previous txids
16

<!-- Slide number: 17 -->
# How to prevent transaction malleability?
scriptSig = <ECDSA signature, Public key> acts as a witness proving that:
The payer has authorized this transaction
The payer can unlock the unspent output of previous transaction
To prevent transaction malleability, we need to segregate this witness from the transaction input
Segregated Witness (SegWit) transaction
Txid is not created using scriptSig
17

<!-- Slide number: 18 -->
# Bitcoin – legacy vs. SegWit Transactions
SegWit – P2WPKH
Legacy – P2PKH

![](Picture4.jpg)

![](Picture5.jpg)
18

<!-- Slide number: 19 -->
# SegWit Transaction
Pay to Witness Public Key Hash (P2WPKH)

![](Picture4.jpg)
19

<!-- Slide number: 20 -->
# SegWit Transaction – P2WPKH
| INPUT Prev. Trans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c Index: 0 ScriptSig “” | OUTPUT Index 0 Value: 0.00025302 BTC scriptPubKey: 00 14 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 Index 1 Value: 0.01094000 BTC scriptPubKey: 00 14 92fd4e32824b531e5152fa9c4b9585b74fd5fd8c |
| --- | --- |
| Witness Signature: 304402208a09e17ddf7f3e7d1d6e18b3b42f9e445c8c6f5f2e93f993b6f6b9c5b1f3a2d702202f7d8b03c2f1763e8c5ff0b8a0b6c80b7d41d6e2a2b9df62d4a056c6bb6f23ef01 Public Key: 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |  |
Babar
Alia
Alia
20

<!-- Slide number: 21 -->
# SegWit Transaction – P2WPKH
| INPUT Prev. Trans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c Index: 0 ScriptSig “” | OUTPUT Index 0 Value: 0.00025302 BTC scriptPubKey: 00 14 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 Index 1 Value: 0.01094000 BTC scriptPubKey: 00 14 92fd4e32824b531e5152fa9c4b9585b74fd5fd8c |
| --- | --- |
| Witness Signature: 304402208a09e17ddf7f3e7d1d6e18b3b42f9e445c8c6f5f2e93f993b6f6b9c5b1f3a2d702202f7d8b03c2f1763e8c5ff0b8a0b6c80b7d41d6e2a2b9df62d4a056c6bb6f23ef01 Public Key: 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |  |
No OP Codes!

Bitcoin internally expands the scriptPubKey of Prev. Trans. Output into the “virtual” script

OP_DUP   OP_HASH160    <pubKeyHash> OP_EQUALVERIFY     OP_CHECKSIG
21

<!-- Slide number: 22 -->
# Execution – P2WPKH
| ScriptSig: “ ” Witness: 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 Alia’s Signatures 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 Alia’s public key ScriptPubKey: (Prev. Trans.) 00 14 076960c3d0cdf8076ecd0cc220022384475aff76e |
| --- |
Stack
|  |
| --- |
|  |
|  |
|  |
SegWit transaction!

Expand ScriptPubKey to virtual scriptPubkey for P2WPKH
22

### Notes:

<!-- Slide number: 23 -->
# Execution – P2WPKH
| ScriptSig: “ ” Witness: 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 Alia’s Signatures 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 Alia’s public key ScriptPubKey: (Prev. Trans.) 00 14 076960c3d0cdf8076ecd0cc220022384475aff76e Virtual ScriptPubKey OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
|  |
|  |
|  |
SegWit transaction!

Expand ScriptPubKey to virtual scriptPubkey for P2WPKH
23

### Notes:

<!-- Slide number: 24 -->
# Execution  – P2WPKH
| ScriptSig: “ ” Witness: 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 Alia’s Signatures 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 Alia’s public key ScriptPubKey: (Prev. Trans.) 00 14 076960c3d0cdf8076ecd0cc220022384475aff76e Virtual ScriptPubKey OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
|  |
|  |
|  |
Push witness items to stack
24

### Notes:

<!-- Slide number: 25 -->
# Execution  – P2WPKH
| ScriptSig: “ ” Witness: 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 Alia’s Signatures 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 Alia’s public key ScriptPubKey: (Prev. Trans.) 00 14 076960c3d0cdf8076ecd0cc220022384475aff76e Virtual ScriptPubKey OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
|  |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
Push witness items to stack
25

### Notes:

<!-- Slide number: 26 -->
# Execution – P2WPKH
| ScriptSig: “ ” Witness: 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 Alia’s Signatures 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 Alia’s public key ScriptPubKey: (Prev. Trans.) 00 14 076960c3d0cdf8076ecd0cc220022384475aff76e Virtual ScriptPubKey OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
|  |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
Execute OP Codes!
26

### Notes:

<!-- Slide number: 27 -->
# Execution  – P2WPKH
| ScriptSig: “ ” Witness: 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 Alia’s Signatures 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 Alia’s public key ScriptPubKey: (Prev. Trans.) 00 14 076960c3d0cdf8076ecd0cc220022384475aff76e Virtual ScriptPubKey OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
27

### Notes:

<!-- Slide number: 28 -->
# Execution  – P2WPKH
| ScriptSig: “ ” Witness: 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 Alia’s Signatures 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 Alia’s public key ScriptPubKey: (Prev. Trans.) 00 14 076960c3d0cdf8076ecd0cc220022384475aff76e Virtual ScriptPubKey OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
| 76960c3d0cdf8076ecd0cc220022384475aff76e |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
28

### Notes:

<!-- Slide number: 29 -->
# Execution  – P2WPKH
| ScriptSig: “ ” Witness: 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 Alia’s Signatures 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 Alia’s public key ScriptPubKey: (Prev. Trans.) 00 14 076960c3d0cdf8076ecd0cc220022384475aff76e Virtual ScriptPubKey OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
| 76960c3d0cdf8076ecd0cc220022384475aff76e |
| --- |
| 76960c3d0cdf8076ecd0cc220022384475aff76e |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
29

### Notes:

<!-- Slide number: 30 -->
# Execution  – P2WPKH
| ScriptSig: “ ” Witness: 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 Alia’s Signatures 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 Alia’s public key ScriptPubKey: (Prev. Trans.) 00 14 076960c3d0cdf8076ecd0cc220022384475aff76e Virtual ScriptPubKey OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
|  |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
30

### Notes:

<!-- Slide number: 31 -->
# Execution  – P2WPKH
| ScriptSig: “ ” Witness: 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 Alia’s Signatures 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 Alia’s public key ScriptPubKey: (Prev. Trans.) 00 14 076960c3d0cdf8076ecd0cc220022384475aff76e Virtual ScriptPubKey OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
|  |
| 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |
| 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 |
31

### Notes:

<!-- Slide number: 32 -->
# Execution  – P2WPKH
| ScriptSig: “ ” Witness: 304402205e4a6ac74d35de1ffc1188f717273bada586b3de78f6844a548d548b0d27634c02207b127fa009b9d755b848772dcee21c4a05554501fd5e0d8a60ee8b9f9d13da7d01 Alia’s Signatures 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 Alia’s public key ScriptPubKey: (Prev. Trans.) 00 14 076960c3d0cdf8076ecd0cc220022384475aff76e Virtual ScriptPubKey OP\_DUP OP\_HASH160 <076960c3d0cdf8076ecd0cc220022384475aff76e> OP\_EQUALVERIFY OP\_CHECKSIG |
| --- |
Stack
|  |
| --- |
|  |
|  |
| True |
32

### Notes:

<!-- Slide number: 33 -->
# SegWit Transaction – P2WPKH
| INPUT Prev. Trans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c Index: 0 ScriptSig “” | OUTPUT Index 0 Value: 0.00025302 BTC scriptPubKey: 00 14 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 Index 1 Value: 0.01094000 BTC scriptPubKey: 00 14 92fd4e32824b531e5152fa9c4b9585b74fd5fd8c |
| --- | --- |
| Witness Signature: 304402208a09e17ddf7f3e7d1d6e18b3b42f9e445c8c6f5f2e93f993b6f6b9c5b1f3a2d702202f7d8b03c2f1763e8c5ff0b8a0b6c80b7d41d6e2a2b9df62d4a056c6bb6f23ef01 Public Key: 026a7cd9a8f65b260bd459d8c1e823110a699391cbaabb6a4304a5e680b2ab2cf8 |  |
Locked to Babar
Locked to Alia
Alia
33

<!-- Slide number: 34 -->
# Lecture 12Thursday, Feb 26, 2026
34

<!-- Slide number: 35 -->
# Multisig Transaction
Multisig – Multiple signatures
A Bitcoin transaction that requires M-of-N keys to authorize spending
Example: 2-of-3 multisig → any 2 signatures out of 3 keys are needed

Why?
Security: Protects funds even if one key is lost or stolen
Shared Accounts: Company treasuries or family accounts requiring multiple approvals
Escrow Services: Buyer, Seller, and Arbitrator in 2-of-3 setups
Lightning Network: Payment channels are built on 2-of-2 multisig outputs
35

<!-- Slide number: 36 -->
# Multisig Transaction – How it works?
1. Locking (Output Side)
Bitcoin is sent to a script:
OP_2 <PubKey1> <PubKey2> <PubKey3> OP_3   OP_CHECKMULTISIG
This script is hashed into an address (P2SH or P2WSH)
2. Unlocking (Input Side)
To spend, the spender provides:
M valid signatures (e.g., 2 signatures in a 2-of-3)
The witness script proving the locking conditions
3. Verification
Bitcoin validates: Do the provided signatures match the required keys?
36

<!-- Slide number: 37 -->
# Multisig Transaction - Format

![](Picture4.jpg)

![](Picture5.jpg)
37

<!-- Slide number: 38 -->
# Multisig Transaction – Execution
| INPUT Prev. Trans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c Index: 0 | OUTPUT Index 0 Value: 0.00025302 BTC scriptPubKey: 00 14 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 |
| --- | --- |
| Witness OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |  |
Multisig trans.
38

<!-- Slide number: 39 -->
# Multisig Transaction – Execution
| INPUT Prev. Trans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c Index: 0 | OUTPUT Index 0 Value: 0.00025302 BTC scriptPubKey: 00 14 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 |
| --- | --- |
| Witness OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |  |
Multisig trans.

Tans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c

Output:
Index 0
Value: 00026102
ScriptPubKey:
00 20 0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef

32-byte hash value follows – P2WSH
39

<!-- Slide number: 40 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
The last witness item must contain the witness script

Stack
|  |
| --- |
|  |
|  |
|  |
40

### Notes:

<!-- Slide number: 41 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Compute SHA256(<witnessScript>) and check if this is equal to the 32-byte value in the scriptPubkey of the Prev. Trans

If not equal → fail (transaction invalid)

If equal → continue

Tans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c

Output:
Index 0
Value: 00026102
ScriptPubKey:
00 20 0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef

Stack
|  |
| --- |
|  |
|  |
|  |
41

### Notes:

<!-- Slide number: 42 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Push all items in the witness on the stack except the last item, which is the witness script
Stack
|  |
| --- |
|  |
|  |
|  |
42

### Notes:

<!-- Slide number: 43 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Push all items in the witness on the stack except the last item, which is the witness script
Stack
|  |
| --- |
|  |
|  |
| 0 |
43

### Notes:

<!-- Slide number: 44 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Push all items in the witness on the stack except the last item, which is the witness script
Stack
|  |
| --- |
|  |
| <sigA>304402208a09e17ddf7f3e7…. |
| 0 |
44

### Notes:

<!-- Slide number: 45 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Push all items in the witness on the stack except the last item, which is the witness script
Stack
|  |
| --- |
| <sigC>d1d6e18b3b42f9e445c8c6f…. |
| <sigA>304402208a09e17ddf7f3e7…. |
| 0 |
45

### Notes:

<!-- Slide number: 46 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Execute the witness script
Stack
|  |
| --- |
| <sigC>d1d6e18b3b42f9e445c8c6f…. |
| <sigA>304402208a09e17ddf7f3e7…. |
| 0 |
46

### Notes:

<!-- Slide number: 47 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Execute the witness script
Stack
| 2 |
| --- |
| <sigC>d1d6e18b3b42f9e445c8c6f…. |
| <sigA>304402208a09e17ddf7f3e7…. |
| 0 |
47

### Notes:

<!-- Slide number: 48 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Execute the witness script
Stack
| <PubKeyA> |
| --- |
| 2 |
| <sigC>d1d6e18b3b42f9e445c8c6f…. |
| <sigA>304402208a09e17ddf7f3e7…. |
| 0 |
48

### Notes:

<!-- Slide number: 49 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Execute the witness script
Stack
| <PubKeyB> |
| --- |
| <PubKeyA> |
| 2 |
| <sigC>d1d6e18b3b42f9e445c8c6f…. |
| <sigA>304402208a09e17ddf7f3e7…. |
| 0 |
49

### Notes:

<!-- Slide number: 50 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Execute the witness script
Stack
| <PubKeyC> |
| --- |
| <PubKeyB> |
| <PubKeyA> |
| 2 |
| <sigC>d1d6e18b3b42f9e445c8c6f…. |
| <sigA>304402208a09e17ddf7f3e7…. |
| 0 |
50

### Notes:

<!-- Slide number: 51 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Execute the witness script
Stack
| 3 |
| --- |
| <PubKeyC> |
| <PubKeyB> |
| <PubKeyA> |
| 2 |
| <sigC>d1d6e18b3b42f9e445c8c6f…. |
| <sigA>304402208a09e17ddf7f3e7…. |
| 0 |
51

### Notes:

<!-- Slide number: 52 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Execute the witness script
Stack
| 3 |
| --- |
| <PubKeyC> |
| <PubKeyB> |
| <PubKeyA> |
| 2 |
| <sigC>d1d6e18b3b42f9e445c8c6f…. |
| <sigA>304402208a09e17ddf7f3e7…. |
| 0 |
52

### Notes:

<!-- Slide number: 53 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Pop
n = 3
Stack
| <PubKeyC> |
| --- |
| <PubKeyB> |
| <PubKeyA> |
| 2 |
| <sigC>d1d6e18b3b42f9e445c8c6f…. |
| <sigA>304402208a09e17ddf7f3e7…. |
| 0 |
53

### Notes:

<!-- Slide number: 54 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Pop 3 public keys
n = 3
<PubKeyC>
<PubKeyB>
<PubKeyA>

Stack
| 2 |
| --- |
| <sigC>d1d6e18b3b42f9e445c8c6f…. |
| <sigA>304402208a09e17ddf7f3e7…. |
| 0 |
54

### Notes:

<!-- Slide number: 55 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Pop
n = 3
<PubKeyC>
<PubKeyB>
<PubKeyA>
m=2

Stack
| <sigC>d1d6e18b3b42f9e445c8c6f…. |
| --- |
| <sigA>304402208a09e17ddf7f3e7…. |
| 0 |
55

### Notes:

<!-- Slide number: 56 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
Pop 2 signatures
n = 3
<PubKeyC>
<PubKeyB>
<PubKeyA>
m=2
<sigC>d1d6e18b3b42f9e445c8c6f….
<sigA>304402208a09e17ddf7f3e7….

Stack
| 0 |
| --- |
56

### Notes:

<!-- Slide number: 57 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |

n = 3
<PubKeyC>
<PubKeyB>
<PubKeyA>
m=2
<sigC>d1d6e18b3b42f9e445c8c6f….
<sigA>304402208a09e17ddf7f3e7….
verify(sigC, [A,B,C]) → valid (matches C)
Stack
| 0 |
| --- |
57

### Notes:

<!-- Slide number: 58 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |

n = 3
<PubKeyC>
<PubKeyB>
<PubKeyA>
m=2
<sigC>d1d6e18b3b42f9e445c8c6f….
<sigA>304402208a09e17ddf7f3e7….
verify(sigC, [A,B,C]) → valid (matches C)
verify(sigA, [A,B,C]) → valid (matches A)
Stack
| 0 |
| --- |
58

### Notes:

<!-- Slide number: 59 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |

n = 3
<PubKeyC>
<PubKeyB>
<PubKeyA>
m=2
<sigC>d1d6e18b3b42f9e445c8c6f….
<sigA>304402208a09e17ddf7f3e7….
verify(sigC, [A,B,C]) → valid (matches C)
verify(sigA, [A,B,C]) → valid (matches A)
count(valid) = 2 = m → success
Stack
| 0 |
| --- |
59

### Notes:

<!-- Slide number: 60 -->
# Mutisig Execution – P2WSH
| Witness: OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |
| --- |
verify(sigC, [A,B,C]) → valid (matches C)
verify(sigA, [A,B,C]) → valid (matches A)
count(valid) = 2 = m → success

POP 0 (CHECKMULTISIG bug), then PUSH TRUE
Stack
| TRUE |
| --- |
60

### Notes:

<!-- Slide number: 61 -->
# Multisig Transaction – Execution
| INPUT Prev. Trans. ID: 0f07ec1c3738873cd6336f0e2c92094bf08d0ad3bce8aba0efa2eb9d172fd60c Index: 0 | OUTPUT Index 0 Value: 0.00025302 BTC scriptPubKey: 00 14 2fa9c4b9585b74fd5fd8c92fd4e32824b531e515 |
| --- | --- |
| Witness OP\_0 <sigA>304402208a09e17ddf7f3e7…. <sigC>d1d6e18b3b42f9e445c8c6f…. <witnessScript> OP\_2 <PubKeyA> <PubKeyB> <PubKeyC> OP\_3 OP\_CHECKMULTISIG |  |
Multisig trans.
Transaction validated!!
61

<!-- Slide number: 62 -->
# Bitcoin Transaction
How can you verify the correctness of a transaction, included in some block?
e.g., a vendor would like to verify the following customer transaction before delivering the merchandize
TXID: 7b9ab087c86818551aa77f59bb2c35bd774abed7fcb19c7e840b502b2604271c
Block No. 720,518
Verification Steps
Check Inclusion
Confirm that the transaction with this TXID is part of Block No. 720,518
Validate Block Integrity
Ensure this transaction’s hash contributes to the overall block hash
This guarantees that if the transaction were missing or altered, the block hash would no longer match
3. Confirm Block Validity
Verify that Block No. 720,518 itself is valid and part of the longest chain

62

<!-- Slide number: 63 -->
# Block Hash
Prev Block Hash
Hash(Tx 1)

Tx 1

Hash(Tx 2)
Tx 2
Aggregate Tx Hash
Block Hash
Hash(Tx 3)
Tx 3

Nonce

Hash(Tx n)
Tx n
63

<!-- Slide number: 64 -->
# Block Hash
Verify that some transaction, say Tx 2, is included in some block
Prev Block Hash
Hash(Tx 1)

Tx 1

Hash(Tx 2)
Tx 2
Aggregate Tx Hash
Block Hash
Hash(Tx 3)
Tx 3

Nonce

Hash(Tx n)
Tx n

Aggregate Tx Hash
64

<!-- Slide number: 65 -->
# Block Hash – Merkle tree
Nonce
Prev. Block Hash
Aggregate Transaction Hash
Merkle Root Hash
Hash(…)
Hash (…)
Hash(3,4)
Hash(1,2)
Hash(n-1,n)

Hash(Tx 4)
Hash(Tx 3)
Hash  (Tx n-1)
Hash (Tx n)
Hash(Tx 1)
Hash(Tx 2)

Tx 4
Tx 3
Tx n
Tx n-1
Tx 1
Tx 2

65

<!-- Slide number: 66 -->
# Block Hash – Merkle tree
Nonce
Prev. Block Hash
Aggregate Transaction Hash
Verify that some transaction, say Tx 2, is included in some block
Merkle Root Hash
Hash(…)
Hash (…)
Hash(3,4)
Hash(1,2)
Hash(n-1,n)

Hash(Tx 4)
Hash(Tx 3)
Hash  (Tx n-1)
Hash (Tx n)
Hash(Tx 1)
Hash(Tx 2)

Tx 4
Tx 3
Tx n
Tx n-1
Tx 1
Tx 2

66

### Notes:
https://hackernoon.com/merkle-trees-181cb4bc30b4

Simplified Payment Verification (SPV)
Simplified Payment Verification (SPV) is a method of verifying if particular transactions are included in a block without downloading the entire block. Merkle trees are used extensively by SPV nodes.
SPV nodes do not have data from all transactions in a block. They only download block headers. Merkle trees enable SPV nodes on the blockchain to check if miners have verified the transactions in a block without downloading all the transactions in a block. This method is currently used by some lightweight Bitcoin clients.

<!-- Slide number: 67 -->
# Merkle Tree
Summarizes transactions
All transactions in a block are combined into one hash (the Merkle root) stored in the block header.
Enables lightweight verification (SPV)
Clients can verify a transaction is in a block using a Merkle proof (only log₂(N) hashes, not the whole block).
Detects tampering
Changing even one transaction alters the Merkle root → invalidates the block.
Improves scalability
Proof size is small (≈ log₂(N)), even if the block has thousands of transactions.

67