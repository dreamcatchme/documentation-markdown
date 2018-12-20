# The Tangle

The Tangle is the data structure at the heart of IOTA. It was formally introduced in `The Tangle` whitepaper published in 2015. 

![The Tangle by Serguei Popov](https://images.ctfassets.net/r1dr6vzfxhev/3EIrsUlBKwuQGSWIMUkC2u/f387f93529198ae573b1c970c6404b86/Tangle.PNG)





IOTA uses a [DAG](https://en.wikipedia.org/wiki/Directed_acyclic_graph) instead of a [blockchain](https://en.wikipedia.org/wiki/Blockchain) to store its ledger, with the main motivation being scalability. A blockchain has an inherent transaction rate limit, because all participants agree on the longest chain, and discard forks and side branches. The Tangle, on the other hand, allows different branches of the DAG to eventually merge, resulting in a much faster overall throughput.