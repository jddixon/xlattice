<h1 class="libTop">XLattice Peer</h1>

[XLattice](https://jddixon.github.io/xlattice) 
is a library of software supporting 
[Peer-to-Peer](https://en.wikipedia.org/wiki/Peer-to-Peer)
communications.  An XLattice network consists of two or more
[Nodes](https://jddixon.github.io/xlattice/node.html),
Each such Node has a cryptographic identity, meaning that it has secret
keys, the public part of which is known to its Peers, allowing them to
easily establish secure, encrypted communications between them.  XLattice
Nodes have interfaces to 
[Overlays](https://jddixon.github.io/xlattice/overlay.html) 
such as the global Internet.

## Peers

To an XLattice Node, a Peer is another XLattice Node, or something which 
behaves like one, with which the Node has established communications,
or with which it knows how to establish communications.  When an XLattice 
Node is started, it might be provided with a
list of Peers, possibly from a configuration file in its local file 
system (**LFS**).  
Alternatively, it might learn a Peer's **BaseNode** details when 
the Peer connects to one of the node's endPoints.  In any case, 
the node maintains a table of Peer descriptors, including the public
part of each Peer's RSA keys.

## BaseNode Properties

A Peer shares 
[BaseNode](https://jddixon.github.io/xlattice/baseNode.html)
characteristics such as name, 
[NodeID](https://jddixon.github.io/xlattice/nodeID.html), 
RSA public keys, and 
[Overlays](https://jddixon.github.io/xlattice/overlay.html).

## Other Properties

Most importantly a Node associates with each peer one or more
[Connectors](https://jddixon.github.io/xlattice/connector.html).
A Connector is essentially a recipe for establishing a connection
to the Peer.  This will include

* a Gateway where necessary
* the Overlay through which the connection is to be made
* the Protocol to be used
* the Address of the Peer 

