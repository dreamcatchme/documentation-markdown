# Tip selection

Before a new transaction can be validated by the IRI and appended to its [ledger](/concepts/the-distributed-ledger.md), that transaction must include the hashes of two transactions that are already in the ledger. In the IRI, these transactions are called tip transactions because they are recent transactions that appear at the tip of the graph.

In the IRI (IOTA reference implementation), [tip selection](https://github.com/iotaledger/iri/tree/dev/src/main/java/com/iota/iri/service/tipselection) is the process of selecting two tip transactions.

Clients can request the hashes of two tip transactions from the IRI by calling the getTransactionsToApprove API method. One of these tip transaction hashes is added to the new transaction's `branchTransaction` field and the other to its `trunkTransaction` field.

## How it works

The IRI finds two tip transaction hashes for clients by selecting a subgraph of the ledger and performing two weighted random walks through it. Each weighted random walk returns a tip transaction hash.

<dl>
<dt>Weighted random walk</dt>
<dd>Algorithm that the IRI uses during tip selection to find a path to a tip transaction in the ledger. To increase the probability of new transactions being selected and appended to the ledger, the algorithm favors a path through transactions that have a larger <a href="#cumulative-weight">cumulative weight</a>.</dd>
</dl>

### Subgraph

A subgraph is a section of the ledger that contains all transactions between a user-defined milestone transaction with a specified index (`depth`) and new tip transactions.

The user-defined milestone transaction is calculated by doing the following:

    `latestMilestoneIndex` - `depth`

The tip selection is performed on a subgraph of the ledger to save computational power. The calculation of each transaction's cumulative weight requires computational power that uses your computer's RAM and CPU. Therefore, if the tip selection was performed on the entire ledger, it would take a long time to finish.

### Cumulative weight

During the weighted random walk, the IRI selects a path from a user-defined milestone transaction to a tip transaction. The IRI favors a path that traverses transactions with a large cumulative weight.

The cumulative weight is a rating that the IRI gives to a transaction, depending on the following variables:
* **Future set:** Transactions that directly or indirectly reference the transaction
* **[`alpha` configuration parameter](/references/iri-configuration-options.md#alpha):** A number that affects the randomness of the tip selection process

The IRI gives a high rating to a transaction with a large future set because it has a higher probability of being confirmed in the [distributed ledger](/concepts/the-distributed-ledger.md) than one with a small future set. However, if the IRI were to rate transactions based only on this variable, the ledger would become a long, narrow chain of transactions, which are referenced by many other transactions. This situation would slow the rate of new transactions being appended to the ledger because new transactions would have to wait until they had a large enough future set before other transactions would reference them. So, to increase the speed at which new transactions are appended to the ledger, the IRI also uses the `alpha` configuration parameter to calculate the cumulative weight.

The `alpha` configuration parameter makes sure that the cumulative weight of each transaction is calculated with an element of randomness. This parameter allows the IRI to select some transactions that have a small future set and by doing so, increase the speed at which new transactions are appended to the ledger.  

For more information about the weighted random walk, and for an in-depth explanation about the theories surrounding the best value for the `alpha` configuration parameter, read our [blog post](https://blog.iota.org/confirmation-rates-in-the-tangle-186ef02878bb).

