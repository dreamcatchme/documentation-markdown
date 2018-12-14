# Local snapshot

A local snapshot is the process in which an IRI node deletes old transactions from its ledger.

Over time, the [ledger](/iri/concepts/the-distributed-ledger.md) of an IRI node accumulates many valid transactions, which often cause the size of the ledger to become larger than the IRI node's available memory. To stop the ledger from becoming too large, you can choose to create local snapshots at regular intervals. This option is enabled by default in the [`LOCAL_SNAPSHOTS_ENABLED` configuration parameter](/iri/references/iri-configuration-options#local-snapshots-enabled). 

**Note:** Local snapshots are available only in version 1.6.0 and higher of the IRI.

## How it works

To create a local snapshot, the IRI deletes old transactions and keeps only a subgraph of newer transactions, increasing the amount of free storage space in the ledger.

### Subgraph

A subgraph is a section of the ledger that contains all transactions between a user-defined milestone transaction and new tip transactions.

For local snapshots, the user-defined milestone transaction is calculated by doing the following:

[`LOCAL_SNAPSHOTS_DEPTH` confirguration parameter](/iri/iri-configuration-options#local-snapshots-depth) + [`LOCAL_SNAPSHOTS_PRUNING_DELAY` confirguration parameter](/iri/iri-configuration-options#local-snapshots-pruning-delay)

The result of this calculation is equal to the amount of milestone transactions that the IRI keeps in the subgraph.

QUESTIONS:

Can you become a local snapshot node at any time by stopping an IRI node and changing the confiration options to `LOCAL_SNAPSHOT_ENABLED`=`TRUE`?

Is it possible to perform local snapshops with the exception of a set of arbitraly choosen transactions — lets call them MyPermaTransactions?

Are snapshot files used by the IRI only when it runs for the first time in order to create the ledger (RockDB database)?

What is the data in the snapshot metadata file?
ZGOFRIQUBGUIGZRGNUEYVDZUVXBS9WFTNVMCZIWJII9GDEPCEERSGRNIJYCFTACCMQLKPLXUNGLKZ9999
917780
1544531791
211
101
MBVHSITOOMNWUWNMQKTXNZQZM9CDLUUOGMQQKLLGQJMDBNSOTGAIHTUFCNJZICIBQEJGTF9KNMBI99999;917740