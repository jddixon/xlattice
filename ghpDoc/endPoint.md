<h1 class="libTop">XLattice EndPoint</h1>

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

### EndPoint

An EndPoint is identified by the associated Transport and an Address.
The Address has either one or two parts.  For example, an IPV4 address
has a 32-bit value and an optional local part.  The IPv4 address part
is normally written as a **dotted quad** like `127.0.0.1`, where each
number represents a byte in the range 0-255.  If it is present the
IPv4 local part is a 16-bit value.

The Address may include an explicit local part or there may be a
default local part included with the Transport.  Thus for example
the default local part associated with the Transport `http` is `80`
and the default associated with the Transport `https` is `443`.

As another example, for email the transport is `smtp` and there is
no default Address or local part.

