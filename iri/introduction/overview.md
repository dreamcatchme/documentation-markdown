# IOTA node software (IRI)

The IRI (IOTA reference implementation) is open-source Java software that you can [run](/how-to-guides/running-the-iri.md) on a computer to participate in an IOTA network. Any computer that runs the IRI is known as an IRI node.

The IRI contains a default protocol that defines what a valid transaction is, what a confirmed transaction is, and how IRI nodes should communicate with each other.

The primary purpose of the IRI is to do the following:
* [Validate transactions](/concepts/transaction-validation.md)
* [Append valid transactions to a ledger](/concepts/the-distributed-ledger.md)
* [Agree on the global state of the distributed ledger](/concepts/the-distributed-ledger.md) with other IRI nodes in the same IOTA network (reach consensus)
* [Allow clients to connect to the IRI](/how-to-guides/interacting-with-the-iri.md) so that they can interact with the ledger and have their transactions appended it

By [running the IRI](/how-to-guides/running-the-iri.md), you have your own direct access to an IOTA network so you can interact with the ledger whenever you like. On the other hand, if you don't run the IRI, you are reliant on connecting to someone else's computer before you can interact with the ledger.

## Types of IRI node

You can choose to run two types of IRI node, depending on your needs and amount of memory space on your computer:

* **Permanode:** An IRI node that keeps a record of all valid transactions in its ledger. Run a permanode if you want to keep a record of all valid transactions. You can run a permanode by setting the `LOCAL_SNAPSHOTS_ENABLED` configuration parameter to `false`. 
* **Local snapshot node:** An IRI node that removes transactions from its ledger at regular intervals by creating a [local snapshot](/concepts/local-snapshot.md). Run a local snapshot node if you don't care about keeping a record of all valid transactions and you want to keep the size of your IRI node's ledger small. You can run a local snapshot node by setting the `LOCAL_SNAPSHOTS_ENABLED` configuration parameter to `true` and by setting the other `LOCAL_SNAPSHOT` configuration options.

## Limitations

The IRI is not client software, so it doesn't create or sign transactions (it's not a wallet). To create or sign transactions, you must use client software such as the Trinity wallet or a client library.
