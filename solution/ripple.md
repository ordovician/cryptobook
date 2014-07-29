# Ripple explained in terms of Bitcoin

Here is a translation of Bitcoin terminology to Ripple:

Bitcoin        | Ripple          | Comment
---------------| --------------- | ------------
Block          | Bundle / Ledger | A Bundle is just part of a ledger. 
               | Closing Bundle  | Block currently being verified
               | Proposal        | List of transaction other servers think should be in Closing bundle
               | UNL             | Unique Node List. A node is a server or collection of servers controlling one private key. If two private keys are controlled by the same node then it is not a unique node.
 Blockchain    | Ledger list     | Ripple doesn't require keeping a list of previous ledgers 
 Proof of work | Consensus       | Ripple isn't based on majority CPU power but majority vote of nodes trusted to not cooperate.
Address        | Account         | Just like Bitcoin accounts are hashes of public keys of account holder.
## Consensus

With Bitcoin we have the blockchain and a new block is verified by having other computer / nodes calculate and create a blocks on top of the new block. So in Ripple **Consensus** is how a *block* get added to the ripple *blockchain* which is called a *ledger* using Ripple terminalogy. Consensus is an interative process. 

Each iteration lasts a specific amount of time. In this period the server receives **proposals** for transactions to include in the **closing bundle**. It only considers proposals coming from servers in its **UNL**. The **UNL** is something each server has to build up manually by the administrator chosing nodes he/she believes can be trusted not to collude. Other than that they may very well be liars and cheaters.

Every transaction in a proposal comming from a UNL approved server gets one vote. For each iteration a cerain amount of votes needs to be obtained for the transaction to be included in the proposal that the server sends out.

This vote requirement increases for each iteration so that all servers will converge towards one approaved list of transactions. When **80% votes** is achieve then these transactions are added to the closing bundle and the closing bundle is attached to the ledger, which now becomes the new **Last Closed Ledger**.

## The Blockchain vs a Ripple Ledger

A Ripple Ledger really corresponds most closely to a block in the Bitcoin blockchain. Nodes don't need the whole history of ledgers to verify transactions unlike Bitcoin.


## Transaction field

Name           | Type            | Comment
---------------| --------------- | ------------
transactionID  | Int             | I think this is the signature (encrypted hash of other fields)
accountFrom    | Bytes           | An account is 160-bit hash of public key in base-58
fromPubKey     | Bytes           | To prove transaction is authorized
sourcePrivate  | Bytes           |
inLedger       | Int             |
status         | Enum            | complete, invalid, comitted ... ?

All these fields are serialized and a magic number is added. Then this is turned into a 256-bit hash which is signed. This signature is added to transaction as a field. Now a different 32 bit magic number is used.

## Terminology and comparison to traditionally banking

### clearing
Denotes all activities from the time a commitment is made for a transaction until it is settled. In 1600s banks settled payments by courier. In 1800 they all met in central location called a banker's clearing house. In the clearing house they would add up checks and figure out how much they owed each other and pay in cash.

### Security
Tradeable financial asset such as bank notes, bonds, stocks etc. 

### Settlement
Delivery of a security for payment. First you make a trade, which is really just a contract about what to do. Settlement means papers denoting ownership are actually physically transfered and are then by law part of that persons property and protected against default by other party.

### Draft
A form of checkque. A Cheque is a draft which can be withdrawn immediatly. In general a draft is a promise of future payment.

### Giro vs Cheques
A Giro is a payment transfer from one bank account to another instigated by the payer. Mainly a European phenomenon. 

With **checks** the person who wants to pay writes the check and hands it over to the one who wants payment (payee). The receiver takes the check to the bank where it is *cleared*. The check must go to the clearing house if I understand correctly and after this is done the money is paid out. So a check is payment from a bank account into cash. While a Giro is a transfer from a bank account to another. The payer writes a giro and sends it by post to a giro centre (think postgiro). The major distinction is that with the post giro model an individial can move money directly from his bank account to another one as long as they have the recipients account number. 

With direct deposit as used in North America you can't tranfer money to someone without approval. So you need to visit the bank in person or do wire transfer.

##### Summary
My own understanding is that cheques **pull** money while giro **push** money. You can give a cheque to the store for payment because it doesn't need to specify receiving bank account number. A giro is usually printed by the one who wants to receive payment so that they can write details about what their bank account number is.


### Remitter
Person making payment.

### Credit

Buying on credit is to offer a promise to pay later. So when the purchase has happened this promise becomes a debt. Credit is extended by lender, meaning the lender says how much they will allow you to owe them. In Ripple terms the creditor/lender sets up a trust line with a limit. This limite is the extended credit.

**creditor** is lender<br>
**debtor** is a borrower<br>

In computer games, the player often has a certain amount of credits to pay for building things. So the credits are "money" the player can use, but it isn't money the player physically has but promises to pay something back of that value.

**Trade credit** Offer of delayed payment for purchase of goods.

Think of how credit card companies extend a certain amount of credit to the card owner. The credit is a sum of money which size is reflected in how much the credit card company thinks you will be able to repay.

### Counter party
Somone exposed to risk (person or company). E.g. the person lending money.

### Counter party risk
Risk that borrower will not pay owed money. E.g. a Ripple Exchange or bank essentially borrows the money which you have on your account. The amount on your account is a statement of a IOU. 

### Money
Medium of exchange. Or if we have the debt view of money they money is a IOU token of some form. It could also be related to a measure of value. 

### Arbitrage
Taking advantage of difference in market prices.

### Credit risk
The lenders risk. Lost principal (lended amount) or interest.

### Principal
The amount the lender lends, or borrower borrows.
