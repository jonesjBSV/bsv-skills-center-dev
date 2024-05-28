---
description: >-
  Local policies specify the limitations that arise from a node's system
  configuration and hardware setup
---

# Local Policies

When a mining node sets up its system, it will configure the software based on its infrastructure. These configurations come under local policies. Some of these policies are also based on the nodes' preferences regarding the services they want to offer beyond their mandated enforcement of protocol-level rules, which come under standard policies.

These policies are typically associated with the node infrastructure and the node's configuration when setting it up.&#x20;

There are certain rules related to:&#x20;

* Block and transaction sizes that the node can support
* Transaction fees
* How the node validates the transaction and blocks received from other participating nodes via the Bitcoin server network&#x20;

> Full List of Consensus Rules and Local Policies&#x20;

{% file src="../.gitbook/assets/tx rules (1).xlsx" %}
This is only provided for reference and does not claim to be a fully exhaustive list of rules present in the code
{% endfile %}

{% hint style="info" %}
All of the Consensus rules that a node need to ensure that it is enforcing is something legally they are bound by contract when they collect block subsidy from the issuer of the coins. This is how the blockchain system integrates the legal framework into it.

Local policies are configuration items that are specific to the node's infrastructure and could be different for each node. These policies will allow various nodes to compete with each other regarding their services, including reliable and high throughput processing, large-size transactions, etc.
{% endhint %}
