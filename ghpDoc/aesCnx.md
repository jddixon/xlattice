<h1 class="libTop">XLattice AesCnx Protocols</h1>

This protocol is used by
[XLattice Nodes](https://jddixon.github.io/xlattice/node.html)
for setting up communications
sessions with
[Peers](https://jddixon.github.io/xlattice/peer.html)
or other
XLattice nodes
where the initiating Node knows the public RSA key associated with an
address.

* the initiator selects a temporary 256-bit/32-byte AES session key,
  encrypts it using the respondent's RSA public key and
  [RSA OAEP](https://en.wikipedia.org/wiki/Optimal_asymmetric_encryption_padding),
  and sends the result to the server, which is an XLattice Peer
* the server chooses the actual 32-byte AES session key, encrypts that using
  the temporary AES key, and sends this back to the initiator
* the initiator uses the temporary AES key to decrypt the response, and
  extracts the real AES session key
* the session continues with both sides using the real session key

The Nodes involved, the initiator and the respondent, may use any mutually
agreed protocol to continue the session.  That may include a procedure
for changing the session key, as is prudent in any longer-term session.
It is probably also advisable to change the session key at least once an hour
if there are significant levels of traffic on the link.

