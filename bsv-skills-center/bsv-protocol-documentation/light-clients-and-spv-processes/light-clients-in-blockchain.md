---
description: >-
  Blockchain is truly decentralised when records and information that are
  contained within it are sent via SPV, IP to IP or person-to-person and
  transactions are maintained by their owners
---

# SPV Wallets

A truly global blockchain is one where the blockchain network not only demonstrates a large transaction processing capability, but it is also able to account for how it can scale.

Something that is commonly misunderstood concerning blockchains is that businesses and users who want to utilise blockchain for their applications need to run a node. This puts a heavy infrastructure burden on businesses to start building Web3 solutions. If they choose to use a service provider for this, they too face the same situation and this creates a bottleneck when it comes to using blockchain.

> _Quoting_ Satoshi Nakamoto -
>
> _"The design outlines a lightweight client that does not need the full block chain. In the design PDF it's called Simplified Payment Verification. The lightweight client can send and receive transactions, it just can't generate blocks. It does not need to trust a node to verify payments, it can still verify them itself._
>
> _The lightweight client is not implemented yet, but the plan is to implement it when it's needed. For now, everyone just runs a full network node._
>
> _I anticipate there will never be more than 100K nodes, probably less. It will reach an equilibrium where it's not worth it for more nodes to join in. The rest will be lightweight clients, which could be millions._
>
> _At equilibrium size, many nodes will be server farms with one or two network nodes that feed the rest of the farm over a LAN._"

The solution lies somewhere in the middle; it shouldn't be necessary to run a node or use third-party services. With light clients, there is no need for a business to run a node This is because light clients offer all the features they need to be able to use blockchain whilst also minimising use of infrastructure. The biggest benefit is that there are no limitations on scaling the application usage of blockchain.

In terms of network topology, scaling happens at edges, not at nodes. Of course, nodes need to scale to be able to support global transaction volume, which is discussed in detail in the section: [Unbounded scaling.](https://github.com/jonesjBSV/bsv-skills-center/blob/master/bsv-skills-center/bsv-protocol-documentation/light-clients-and-spv-processes/broken-reference/README.md)

When any application is looking to utilise blockchain for data or payment transactions, they will need a set of components that enables them to read and write to the blockchain. You can find out more about the context of application and utility layers with blockchain networks in [https://github.com/jonesjBSV/bsv-skills-center/blob/master/bsv-skills-center/bsv-protocol-documentation/light-clients-and-spv-processes/broken-reference/README.md](https://github.com/jonesjBSV/bsv-skills-center/blob/master/bsv-skills-center/bsv-protocol-documentation/light-clients-and-spv-processes/broken-reference/README.md "mention").

{% hint style="info" %}
The blockchain system allows pruning but also equally, you can use SPV in the block header and the Merkle proof to prove the full existence and probity of all transactions till the Genesis on your system. This utilises the block headers and causes no overhead to miners/nodes. You can charge customers for the service.
{% endhint %}

There are no strict definitions of what a light client should be designed as except for the fact that these applications will typically be either running the SPV infrastructure themselves or they will connect to service providers who do it on their behalf. This makes every application that is not a node creating blocks a light client. The term 'client' is analogous to the client role in client-server architecture used in web applications where the central node network acts as a blockchain server, and every other application becomes its client.

The overall view of the blockchain network will show the network having only a small number of nodes at the core. Most of the other applications will function as light clients.

<figure><img src="https://github.com/jonesjBSV/bsv-skills-center/blob/master/bsv-skills-center/bsv-protocol-documentation/.gitbook/assets/LightClientsandSPVInfastructures_Slide08%20(1).png" alt=""><figcaption></figcaption></figure>

The diagram shows the overall network topology identifying everything except from the nodes as light clients.

**What will these applications look like?**

Applications, whether they are hosted in a data centre or a cloud platform, will include some components which allow them to interact with blockchain. Note that these applications will predominantly be focused only on writing transactions to the blockchain. They shouldn't need to read data written on the blockchain as they can store all of their transactions with the Merkle proof themselves.

The infrastructure requirements of a client application’s blockchain are:

1. Block Headers client
2. Wallet with, at minimum, the following capabilities:
   1. Key Management
   2. Signing transactions
   3. Wallet functionality like backup and storage of keys, user identity and data
   4. UX/UI as per feature requirements
3. Transaction manager (could be part of wallet itself)
   1. Transaction creation and building custom transaction scripts
   2. Transaction broadcaster to nodes
   3. Merkle proof retriever and storage
   4. SPV process validator
   5. Signature and script validator

Most applications which are using these components will need to either design the components based on their own needs or use the services offered by a third party.

Reading Blockchain transactions in most cases will not be necessary, however there may be some scenarios where this might be desirable. One such case concerns the wallet itself, which stores keys and will need to provide the ability to restore transactions. In this situation the wallet will need to index all of the transactions that are part of the keys that it is hosting and, when required, may want to download all the transactions and their Merkle proof. The following might also be required:

1. Indexing service
2. Raw transaction data
3. Merkle proof data

Most of the nodes provide API endpoints with these services. Many of them provide a large set of API endpoints for various requirements such as UTXO services, broadcasting endpoint, transaction and block data retrieval and more. Some of these services are provided by the Block Explorer, one of the most commonly-used services for reading the blockchain. They currently exist in a form where they provide not just blockchain information but also analytics on blockchain data. Many of them are free, however as the size of the blockchain increases, these services will develop business models which include charging fees.

The Bitcoin Association provide a reference implementation as a good starting point for such infrastructure. The following diagram provides an overview of this implementation.

<figure><img src="https://github.com/jonesjBSV/bsv-skills-center/blob/master/bsv-skills-center/bsv-protocol-documentation/.gitbook/assets/image%20(17).png" alt=""><figcaption></figcaption></figure>

Aptly called LiteClient, this contains most of the elements that have been discussed in this section. The LiteClient toolbox consists of:

* A simple web wallet
* Block headers client
* A transaction builder and broadcaster
* mAPI (component to interact with node RPC endpoint to receive broadcasted transaction)
* Paymail (a user readable email like address to simplify public key usage in user experience)
* A complete library for performing most of the SPV processes and wallet functions

Further details can be found at: https://docs.bitcoinsv.io/introduction/liteclient-toolbox

{% hint style="info" %}
Blockchain is not decentralised because it has a peer network for miners. It is not decentralised because lots of permission-less running of node. Rather, what made it into a decentralised system of exchange was the fact that you could do SPV and IP to IP transactions. Decentralised and without intermediaries means that Alice and Bob can communicate directly. For example, Alice can exchange a transaction with Bob, and Bob can send the transaction to be registered. That is how you make a decentralised system. The nodes form a distributed intermediary, but they are not decentralised or involved in creating a decentralised exchange. It is rather the direct transmission from Alice to Bob without the nodes that makes a Blockchain decentralised.
{% endhint %}
