|Table of contents |
|:----------------:|
|[What is IOTA?](#what-is-iota)|
|[What is the purpose of IOTA?](#what-is-the-purpose-of-iota)|
|[How does IOTA work?](#how-does-iota-work)|
|[What is the IOTA token and why is it valuable?](#what-is-the-iota-token-and-why-is-it-valuable)|
|[What are the benefits of IOTA?](#what-are-the-benefits-of-iota)|
|[For what industries is IOTA useful?](#for-what-industries-is-iota-useful)|
|[How do I get started?](#how-do-i-get-started)|
||


# What is IOTA?

IOTA is a [distributed ledger technology (DLT)](/introduction-to-iota/concepts/distributed-ledger-technology.md) that allows computers in an IOTA network to do the following:
* Transfer data and value among each other
* Store an immutible record of all data and value transfers
* Access records of data and value transfers

## What is the purpose of IOTA?

IOTA is standardized protocol that offers you the building blocks for developing applications that make automated transactions for the machine-to-machine economy.

OK, but what's that? A machine-to-machine economy is one in which any computer can transfer value to other computers. At the moment, this type of economy is impossible. Computers need an identity and permission to connect to a bank before they can have a bank account.

IOTA solves this problem by giving computers a unique, verifiable identity (seed) that allows them to have accounts (addresses) on which they can store value and transfer it in the form of [IOTA tokens](#what-is-the-iota-token-and-why is-it-valuable).

But IOTA isn't just about sending value. In IOTA, you can also send data, which is set to become the [world's most valuable resource](https://www.economist.com/leaders/2017/05/06/the-worlds-most-valuable-resource-is-no-longer-oil-but-data). By allowing computers to send secure data to each other, IOTA opens the flood gates for applications that monetize data to bring about a [third industrial revolution](https://www.youtube.com/watch?v=QX3M8Ka9vUA&feature=youtu.be).

## How does IOTA work?

In an IOTA network, data is sent and stored in packages called transactions, which are handled by the following entities:
* [**IRI nodes:**](/iri/introduction/overview.md) Computers that are reponsible for storing transactions in a ledger
* Clients: Computers that create and send transactions to IRI nodes

Each client in an IOTA network has a secret password called a seed, which is used to generate unique addresses and to create digital signatures. Addresses are the accounts from which transactions are sent and received. Digital signatures prove ownership of an account and allow value transactions to be sent from addresses.

Transactions can be one of the following types:
* Data transaction: Transaction that sends only plain text or encrypted data to a recipient's address
* Value transaction: Transaction that transfers IOTA tokens to a recipient's address

## What is the IOTA token and why is it valuable?

The IOTA token is a scarce digital good that's built into the [IOTA MainNet network](/introduction-to-iota/references/iota-networks.md). 

All IRI nodes agree that a mamimum of 2,779,530,283 277,761 tokens exist in the network. This maximum number is built into the network and can't ever be changed.

You own IOTA tokens only when the IRI nodes in a network reach a consensus on the balance of your address.

To reach consensus, all IRI nodes must [validate transactions](/iri/concepts/transaction-validation.md) that transfer IOTA tokens by doing a number of checks, which include checking that the sender owns the tokens.

## What are the benefits of IOTA?

IOTA is an open-source technology that can streamline, secure, and automate any process that sends data or transfers value from different devices.

### Trust

All transactions in the ledger are immutible and transparent.

Each IRI node in an IOTA network validates and stores transactions in its ledger, then sends its contents to other IRI nodes that do the same. As a result, all valid transactions are agreed on by all nodes, removing the need to trust a single one in the network.

### Security

IOTA uses quantum-resistant cryptography to secure the network and prevent attackers from stealing IOTA tokens.

IOTA networks are peer-to-peer networks. No central authority controls the ledger of transactions, instead all IRI nodes hold a copy and run the software that contains the IOTA protcol to automate the agreement on its contents.

### Cost saving

IOTA is free to use. You don't need to pay a subscription, or sign a contract. Even transactions are free to send.

### Scalable

For each transaction that's appended to the ledger validates two previous transactions. This process makes IOTA incredibly scalable because the more new transactions that propagate through the network, the faster other transactions are validated.

This process forms a data structure called a directed acyclic graph (DAG), which we call the Tangle.

## For what industries is IOTA useful?
IOTA is an open-source technology that can streamline, secure, and automate any process that sends data or transfers value among different devices.

Therefore, many industries such as the following could benefit from using IOTA:

* [Mobility](https://www.iota.org/verticals/mobility-automotive)
* [Global trade and supply chains](https://www.iota.org/verticals/global-trade-supply-chains)
* [Industrial IoT (Internet of things)](https://www.iota.org/verticals/industrial-iot)
* [Healthcare](https://www.iota.org/verticals/ehealth)
* [Energy](https://www.iota.org/verticals/smart-energy)


## How do I get started?

[Start your IOTA journey by creating your first seed](/getting-started/creating-a-seed.md)