---
description: Understanding transaction bitwise
---

# Constructing a transaction

We have already looked at the composition of a transaction. Now, let's dig a bit deeper. The following table shows the data structure of a transaction.

| Field                                                                                | Description                                                                                                      | Size                                               |
| ------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| Version no                                                                           | currently 2                                                                                                      | 4 bytes                                            |
| In-counter                                                                           | positive integer VI = [VarInt](https://wiki.bitcoinsv.io/index.php/VarInt)                                       | 1 - 9 bytes                                        |
| list of inputs                                                                       | [Input Structure](https://wiki.bitcoinsv.io/index.php/Bitcoin\_Transactions#Format\_of\_a\_Transaction\_Input)   | \<in-counter> qty with variable length per input   |
| Out-counter                                                                          | positive integer VI = [VarInt](https://wiki.bitcoinsv.io/index.php/VarInt)                                       | 1 - 9 bytes                                        |
| list of outputs                                                                      | [Output Structure](https://wiki.bitcoinsv.io/index.php/Bitcoin\_Transactions#Format\_of\_a\_Transaction\_Output) | \<out-counter> qty with variable length per output |
| [nLocktime](https://wiki.bitcoinsv.io/index.php/NLocktime\_and\_nSequence#nLockTime) | if non-zero and sequence numbers are < 0xFFFFFFFF: block height or timestamp when transaction is final           | 4 bytes                                            |

The following image provides an example of a typical raw transaction (P2PKH transaction with two inputs and two outputs):

<figure><img src="../.gitbook/assets/P2PKH transaction with two inputs and two outputs.png" alt=""><figcaption></figcaption></figure>

The colours help to differentiate every field present in the transaction. Input script is denoted as scriptSig, and output script is denoted as scriptPubKey (due to the nature of the input script being a signature and output being a script locking the funds to a public key).

As shown in the attachment below, each field in the transaction is modularised i.e. you can build a raw transaction one by one by adding each of these fields in the right format and endianness. These transactions are usually built using well-defined libraries and functions available in various programming languages.&#x20;

{% file src="../.gitbook/assets/txbits.xlsx" %}

There will often be visualisation tools which will present the transaction details in a much more readable format; for example, below is the translated version of the input and output scripts for the raw transactions in discussion.

<figure><img src="../.gitbook/assets/TransactionLifecycle_Slide07 (1).png" alt=""><figcaption></figcaption></figure>

Once the transaction is constructed, it is submitted to a mining node. This can be done using the RPC endpoint (called bitcoind), which is made available by the mining nodes to users. Some mining nodes also use a service component built on top of bitcoind called Merchant API or mAPI. mAPI provides a REST interface for broadcasting a transaction and returns the Merkle Proof of the transaction once the block is mined. Either way, the broadcasting of transaction is a responsibility of the user who uses either of the methods mentioned above.

