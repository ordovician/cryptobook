# Bitcoin explained in terms of Git

Git is quite well known to many. Having read about the Git data model, it helps me understand Bitcoin by relating it to how git is made. So I will try to explain Bitcoin in terms of Git. It is bound to be some inaccuracies. My motivation is not to be 100% correct but to make you understand the concept.

# High level similarities

Both Bitcoin and Git are distributed systems. Every node in a git system contains a full copy of the repository. Likewise every node in the Bitcoin network contains a full copy of the blockchain, which is essentially a ledger. With Git users explicitly syncronize with each other through push and pull operations. With Bitcoin this happens automatically.

## Objects

Both systems are made up of a few key types of objects. In git's case we have these objects:

* commit
* tree
* blob

A repository is essentially a chain of commit objects pointing to tree objects with again points to blob objects. With Bitcoin there are 3 essentiall objects:

* block
* transaction
* address

Each commit represent a snapshot of the repository for a point in time. A Bitcoin block is also related to time, in that it represents all the transactions which happened at a point in time. Whenever there is a collection of new files change we commit a hierarchy of tree and blob objects. The commit is attached to a previous commit. Likewise in Bitcoin a collection of new transactions are added to a block which is attached to a previous block.

A transaction consists of mutliple input and output addresses. One thing which is a bit counter intuinitive at first is that everything from an input has to be spent in a transaction. So if you have 10 bitcoins on an address and only want to send 4 to another user, then you create a transaction whith two outputs where one of the outputs is your own address, so 6 bitcoins gets sent back to your address.

The transactions form an acyclic graph. The amount of bitcoins at a particular address is never explicitly recorded in the system. To figure out the balance on a particular address you have to look at all the transactions going into an address and out of it and add and substract to get the present balance.

# Ramblings about how a Transaction is setup and works

Using the bitcoin client

    $ bitcoind createrawtransaction
    '[{"txid" : "9ca8f",
       "vout" : 0}]'
       
     '{"1Lnf" : 0.0250},
      {"1hvz" : 0.0245}'
     0100...1e34a...
     
This is a compressed form of what is in a transaction. The first argument to `createrawtransaction` is a JSON array of the inputs. For each input we have:

* **txid** the ID of the previous transaction.
* **void** which output from previous output is this input. 

So each output is assigned an index. 

The second argument, gives us a dictionary with key-values, where each key is a address to send bitcoins to. The value of the key is the amount to send. When you hit enter you get `0100...1e34a...` which is the whole transaction encoded in binary format (raw format). You can decode this to see all the info in the transaction which gets derived from what you write.

Most notable the decoded transaction will contain:

* An assigned transaction ID for this transaction. I believe this is a hash of most of the transaction data.
* The transaction script. Our input didn't specify any scripts all it said was to send some amount to given addresses. But the scripts give conditions for this to happen. The addresses are part of the script.

Before you can send transaction you need to sign it. Otherwise you have no proof that you are allowed to do this. 

	$ bitcoind walletpassphrase mypasswd 360
	
Unlocks your walled using passord  `mypasswd`.

	$ bitcoind signrawtransaction 0100...1e34a...
	{
		"hex" : 0100...1e3b3..
		"complete" : true
	}

The `hex` key contains the whole transaction encoded in binary with the new signature data added. You can decode this again with `bitcoind decoderawtransaction` to see how the transaction was changed. All the inputs will now contain a `scriptSig` which contains the signature along with the input script. This makes the transaction verifiable by others.

You can now send it with:

	$ bitcoind sendrawtransaction  0100...1e3b3..
	



[bitcoinwhite]: https://bitcoin.org/bitcoin.pdf