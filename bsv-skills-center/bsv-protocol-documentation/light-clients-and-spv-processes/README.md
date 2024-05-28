---
description: Users of blockchain only need block headers, not the full blockchain
---

# Light Clients and SPV Processes

Transactions are a means used to write on to the Bitcoin Ledger. In the [Broken link](broken-reference "mention") topic we saw how various layers serving applications can be built on top of the core network of nodes which provide the base infrastructure.&#x20;

In this section, we will explore in depth the Simplified Payment Verification Process and its usage in applications known as light clients for the node network (which acts as a server of blockchain processes for these applications).

Firstly, we will explore the concept of SPV and its core features. We will then look at how it's applied in the real world and show how it is used for building light client applications.

{% hint style="info" %}
Light clients are also sometimes referred to as SPV Overlay. All the applications that interact with blockchains fall under this category. It is the SPV clients which make a blockchain decentralised as they will be recording all block headers ensuring the blockchain's integrity
{% endhint %}
