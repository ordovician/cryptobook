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


[bitcoinwhite]: https://bitcoin.org/bitcoin.pdf