# Key Distribution

When using private and public keys for encryption and decryption the issue is how to distribute your public keys so that the receiver can trust who owns the public key.


## Distributing keys with PGP

With key handling systems such as PGP there is no central authority to vouch for a public key (certificate). You can easily send a public key to some other party. The problem is for the other party to verify that the public key is indeed from you. To do that you can send a **finger print** of the public key (a hash of the public key). Receivers of your public key can then verify the public key by checking that it hashes to the same **finger print** that you told them over the phone or showed through a QR code.