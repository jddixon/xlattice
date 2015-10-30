<h1 class="libTop">XLattice U</h1>

Content-keyed directory structures for
[xlattice,](https://jddixon.github.io/xlattice)
a file system
based on **content keys**, where a content key is a cryptographically
secure hash either 20 or 32 bytes long.

## Directory Structure

**U* is optimized for storing very large numbers of files.  The
first byte of the content key determines which mid-level directory
the file goes in; the second byte determines its lower-level
directory.  The upper-level directory is conventionally called **`U`**.

So if a file's content hash is `abcdef...1234`, then it
will usually be stored in `U/ab/cd/ef...1234`.  There are 256 mid-level
directories and 256 subdirectories below each of these, so there are
256x256 = 65536 such lower-level directories.

There will also be at least two more subdirectories at the upper level

* `U/in`, used for assembling files prior to being moved into the
  appropriate lower directory; typically used for files being
  received over the wire
* `U/tmp`, similarly used by the system for temporary storage of files
  being moved into `U/` from the local file system

## Content Keys

Hashes are calculated using
a variant of the
[Secure Hash Algorithm](https://en.wikipedia.org/wiki/Secure_Hash_Algorithm).
Currently three versions of SHA are supported:

* **SHA1** (20 bytes/160 bits), also called SHA-1
* **SHA2** (32 bytes/256 bits), also called SHA-256
* **SHA3** (32 bytes/256 bits), which is the 256-bit variant of **Keccak**,
  the winner of a recent competition run by an agency of the US government

## API

Pseudo code: function name, parameter list, and values returned.  Parameter
type follows the paramter name.

    // Copy a data file into U.
	CopyAndPut(path string, key []byte) (int64, error)
	CopyAndPut1(path, key string) (int64, string, error)
	CopyAndPut2(path, key string) (int64, string, error)
	CopyAndPut3(path, key string) (int64, string, error)

    // Retrieve a data file from U.
	GetData(key []byte) ([]byte, error)
	GetData1(key string) (data []byte, err error)
	GetData2(key string) (data []byte, err error)
	GetData3(key string) (data []byte, err error)

    // Move a data file into U.
	Put(inFile string, key []byte) (length int64, err error)
	Put1(inFile, key string) (length int64, hash string, err error)
	Put2(inFile, key string) (length int64, hash string, err error)
	Put3(inFile, key string) (length int64, hash string, err error)

    // Write a block of data into U; the length and actual h
    // are returned.
	PutData(data []byte, key []byte) (length int64, hash []byte, err error)
	PutData1(data []byte, key string) (length int64, hash string, err error)
	PutData2(data []byte, key string) (length int64, hash string, err error)
	PutData3(data []byte, key string) (length int64, hash string, err error)

	GetDirStruc() DirStruc
	GetPath() string

	// These functions take two forms, for convenience
	HexKeyExists(key string) (bool, error)
	ByteKeyExists(key []byte) (bool, error)

	HexKeyFileLen(key string) (length int64, err error)
	ByteKeyFileLen(key []byte) (length int64, err error)

	GetPathForHexKey(key string) (string, error)
	GetPathForByteKey(key []byte) (string, error)

