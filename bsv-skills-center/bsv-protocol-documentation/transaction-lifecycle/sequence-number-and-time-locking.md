---
description: >-
  Non-Final transactions allow for trade negotiation while still using
  blockchain transactions, or even to build side-chains like a payment channel
  and private ledgers
---

# Sequence Number and Time Locking

Every input in a transaction contains a field titled nSequence. This is a 4-byte field, i.e., it can hold 2^32 values (0x00000000 to 0xFFFFFFFF). While nLockTime allows creation of a transaction which will only become valid at a future date and time specified in the field or at a specified block height. Once the date/time mentioned in the nLockTime happens, the transaction, even if it has a non-final state due to a lesser than maximum nSequence value, will be considered final.

Sequence numbers were designed to be used for transaction replacement before a transaction was finalised. Let us see how are they used by looking at an example.&#x20;

* Alice sends a transaction where the nLockTime value is set to a date in the future. We can start with anything, but by default we would start at a sequence number of 0.
* The miners will not recognise this transaction to be valid, and thus, it is not “final”. The network of miners will not include it in a block before it is final, and that will only occur when the nLockTime value has been reached.
* As the transaction cannot be included in a block until the time specified in the nLockTime is reached, there is a final state that both parties have agreed to and also the ability to send updated transactions. If there is a 2-of-3 address (known as multi-sig), the parties can use an escrow (such as a licensed shared registry) to ensure that a transaction that has been agreed is final. If not, we can also have the parties negotiate and allow a means to “pull out” of the negotiation at any time before the nLockTime deadline.
* Using this method, and prior to when the set nLockTime is reached, the users can replace the transaction with a higher-version transaction. A higher sequence number is a newer version that replaces the ones before. That is, the network will accept the highest sequence number for transactions once the nLockTime has been reached, rejecting all others with a lower value.
* The negotiations can also be finalised. If a party sets the sequence number to UINT\_MAX, the transaction is considered as being finalised by the miners. No replacement can occur. When the sequence equals UINT\_MAX, miners will no longer accept a replacement transaction even where the nLockTime value remains in the future.
* If you ever want to lock the transaction permanently, you can set the sequence number to UINT\_MAX. Then the transaction is considered to be final, even if the time represented in nLockTime remains in the future.

This feature allows two (or more) negotiating parties to create and sign a prepared transaction.

* These prepared transactions can be negotiated, agreed, and signed by the the parties allowing them to move money between each other. This can allow for a base agreement and payment stream. This is conducted securely and without fees — the fees paid are to the miners for the settled transaction, not the exchange.
* Extending this would allow for a range of services to be created that involve users withdrawing and depositing funds into a service without waiting for confirmations.
* If the user breaches the contract, the final transaction could be signed with an escrow to ensure compliance and that the merchant is not “cheated”.

{% hint style="info" %}
Payment Channels come with huge amount of potential to be used in any trade negotiation scenarios. Usage of such payment channels is until now largely unexplored, primarily because the amount of real trade (i.e. exchange of goods and services) largely does not use any blockchain as yet. Due to that, there is little research and development that has been done on building products around these capabilities. We will cover many such use cases in the section _Electronic contracts and scripts_.
{% endhint %}
