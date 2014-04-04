# Certificate

Given a user **A** and a Certificate authority (CA) **X** then a certificate for **A** issued by **X** consists of:

* Identity of **A**
* **A**'s public key
* expiry date
* signature created with **X**'s private key

A signature is created by hashing the fields:

* Identity of **A**
* **A**'s public key
* expiry date

Then encrypting the hash value with the private key of **X**. If user **B** wants to validate that he/she has the **A**'s public key then she uses **X**'s public key to decrypt the signature on **A**'s certificate. Then she hashes the 3 other fields and compares this value with the decrypted signature.

For this to work we assume that **X** has made an effort to make sure that **A**'s public key belongs to **A** and **A** is who he/she says she is.

### Code Signing Identity
A Certificate and its Private Key together can be referred to as 'identity' or 'Code Signing Identity

### Certificate level

How secure is the certificate. Meaning how did the CA (Certificate Authority) validate the identity of the owner of a public key. It could have been validated with:

* Email
* SMS message
* Passport (manual process)

### Chaining

**X** could sign certificate of **A** with his private key, and then **A** could sign certificate of **B** with his private key.

A VA (Validation Authority) can be used to validate a whole chain.

### Possible usage of Certificate

With a certificate from **A**, **B** can send encrypted messages to **A** or verify that a document is from **A** by looking at its signature.
