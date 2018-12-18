## MAM Functions

MAM is used to send and to receive encrypted messages over the Tangle distributed ledger network.  MAM offers subscription channels.  Channel owners publish data.  Channel subscribers receive data.  

### Channel Modes

Channel owners can publish channel data using three modes:  public, private, and restricted.

#### Public
Public mode is useful for public announcements.  Anyone who sees the message can decode it because the channel ID and the address are the same.  

#### Private
Only subscribers can view private messages.  In private mode, a hash of the channel ID is used as the address.  This stops random users from decrypting the message because they cannot derive the root from the hash.

#### Restricted
In restricted mode, channel owners specify viewers by telling them a key.  The key is called the side_key.  Only those with the side_key can unlock the content in the message.


### Message Chain Flow
Every message in the message chain holds a reference to the next message.   Therefore, the message chain flows in a forward direction.  Subscribers may only view messages going forward from the date they subscribed.  They may not view prior messages.


### Confirmation 
Unlike IOTA transactions, MAM messages do not need to be confirmed


### Message Archival
After a snapshot, all messages are deleted from the Tangle unless the subscriber is connected to a permanode then MAM messages are saved
