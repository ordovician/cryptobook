# Key Distribution

When using private and public keys for encryption and decryption the issue is how to distribute your public keys so that the receiver can trust who owns the public key.


## Distributing keys with PGP

With key handling systems such as PGP there is no central authority to vouch for a public key (certificate). You can easily send a public key to some other party. The problem is for the other party to verify that the public key is indeed from you. To do that you can send a **finger print** of the public key (a hash of the public key). For example, a 128-bit MD5 fingerprint for SSH would be displayed as follows:

	43:51:43:a1:b5:fc:8b:b7:0a:3a:a9:b1:0f:66:73:a8

Receivers of your public key can then verify the public key by checking that it hashes to the same **fingerprint** that you told them over the phone or showed through a QR code.

### Generating fingerprints

If you use GPG through e.g. the *GPG Keychain Access* tool, then the name of your key is the same as what you wrote in the field for full name. So if your name is 'The Joker' then you can write:

	 gpg --fingerprint 'The Joker'
	 
And get output like this:

	pub   2048R/61DBE7BE 2014-04-02 [expired: 2014-04-04]
	      Key fingerprint = 0F4C 4446 AFDD 4305 3E8D  4E7D 17D8 76C2 61DB E7BE
	uid                  The Joker (Key made for testing purposes) <erik.thejoker@mac.com>


SSH keys you can usually find stored under `.ssh` in your home directory. You can get the fingerprints with using `ssh-add`:

	$ ssh-add -l
	2048 f7:4f:5b:19:8b:a5:c7:b1:b7:4b:72:4a:b1:8b:fa:1f work_id_rsa (RSA)
	2048 c5:23:cd:e6:3a:48:52:c2:5e:44:e9:1e:fc:f2:b1:32 github_rsa (RSA)

But if you want to look at a specific file you can do it like this:
	
	$ ssh-keygen -lf github_rsa.pub
	2048 c5:23:cd:e6:3a:48:52:c2:5e:44:e9:1e:fc:f2:b1:32  GitHub@ordovician (RSA)
	
### PGP word list

The whole existance and point of fingerprints from public keys is to allow humans to do an inspection of the fingerprints of two keys to see if they are the same. So a fingerprint should be distributed in the most secure way. One way is to read it out over a phone or write it down by hand on a card you show another person. The facilitate reading out loud the fingerprints PGP (GPG is an implementation of PGP) came up with a [special wordlist][pgpwordlist]. One word for every byte value. A PGP public key fingerprint that displayed in hexadecimal as

	E582 94F2 E9A2 2748 6E8B
	061B 31CC 528F D7FA 3F19

would display in PGP Words (the "biometric" fingerprint) as

	topmost Istanbul Pluto vagabond
	treadmill Pacific brackish dictator
	goldfish Medusa afflict bravado
	chatter revolver Dupont midsummer
	stopwatch whimsical cowbell bottomless

The order of bytes in a bytestring depends on Endianness.


[pgpwordlist]: http://en.wikipedia.org/wiki/PGP_word_list

