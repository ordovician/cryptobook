# Hashes
Data is transformed using a `hash function` into something we can either call:

* A hash
* Digital fingerprint
* Message digest

A hash function is different from a cipher in that it only goes one way. Multiple messages may be turned into the same `digital fingerprint`. If we only need to decide whether two messages are equal we can compare just the hashes if there exists a **sufficiently large number** of hashes so that collision is practically impossible.

E.g. an attacker can't trivially create a bogus message with the same hash as the valid message unless trial and error is performed, which would be impractical if the number of possible hashes is very large.

Hashes are used with digital signatures to **compress** a message so we only have small amounts of data to encrypt and decrypt.
