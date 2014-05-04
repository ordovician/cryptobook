# Hashes
Data is transformed using a `hash function` into something we can either call:

* A hash
* Digital fingerprint
* Message digest

A hash function is different from a cipher in that it only goes one way. Multiple messages may be turned into the same `digital fingerprint`. If we only need to decide whether two messages are equal we can compare just the hashes if there exists a **sufficiently large number** of hashes so that collision is practically impossible.

E.g. an attacker can't trivially create a bogus message with the same hash as the valid message unless trial and error is performed, which would be impractical if the number of possible hashes is very large.

Hashes are used with digital signatures to **compress** a message so we only have small amounts of data to encrypt and decrypt.

# Usage of Hash Functions

Hash function have a wide variety of applications, which might not be immediatly obvious:

* Store passwords safely (e.g. Unix password file)
* Create encryption keys
* Deterministic password generation
* Cheaply check over the network if two files or parts of a file are equal

The properties of hashes that make them usefull for all these tasks is that when hashing something you lose information, so it is impossible to recreate the original message from a hash. This is used in a Unix login system to store passwords as hashes. A login is then performed by hashing the users provided password and comparing it to a hashed password in the password file. This way if a hacker is able to get hold of the password file there is no way to decrypt the file and see all the passwords in plaintext. He or she has to find the password through brute force.

You can use this property to combine simple passwords with other information to create strong passwords. E.g. if you concatinate "pass123" and "amazon" as you login password for amazon this will produce a string full of giberish. 

### Different algorithms for different Usage

The desired properties of the hashing function used will vary depending on application. If you want to compare two files on separat locations on a network you want to be able to hash the content of the files **fast**, before you transmit the hash to compare the files.

But if you derive a password or a key using a hash you probably want it to be **slow**, because you want a brute force attack to be time consuming.

| Type         | Algorithm     | Usage    |
| ------------ | ------------- | ------------ |
| Key Derivation |             | kdf(key, salt, iterations) |
|              | PBKDF2        | pbkdf2(PRF, password, salt, iterations, keylength) |
