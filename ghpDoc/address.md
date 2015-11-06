<h1 class="libTop">XLattice Address</h1>

## XLattice Transport

XLattice
[Nodes](https://jddixon.github.io/xlattice/node.html)
communicate by sending messages over connections.  The primitive
notions common to all XLattice connections are

* [Acceptor](https://jddixon.github.com/xlattice/acceptor.html),
  an EndPoint on which a Node listens
* [Address](https://jddixon.github.com/xlattice/address.html),
  a sequence of bytes distinguishing EndPoints
* [Connection](https://jddixon.github.com/xlattice/connection.html),
  a pair of EndPoints enabling communications between the Nodes at either end
* [Connector](https://jddixon.github.com/xlattice/connector.html),
  an address and other information necessary to establish
  a connection to another Node
* [EndPoint](https://jddixon.github.com/xlattice/endPoint.html),
  an address and a Transport
* [Transport](https://jddixon.github.com/xlattice/transport.html),
  a name identifying a communications protocol
### Address

An Address is a sequence of bytes sufficient to distinguish a Node within
a set of Addresses.  The Address may include a local part.  For example

* in
  [**ipv4**](https://en.wikipedia.org/wiki/IPv4)
  the Address must include a 32-bit value identifying the host
  and may include a 16-bit port number associated with a thread or process
  on that host.  The 32-bit limit restricts the number of hosts to roughly
  4 billion
* in
  [**ipv6**](https://en.wikipedia.org/wiki/IPv6)
  the main part of the Address is a 64-bit value instead, restricting
  the number of hosts to about 16 quintillion (`10^18`)
* a simple **email** address consists of a userID and a fully qualified domain
  name (so in `john.doe@example.com` the local part is `john.doe` and the
  domain name is `example.com`.

In ipv4 and ipv6 it is necessary to distinguish the **serialization** of the
Address from its binary form.  The main part of an ipv4 address, for example,
is a 32-bit binary value in its wire form, but normally written as a
[**dotted quad**,](https://en.wikipedia.org/wiki/Dot-decimal_notation)
`A.B.C.D`, in which each byte is represented by its decimal
value, a number between `0` and `255` inclusive.

