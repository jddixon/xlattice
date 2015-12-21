<h1 class="libTop">XLattice Gateway</h1>

[XLattice](https://jddixon.github.io/xlattice)
is a library of software supporting
[peer-to-peer](https://en.wikipedia.org/wiki/Peer-to-peer)
communications.  An XLattice network consists of two or more
[Nodes](https://jddixon.github.io/xlattice/node.html),
Each such Node has a cryptographic identity, meaning that it has secret
keys, the public part of which is known to its peers, allowing them to
easily establish secure, encrypted communications between them.  XLattice
Nodes have interfaces to
[Overlays](https://jddixon.github.io/xlattice/overlay.html)
such as the global Internet.

A **Gateway** is an XLattice Node which facilitates communcations between
Nodes which do not share a common Overlay.  Nodes may be for example on
different
[private IP networks](https://en.wikipedia.org/wiki/intranet)
or they might route traffic through an unusual protocol such as email
([SMTP](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol) or
they may prefer to route traffic through a public service such as
[Tor](https://www.torproject.org).

A Gateway is not the same as a
[router,](https://en.wikipedia.org/wiki/Router_\(computing\))
although it may be resident on
a router.  A Node communicating with an otherwise unreachable Node sends
messages through an Internet Protocol (IP) network to the Gateway, which
forwards the messages though an address on the remote Overlay to the
destination Node.  The remote Node will route traffic back in the same
manner, usually but not necessarily using the same Gateway.

