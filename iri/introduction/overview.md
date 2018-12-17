# IOTA node software (IRI)

The IRI (IOTA reference implementation) is open-source Java software that you can [run](/how-to-guides/running-the-iri.md) on a computer to participate in an IOTA network. Any computer that runs the IRI is known as an IRI node.

The IRI contains a default protocol that defines what a valid transaction is, what a confirmed transaction is, and how IRI nodes should communicate with each other.

The primary purpose of the IRI is to do the following:
* [Validate transactions](/iri/concepts/transaction-validation.md)
* [Append valid transactions to a ledger](/iri/concepts/the-distributed-ledger.md)
* [Agree on the global state of the distributed ledger](/iri/concepts/the-distributed-ledger.md) with other IRI nodes in the same IOTA network (reach consensus)
* [Allow clients to connect to the IRI](/iri/how-to-guides/interacting-with-the-iri.md) so that they can interact with the ledger and have their transactions appended it

By [running the IRI](/iri/how-to-guides/running-the-iri.md), you have your own direct access to an IOTA network so you can interact with the ledger whenever you like. On the other hand, if you don't run the IRI, you are reliant on connecting to someone else's computer before you can interact with the ledger.

## Limitations

The IRI is not client software, so it doesn't create or sign transactions (it's not a wallet). To create or sign transactions, you must use client software such as the Trinity wallet or a client library.
