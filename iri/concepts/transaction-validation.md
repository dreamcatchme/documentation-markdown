# Transaction validation

The IRI allows only valid transaction to be appended to its ledger. Therefore, the IRI is responsible for validating transactions during the following stages:
* On receipt of new transactions
* During the tip selection process

| **Table of contents**                  |        
| :------------------- |
|[Transaction validation on receipt of new transactions](#transaction-validation-on-receipt-of-new-transactions)|
|[Validation during the tip selection process](#validation-during-the-tip-selection-process)|
|[  &raquo; Bundle validator](#bundle-validator)|
|[  &raquo; Ledger validator](#ledger-validator)|
||

## Transaction validation on receipt of new transactions

The IRI receives new transactions from both clients and its neighbor nodes.

When the IRI receives a new transaction, the transaction validator checks the transaction for the following:
* The proof of work was done
* The value of any transaction in the bundle doesn’t exceed the total global supply
* The transaction is not older than the last snapshot and not newer than two hours ahead of the node’s current time

## Validation during the tip selection process

When clients asks a node for tip transactions, the IRI performs the [tip selection process](/iri/concepts/tip-selection.md).

The bundles of each transaction that the IRI traverses during the tip selection process are checked by the bundle validator and the ledger validator.

### Bundle validator

The bundle validator makes sure that all transactions in a bundle are valid.

When the IRI traverses a transaction during a weighted random walk, the bundle validator checks its bundle for the following:
* The value of any transaction in the bundle doesn’t exceed the total global supply
* The total value of all transactions in the bundle is 0 (inputs and outputs are balanced)
* Any signatures in value transactions are valid

### Ledger validator

The ledger validator makes sure that all the bundles that lead to a tip transaction are valid and do not include addresses that double spend.

After the bundle validator has finished, the ledger validator checks that each bundle does not lead to a double spend by checking the values of all addresses in a bundle. If a double-spend is found, the random walk steps back one transaction and finds another route to a tip transaction. As a result, the ledger validator makes sure that double-spends are never confirmed.
