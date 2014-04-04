# Strength of a Cryptographic Algorithm

You can always try a brute force attack by trying every possible private key to decrypt a message. Thus the strength is related to the number of bits in the key.

However there is often an approach which allows you to do less brute force attacks than the number of bits suggests. E.g. if a 32 bit key requires 2^32 attempts to break it has a security of 32 bits. However if there exists a smarter approach which only requires  2^12 attempts then the security is just 12 bits.

A RSA key of length 1024 e.g. has security of 80 bits. 

# BLS

Elliptic curve based. Is currently the strongest encryption algorithm known. Can use the shortest keys for digital signing. Can securely sign with a 128 bit key. 80 bit might be possible if you strech it. Can get you down to **20 bytes** long signatures (160bit).

[PBC][pbc] is a C library for performing BLS signatures.

# DSA and ECDSA

DSA and *Elliptic Curve DSA* is currently the most commonly algorithms for digital signatures.

Using a 320 bit key you can get down to signature sizes of about 40 bytes.


[pbc]: http://crypto.stanford.edu/pbc/