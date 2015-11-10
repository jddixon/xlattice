# XLattice Transport

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

