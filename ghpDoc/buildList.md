# buildList

A BuildList is a view of the contents of a directory tree at some particular
moment in time.  Its authenticity is usually guaranteed by the holder of an 
[RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) key
whose public part appears at the top of the BuildList.  The keyholder makes
the guarantee my appending a digital signature to the BuildList,
allowing a single-operation check on the BuildList's validity.
Files in the BuildList are identified by name and by an 
[SHA](https://en.wikipedia.org/wiki/Secure_Hash_Algorighm) 
**content key**, where the content key is the SHA hash of the content
of a file..

## Serialization

In its serialized form a BuildList consists of

* a public key line,
* a title line,
* a timestamp line,
* a fixed-format `## BEGIN CONTENT ##` line,
* a number of content lines,
* a fixed-format `## END CONTENT ##` line,
* and optionally a digital signature.

Each of the lines ends with a linefeed (a byte with the value `10`,
conventionally written as `\\n`).

A blank line follows the last content line.

The timestamp (in `CCYY-MM-DD HH:MM:SS` form) represents the time at which
the list was signed using the RSA private key corresponding to the key in
the public key line.

The public key itself is 
[base-64](https://en.wikipedia.org/wiki/Base64) encoded.

An example of a correctly formatted BuildList header:

    -----BEGIN RSA PUBLIC KEY-----
    MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAoM2sBgX0ChP2JriXkOxS
    e2FjHYVzBGkNvgf0vIAa7FFYZi2pWmxBAVXgl3tTiB3quqqud/MbKqdejM6gkKBK
    v8f7hlcBQLD6BLIZ/RRfhIElc+WlDVfKSnBTB4va5qTQAgvuq5i8+oMj7G8WEy5d
    7cYucWyUJMtHvT4pCDtBWeeqQ62tByWjv34Ud/+A9Mjf0leiWxM3tiToVsqIKb4s
    zPjEShF9rvcNa9XEy1dKpcDz9Szbm2SlxOgM83fDDGtOq4SSCSqndtxrOvXXPB57
    H1mJV/FmerbXRPm5ERJVNIxtLk7Gr2Ce45FVlWyJGMhpfVlKkkk+bRQ02OFfazJI
    GQIDAQAB
    -----END RSA PUBLIC KEY-----
    optionz v0.1.11
    2016-08-02 22:27:12
    # BEGIN CONTENT #

## Content Lines

The content lines section begins and ends with fixed `# BEGIN CONTENT #`
and `# END CONTENT #` delimiters.  Each actual content line consists of

* either a directory name or
* a file name followed by its `content hash` in hexadecimal form.

The **content hash** is calculated from the file contents using one of
the forms of the **Secure Hash Algorithm**, either **SHA1**, yielding a
40-character hex value, or **SHA2**, yielding a 64-character value.
SHA is a one-way hash, meaning that it is easy to calculate the hash
but extremely difficult or impossible to perform the reverse operation,
identifying a document from its hash.

The name in a content lne
is indented by a number of spaces equivalent to its depth in the hierarchy.

	# BEGIN CONTENT #
	dir1
	 fileForHash0 0123456789012345678901234567890123456789
	 fileForHash1 abcdef0123456789abcdef0123456789abcdef01
	dir11
	 fileForHash2 12abcdef0123456789abcdef0123456789abcdef
	 fileForHash3 3456abcdef0123456789abcdef0123456789abcd
	# END CONTENT #

That is, the data structure between the BEGIN/END CONTENT lines is an
[NLHTree](http://jddixon.github.io/nlhtree_py).

## Digital Signature

The **SHA1withRSA**
[digital signature](https://en.wikipedia.org/wiki/Digital_signature)
is over the entire SignedList excluding
the digital signature line and the blank line preceding it.  All line
endings are converted to LF ('\\n') before taking the digital signature.

## Extended Hash

The BuildList itself has a 20-byte **extended hash**, the 20-byte SHA1
digest of a function of the public key and the title.  This means
that the owner of the RSA key can create any number of documents
with the same hash but different timestamps with the intention
being that users can choose to regard the document with the most
recent timestamp as current.

