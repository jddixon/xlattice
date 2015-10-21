#hamt

An implementation of the HAMT data structure.

A Hash Array Mapped Trie ([HAMT][bagwell2001]) 
provides fast and memory-efficient access to large amounts of data held 
in memory.  Values are stored by **key**.  All HAMT keys are mapped into 
fixed length unsigned integers. In this implementation these are 64 bits
long, `uint64`s.  The **value** may be of any type but typically is a 
pointer to a data structure of interest.

The HAMT trie is essentially a prefix trie where the nodes in the tree
are either tables or leaf entries.

In a simpler implementation at each level there is either a leaf node
or a table with up to `2^w` slots, where w is a small 
integer.  The next `w` bits of the hash 
derived from the key are construed as an index into that table.  The
table grows dynamically to its maximum number of slots as entries are added.  
Whenever there is a 
collision at a given level, a pointer to a new table replaces the current 
leaf entry,
and both new and old entries move to the child table, possibly 
recursing in the process.

The current implementation has been tested with values of
3, 4, 5, and 6 for `w`.  Preliminary performance tests indicate 
that `w=6` is optimal.  That is, a table with 64 slots gives the best
performance.  

An enhancement introduces a fixed size table at the root.  This is
characterized by another small integer t: the root has 2^t entries
and the table at the root is indexed by the first t bits of the
key's hashcode.  Performance tests show that for optimal performance
the root table should approach the total number of entries in size.

A further enhancement would allow dynamic resizing of the root table.

Whereas a normal hash table would be quite large and might periodically
require expensive resizing, the HAMT data structure is roughly 
as fast as a hash table, but starts small and consumes more memory only 
as needed.

## Limitations

* This code is not thread-safe.  That is, using code must provide any
necessary locking.

* the HAMT algorithm depends upon bit-counting.  On modern Intel and AMD 
processors this 
can be done using a specific machine-language instruction, POPCNT.  Current
XLattice implementations of HAMT emulates this in software using the 
[SWAR][wiki-swar] algorithm,  The emulation code is on the order of ten times
slower than the machine instruction.  

## References

[Bagwell, "Ideal Hash Trees"][bagwell2001]  (2001 PDF)

[Wikipeida, "Hash array mapped trie"][wiki-hamt]

[Wikipedia, "SWAR"][wiki-swar]


[bagwell2001]: http://infoscience.epfl.ch/record/64398/files/idealhashtrees.pdf

[wiki-hamt]: http://en.wikipedia.org/wiki/Hash_array_mapped_trie

[wiki-swar]: http://en.wikipedia.org/wiki/SWAR

