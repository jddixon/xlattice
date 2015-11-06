<h1 class="appTop">XLattice Upax</h1>

A distributed content-keyed data storage system.

## Current Implementation

A Upax implementation has three parts:

* [server](upaxServer.html),
* [client](upaxClient.html), and
* [fault-tolerant log](ftLog.html).

Upax accepts and stores data files of arbitrary size.  A data file is
identified by its 256-bit/32-byte (SHA-256 or SHA3-256) content key.
The content key is the hash of the file.

Early versions
of Upax will store a copy of a file on each participating server node.
Later versions will store fewer copies, probably at least three,
deleting the least recently used where storage capacity is neared
and in effect migrating data to machines where it is more frequently
used.

Later implementations of  are expected to add a
[UpaxMirror](upaxMirror.html)
which will be capable of dealing with client queries but not able to add
to the data store.  That is, clients can use the UpaxMirror as a fast
local cache, but to add files to the distributed storage system
they will have to go through a UpaxServer instead.

Upax servers and clients are
[XLattice nodes](https://jddixon.github.com/xlattice/node.html)
and so are identified by
unique 256 bit keys,
[NodeIDs.](https://jddixon.github.com/xlattice/nodeID.html)
Each has a pair of RSA keys, one used
for encryption and one used for digital signatures.  At least in the
near term Upax servers will only accept messages from known hosts.
Specifically, a client must prove that it has the private RSA key
corresponding to its public RSA key when opening any connection to
a server.

In current implementations of Upax, files are owned by the first
to commit them.  There is no notion of privacy.  Any client may
request a copy of any file - but only the owner may delete it.  It
is likely that upax_go will retain these characteristics in the near
term.
