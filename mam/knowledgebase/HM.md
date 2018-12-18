## Where's my Porsche?

Using IOTA High-Mobility software, a Porsche Emulator can broadcast its location via GPS coordinates. 

Technology featured:

- High Mobility SDK
- Masked Authentication Messaging (MAM)

This demo consists of a sender and a receiver.  The sender monitors the vehicle through the High Mobility API.  One vehicle emulator available is the Porsche Mission E.  The Porsche sends GPS coordinates through a restricted Masked Authentication Messaging (MAM) stream to the IOTA tangle where they are stored.  To avoid data traffic jams, it keeps track and sends GPS coordinates only when they change as the Porsche moves.  

The receiver allows you to monitor this MAM stream.  Sender and receiver can run on totally different systems as long as they are connected to the internet.

Watch the video:  [How to send car data over the IOTA Tangle using MAM and the High Mobility API](https://youtu.be/L-O-okg0bWk)

Read the blog:  [Masked Authenticated Messaging](https://high-mobility.com/K0G4/blueprints/QYLJ/masked-authenticated-messaging-blueprint)

Learn how:  [IOTA High Mobility Blueprints - MAM](https://github.com/iotaledger/high-mobility-blueprints/tree/master/mam)
