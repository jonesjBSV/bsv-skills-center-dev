---
description: >-
  SPV is the magic behind p2p exchange, this is what allows two users to
  transact directly with each other and building decentralised, privacy
  preserving systems
---

# Simplified Payment Verification (SPV)

SPV is a process to verify the presence of transaction in a block. The 'payment' part of the term stems from the fact that blockchain itself is an electronic cash system, and every transaction is a payment. Even when a transaction is used to upload data onto the ledger, it still contains a small payment to the nodes to pay transaction processing fees.

To illustrate this process, we'll use a hypothetical scenario where Alice pays Bob for her coffee. Bob owns a coffee shop and accepts payment in BSV. So Alice makes the payment for her coffee using the BSV equivalent of £3.

First, let's look at the business process flow to understand the requirements of this system.

<figure><img src="https://github.com/jonesjBSV/bsv-skills-center/blob/master/bsv-skills-center/bsv-protocol-documentation/.gitbook/assets/LightClientsandSPVInfastructures_Slide01.png" alt=""><figcaption></figcaption></figure>

1. Alice orders her coffee at the counter. Bob will provide Alice with an invoice containing either a Bitcoin address or a QR code, which are Bob’s preferred methods of payment.
2. Alice creates a payment transaction using a UTXO which is large enough to cover the payment value. Alice will then provide the raw payment and Merkle proofs to Bob.
3. Bob receives and validates the transaction using the SPV process. If this is successful, he will submit the transaction to a node.
4. The node will receive the payment transaction and perform various policy checks. If successful, it accepts the payment as valid and provides acknowledgement to Bob. Simultaneously, this transaction is included by the node in their mempool, from which point it will become part of the PoW block creation process that the node participates in. Typically, the response to Bob is provided under 500ms.
5. Bob provides the payment receipt to Alice based on his payment acknowledgement.
6. Alice leaves the coffee shop with her coffee. Bob waits until the block is created and, once this is done, retrieves the Merkle proof from the node.
7. Bob could provide the Merkle proof to Alice, or Alice could also retrieve the Merkle proof from any of the nodes participating in the network.

Notice that Bob doesn’t wait for payment settlement when the block is created. He approves the payment instantly and provides the service to Alice even though the payment is still not yet confirmed within a block.\
This blockchain capability exists due to the design of the network protocol, where the first-seen rule ensures that once the payment is seen by a node, any double-spending attempts will be rejected by the nodes in the network. This is called 0-conf or zero confirmation and, due to network policies, is considered to be a safe and secure mechanism. This is also the key to the scaling of a blockchain.

We will discuss this scenario to explore what happens in the SPV process and how this methodology provides a highly scalable public blockchain. At a high level, the following elements prove the validity of a transaction:

* Proof of Publication
* Instant Payment confirmation
* Proof of Integrity

{% hint style="info" %}
SPV allows applications to have a subset of the entire Blockchain linked using the block headers and transactions of their interest
{% endhint %}
