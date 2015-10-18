<h1 class="libTop">XLattice Cluster</h1>

An XLattice cluster is a group of cooperating servers.  Each has a 
cryptograpic identity.  That is, each has 

* a [ NodeID](https://jddixon.github.io/xlattice/nodeID.html),
* an RSA key used for creating digital signatures (**skPriv**), and
* an RSA key used for encrypting data (**ckPriv**).  

In other words each cluster member is
or carries an 
[XLattice Node](https://jddixon.github.io/xlattice/node.html), 
which incorporates that cryptographic identity.

The NodeID is a unique 160- or 256-bit number.  
Each of `skPriv` and `ckPriv`is a RSA private key, normally
at least 2048 bits in length.  Each has a corresponding public key 
(**sk** and **ck** respectively) which can be distributed freely without
compromising the secrecy of its private key counterpart.  

You open communications with an XLattice node by using it well-known
public key `ck` to encrypt a secret, one that only that cluster member can
decrypt, because only that node (cluster member) has the corresponding private
key.  The secret is an AES key.  The RSA-encrypted secret is used to encrypt 
a second key,
the AES key used for the rest of the messages in the communications session.
The cluster member sends the encrypted second key back to whoever has 
initiated the conversation, and further messages between the two machines 
are encrypted using the second key.

The members of the cluster have at least two well-known ports.  These 
are 16-bit numbers, as is conventional on network servers.  All of the
members will listen on one of the ports (the same 16-bit number on each
member) for messages from other members of the cluster.  This port number
will not generally be published: it is private to the cluster and any 
messages received on this port from other hosts (other machines on the
network but not members of the cluster) will be ignored.  

The second port, whose 16-bit number is shared by all members of the cluster,
is used for communications between members of the cluster and the outside
world.  That is, this port number will generally be published, and clients
(legitimate users of the cluster's services) communicate with the cluster
through this port using whatever protocol is appropriate for the service
provided by the cluster.

