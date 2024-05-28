---
description: Data structure composition of a transaction
---

# Transaction Inputs and Outputs

A transaction is a standardised data structure encoding a transfer of some digital asset from the first party to a second party. At a high level, each transaction comprises inputs and outputs.

The inputs of a transaction consist of the following information:

1. A pointer to the record - a previous output on the ledger - that the digital asset exists.
2. The requisite unlocking condition(s) that authorise the sender (i.e. the first party) to transfer ownership of the asset (i.e. spend it). This will typically be a digital signature or a secret known only to the first party.

The outputs of a transaction each specify the following information:

1. A recipient (i.e. the second party) to whom the ownership of the digital asset is transferred.
2. The locking condition(s) that specifies how the recipient may subsequently unlock, and thus ‘spend’, the digital asset.

Each transaction to be recorded on the blockchain ledger is assigned a unique identifier (a Transaction Identifier or TxID).

<figure><img src="../.gitbook/assets/TransactionLifecycle_Slide01.png" alt=""><figcaption></figcaption></figure>

Input in the transaction is to have a set of fields that unlock funds from the previous unspent output. The nature of the unlocking process depends on the lock used when the output was created in the previous transaction (UTXO), which is being spent. There is no specific limit imposed on the number of inputs or number of outputs, but the technical limit is about 2 raised to 32 inputs. Typically, the transaction size limits imposed by miners will come into effect before the number limit is reached.

The overall data structure of a transaction is shown in the following diagram.

<figure><img src="../.gitbook/assets/TransactionLifecycle_Slide02.png" alt=""><figcaption><p>Internal data structure of a transaction</p></figcaption></figure>

{% hint style="info" %}
One of the biggest nuisances in transaction formats used in bitcoin is the usage of little endian and big endian format for different things. Always keep in mind this property as part of debugging process when developing code to build transactions.&#x20;
{% endhint %}
