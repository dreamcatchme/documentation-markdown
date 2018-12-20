## MAM Architecture

Language:  	Rust (similar to C++) along with Emscripten for producing WebAssembly

### Merkle Tree Signature Scheme

Merkle Tree was named for its inventor, Ralph Merkle, in 1979.  The architecture is a binary tree (meaning only two leaves) where each “no-leaf” node contains the hash of its children as shown in this diagram.  




![Diagram showing Merkle Tree with four no-leaf nodes joined to two leaves joined to one root as explained in the text](images/merkletree.png)




The top level shows Index 0-3 as part of a private key.  A private key is computed from the seed, index, and security level.  The second level shows each Leaf A-D.  Each Leaf A-D contains an address.  Each address is a hash of it's corresponding private key.  The Merkle Tree Signature Scheme begins by hashing each Leaf A-D then combining all these hashes into two leaves.  The root combines all the hashs.  For purposes of MAM, the root is also called the “channel ID”.  


For more information:

[Merkle Trees Explained](https://www.youtube.com/watch?v=WF5dNyFOqEc)

[Merkle Tree](https://en.wikipedia.org/wiki/Merkle_tree)

[Merkle Signature Scheme](https://en.wikipedia.org/wiki/Merkle_signature_scheme)

[IOTA MAM Eloquently Explained](https://medium.com/coinmonks/iota-mam-eloquently-explained-d7505863b413)


### MAM Bundle

A bundle of MAM has basically two sections:  signature section and message section.  The signature contains a Merkle tree signature scheme used to validate ownership.  The message section contains the actual message.

### Message Chain

The message chain flow only goes forward.  Subscribers may not view old messages sent before they subscribed.  Once a message is sent, it cannot be changed.
