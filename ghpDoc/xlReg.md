<h1 class="libTop">xlReg</h1>

[xlReg](clusterReg.html) is a tool, primarily intended for use in testing,
which facilitates the formation of
[clusters,](https://jddixon.github.io/xlattice/cluster.html)
groups of cooperating
[nodes.](https://jddixon.github.io/xlattice/node.html)

On registration, a client (an xLattice cluster member)
is issued a globally unique NodeID, a 256-bit random value.
Once it has an ID, the member can create and/or join clusters.

A cluster has
a maximum size set when it is created.  When members join the cluster they
register their two RSA public keys and one or more IP addresses.
If the cluster only supports communications between members, members
register only one IP address.  If non-member clients are allowed to
communicate with the cluster, members register a second address for
that purpose.  It is possible that certain applications may require
additional IP addresses.  (The first address is used for communications
between cluster members.  Any second address is used for communications
between cluster members acting as servers and their clients.)

When a member has completed registration, it can retrieve
the configuration data other members have registered.

The xlReg server, its clients, and the cluster members, are all
[XLattice nodes](https://jddixon.github.io/xlattice/node.html)
which means that each has

* a unique [NodeID](https://jddixon.github.io/xlattice/nodeID.html)
* two RSA keys, one for encrypting data and the other for creating
  digital signatures
* at least one address (such as a TCP/IP connection) on which it
  listens at all times
* and optionally a local file system

