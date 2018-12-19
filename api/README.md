## Client Libraries

Sending and receiving transactions directly through the Tangle using the IRI API requires an in-depth understanding of the IOTA protocol.  To make it easier, several client libraries are available:

- [JavaScript](https://github.com/iotaledger/iota.lib.js)
- [JAVA](https://github.com/iotaledger/iota.lib.java)
- [C](https://github.com/iotaledger/entangled)
- [C++](https://github.com/thibault-martinez/iota.lib.cpp)
- [PYOTA](pyota/README.md) (IN PROGRESS)
- [Go](https://github.com/iotaledger/giota)

These client libraries include instructions for the following:

-  getting transactions, ```getTips```, to approve when sending a transaction
-  sending a transaction/bundle to the tangle using ```attachToTangle```
-  fetching transaction data from the tangle in order to ```getBalances```, ```findTransactions``` or ```getTrytes```
-  performing ad hoc queries and analysis

For more information see the [IOTA API reference guide](https://iota.readme.io/reference)
