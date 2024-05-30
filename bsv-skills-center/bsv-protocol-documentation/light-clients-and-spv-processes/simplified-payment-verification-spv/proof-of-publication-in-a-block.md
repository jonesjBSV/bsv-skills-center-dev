---
description: proving that a transaction is present on the blockchain
---

# Proof of Inclusion in a block

When Alice makes payment to Bob, she also provides him with Merkle proof of the raw transaction input. Bob uses that to verity the transaction validity before he broadcasts the transaction to the node.

**What is the Merkle proof, what is Bob validating and what does he need to be able to perform the validation?**

Bob has the following:

1. A Block Headers Client (BHC)
2. Raw transaction
3. Merkle Proof for all the inputs present in the raw transaction

As discussed in [https://github.com/jonesjBSV/bsv-skills-center/blob/master/bsv-skills-center/bsv-protocol-documentation/light-clients-and-spv-processes/simplified-payment-verification-spv/broken-reference/README.md](https://github.com/jonesjBSV/bsv-skills-center/blob/master/bsv-skills-center/bsv-protocol-documentation/light-clients-and-spv-processes/simplified-payment-verification-spv/broken-reference/README.md "mention") a BHC is a client which interacts with the Blockchain’s Peer-to-peer network and downloads block headers from the longest chain. At any point in time, BHC can provide the latest block headers downloaded from the blockchain. The proof of validation process is described in [network-policies](../../network-policies/ "mention").

Once Bob receives the raw transaction and Merkle proof from Alice, he performs the Simplified Payment Verification, meaning that he will take every input present in the raw transaction and perform verification of the previous transaction that created this input UTXO using the provided Merkle proof.

To validate proof of publication, Bob calculates the Merkle root value using the Merkle proof and transaction data. He compares it with the corresponding block header’s Merkle root value. If there is a match, the proof of that transaction’s presence in the block/blockchain is mathematically proven and validation is successful. This is what makes BSV Blockchain so scalable; even with billions of light clients running in the node network, it will, in theory, still function well.

Once Bob validated the existence of the transactions referenced by the raw transaction on the blockchain, it considers them SPV verified. There is an additional step required here which is the validation of the script present in the previous transaction so that Bob knows that the input provided by Alice are valid. This is something that Bob delegates to mining nodes; he receives a confirmation when the node accepts the transaction as valid.

## Infrastructure Requirements

The three elements discussed above require the following infrastructure:

**Block Header Client** - 80 bytes per block × 52,416 blocks per year ≈ an increase of 4.2 MB per year

**Transaction data** - about 400 bytes for a simple p2pkh transaction

**Merkle Proof** - Approx. 1 KB, assuming 4 billion transactions in one block

As shown above, a merchant like Bob can run a light client, with minimal infrastructure, to support his usage needs for BSV Blockchain.
