---
layout: post
title: "How Bitcoin Works (Basics)"
date: 2021-08-18
categories: [web3]
---

In this series, I'm going to explore how Bitcoin works. Focusing on the technical point of view, I'm trying to keep it as simple as possible. If you're interested in a political/economical perspective, I highly recommend "[The Bitcoin Standard](https://saifedean.com/thebitcoinstandard/)" from Saifedan Ammous.

In the first part, I'm trying to give an overview about Bitcoin. It's organised like "[Mastering Bitcoin](https://www.amazon.de/-/en/Andreas-Antonopoulos/dp/1491954388)" by Andreas Antonopoulos, but I've added/cutted some information.

## Which problem does Bitcoin solve?

Bitcoin provides an alternative to the current central bank-controlled fiat money. Transactions are made peer-to-peer, it doesn't require a third Party. In fact, there isn't a central authority at all. You don't need to trust anybody, you are able to *verify.* From a historical perspective, this is revolutionary.

<div style="text-align:center">
<img src="/wp-content/uploads/2021/08/image-1024x657.png" alt="Bitcoin peer-to-peer system" style="width: 70%; height: auto;">
</div>

Bitcoin is completely digital. But how does it prevent the [double-spending problem](https://www.investopedia.com/terms/d/doublespending.asp)?

We are able to provide digital signatures with *cryptography*. In that way, users can prove their ownership of that (digital) asset and it solves the double-spend issue.

## History of Bitcoin

Bitcoin was invented in 2008 with the publication of a paper called "Bitcoin: A Peer-to-Peer Electronic Cash System," written under the alias of Satoshi Nakamoto. He combined several prior inventions:

<div style="text-align:center">
<img src="/wp-content/uploads/2021/08/image-1-1024x711.png" alt="Bitcoin history timeline" style="width: 70%; height: auto;">
<figcaption>(Graphic created by <a href="https://twitter.com/danheld">Dan Held</a>)</figcaption>
</div>

The four key innovations brought together are:

* A decentralized peer-to-peer network (the bitcoin protocol)
* A public transaction ledger (the blockchain)
* A set of rules for independent transaction validation and currency issuance (consensus rules)
* A mechanism for reaching global decentralized consensus on the valid blockchain (Proof-of-Work algorithm)

## Wallets

Bitcoin is a protocol. If a client application speaks this protocol, it can be accessed. A *bitcoin wallet* is the most common user interface to the bitcoin system. Like there are many web browsers (firefox, chrome, …), there are different implementations of bitcoin wallets. They vary in quality, performance, security, privacy, and reliability.

Wallets can be categorized by their platform:

* Desktop wallet
* Mobile wallet
* Web wallet (user's wallet it stored on a server owned by a third party)
* Hardware wallet (devices that operate a secure self-contained bitcoin wallet)
* Paper wallet (keys controlling bitcoin are printed on paper, metal, …)

Or by their degree of autonomy and how they interact with the bitcoin network:

* Full-node client
  * stores the entire history of bitcoin transactions
  * can initiate transactions directly on the bitcoin network
  * complete autonomy
* Lightweight client
  * connects to full nodes for access to the bitcoin transaction information
  * stores the user wallet locally
* Third-party API client
  * all transactions go through a third-party
  * wallets *may* be stored by the user

## Getting started:

For someone who is not a technical user, a mobile wallet (like BlueWallet) is the best way to start. If you create a new Bitcoin wallet, you will be given a *mnemonic phrase.* These 12-24 English words are created randomly by the software. In case your mobile device is lost, you can restore your wallet with that seed phrase. But it needs to be stored carefully. The recommended way is to write down two copies on a paper and keep it on separate places.

The application also generated a *private key* which will be used to deduce *bitcoin addresses* that direct to your wallet. At this point, Bitcoin addresses are not registered within the bitcoin system. They are just random numbers that correspond to the private key. The private key provides access to the funds. Only once an address has been associated with a transaction does it become part of the known addresses in the network.

You can create new addresses as often as you like, all of which will direct funds to your wallet. Many wallets create automatically a new address for every transaction to maximize privacy.

## Making transactions:

<span style="text-decoration: underline;">Receive:</span>

Obviously, you need bitcoin in order to spend it. You can either receive bitcoin directly, or purchase some over an exchange.

<div style="text-align:center">
<img src="/wp-content/uploads/2021/08/image-2-1024x854.png" alt="BlueWallet receive screen" style="width: 70%; height: auto;">
<figcaption><a href="https://bluewallet.io">Bluewallet</a> (available for IOS/Android)</figcaption>
</div>

Another Person can send you bitcoin, either by scanning the QR-Code or by typing in the address manually. Bitcoin addresses start with *1, 3* or *bc1*. There is nothing sensitive, from a security perspective, about the bitcoin address. It can be posted anywhere without risking the security of the account.

<span style="text-decoration: underline;">Send:</span>

<div style="text-align:center">
<img src="/wp-content/uploads/2021/08/image-3-576x1024.png" alt="BlueWallet send screen" style="width: 70%; height: auto;">
</div>

The note/description input provides space for future reference. It will stored in the wallet and can only be seen by the owner.

Transactions are irreversible. Therefore, the inputs should be double-checked.

Once a transaction is signed with the private key, it quickly propagates across the bitcoin network via the peer-to-peer protocol. Meanwhile, the receiving wallet is constantly "listening" to published transactions.

## Confirmations:

Wallets will recognize a transaction within seconds, but it will be "unconfirmed". To be confirmed, a transaction must be included in a block and added to the bitcoin transaction ledger (blockchain), which happens every ~10 minutes.

## Transaction example:

Situation: Person A wants to buy a cup of coffee for 1$ (≈ 0,0000352 BTC). The shop owner creates a *payment request.*

Unlike a QR code that simply contains a destination bitcoin address, a payment request is a QR-encoded URL that contains:

* destination address
* a payment amount
* a generic description

<div style="text-align:center">
<img src="/wp-content/uploads/2021/08/image-4-1024x854.png" alt="Payment request screen" style="width: 70%; height: auto;">
<figcaption>payment request</figcaption>
</div>

Person A can now scan the QR-encoded URL with their smartphone.

<span style="text-decoration: underline;">Note:</span> The bitcoin network can transact in fractional values down to 1/100,000,000th of a bitcoin, which is known as a *satoshi*. There are already Layer 2 solutions, like the *Lightning Network*, which allows to split a bitcoin even further.

## How transactions work:

In simple terms, a transaction tells the network that the owner of some bitcoin value has changed. Each transaction contains one or more "inputs," which are like debits against a bitcoin address. On the other side of the transaction, there are one or more "outputs," which are like credits added to a bitcoin account.

It's like lines in a double-entry bookkeeping ledger:

<div style="text-align:center">
<img src="/wp-content/uploads/2021/08/image-5-1024x768.png" alt="Transaction as double-entry bookkeeping" style="width: 70%; height: auto;">
<figcaption>Transaction as double-entry bookkeeping</figcaption>
</div>

**Transaction chains**: Person A sends Bitcoin to Person B, Person B also spend Bitcoin afterwards. Therefore, the output of one transaction is the input of another transaction.

<div style="text-align:center">
<img src="/wp-content/uploads/2021/08/image-6-1024x768.png" alt="Chain of transactions" style="width: 70%; height: auto;">
<figcaption>Chain of transactions</figcaption>
</div>

Transaction inputs cannot be divided. Therefore, many transactions will include outputs that reference both, an address of the new owner and an address of the current owner, called the *change address*. Importantly, the change address does not need to match the input's address. It's often a new address from the owner's wallet (due to privacy reasons).

There are different ways how a wallet handles its inputs. It's like dealing with cash. If you doesn't have the correct amount, you can either use many small inputs, or a few large ones and receive change. A Bitcoin wallet developer tries to find a balance between these options.

## Constructing a transaction:

Firstly, the wallet application needs to find inputs to pay the required amount. A bitcoin wallet application that runs as a full-node client actually contains a copy of every unspent output from every transaction in the blockchain. This allows a wallet to construct transaction inputs as well as quickly verify incoming transactions as having correct inputs. But a full-node client takes a lot of disk space. Therefore, most user wallets run "lightweight" clients that track only the user's own unspent outputs (Inputs). Some don't maintain a copy at all, they retrieve the information from the bitcoin network through an API.

The Output is constructed as a script that creates an encumbrance. It says something like: " This Output is payable to whoever can present a signature from the key corresponding to Person X's address".

The sum of inputs is slightly higher than the sum of outputs. The resulting difference is the transaction fee that is collected by the miner as a fee for validating and including the transaction in a block to be recorded on the blockchain (more about that later).

<div style="text-align:center">
<img src="/wp-content/uploads/2021/08/image-7-1024x440.png" alt="Transaction inputs and outputs" style="width: 70%; height: auto;">
</div>

## Blockchain explorer:

The Blockchain explorer is a web application that allows you to search for addresses, transactions, and blocks and see the relationships and flows between them.

e.g. [Blockstream Explorer](https://blockstream.info)

## Adding the transaction to the ledger

The transaction contains everything necessary to confirm ownership of the funds and assign new owners. Now, the transaction must be transmitted to the bitcoin network where it will become part of the blockchain. It will be included in a new *block*. Once the block is *mined*, it will be added to the blockchain. With every new block, the security of the previous transactions will increase.

But how does a wallet propagate the transaction?

Any system that participates in the bitcoin network by "speaking" the bitcoin protocol is called a *bitcoin node*. A wallet application can send the new transaction to any bitcoin node it is connected. Any bitcoin node that receives a valid transaction it has not seen before, will immediately forward it to all other nodes to which it is connected (known as *flooding*).

What happens if the transaction reaches the receiving wallet?

Within seconds, the wallet will identify the transactions as an incoming payment. The wallet can independently verify that the transaction is well formed by checking previous unspent outputs and the transaction fees. With little risk, the receiver can assume that the transaction will shortly be included in a block.

## Bitcoin Mining

The bitcoin system of trust is based on computation. Transactions are bundled into blocks, which require an enormous amount of computation to prove. The mining process serves two purposes in bitcoin:

* Mining nodes validate all transactions by reference to bitcoin's *consensus rules*. Therefore, mining provides security for bitcoin transactions by rejecting invalid or malformed transactions.
* Mining creates new bitcoin in each block, almost like a central bank printing new money. The amount of bitcoin created per block is limited and diminishes with time, following a fixed issuance schedule (*halving*).

<div style="text-align:center">
<img src="/wp-content/uploads/2021/08/image-8.png" alt="Bitcoin halving schedule" style="width: 70%; height: auto;">
<figcaption>every 4 Years, the amount of "new Bitcoin" per block halves (Halving)</figcaption>
</div>

Mining achieves a fine balance between cost and reward. Mining uses electricity to solve a mathematical problem. A successful miner will collect a *reward* in the form of new bitcoin and transaction fees. However, the reward will only be collected if the miner has correctly validated all the transactions, to the satisfaction of the rules of *consensus*. This delicate balance provides security for bitcoin without a central authority.

The mathematical "puzzle" is based on cryptographic hash. It's asymmetrical hard to solve, but easy to verify. The difficulty is adjusted to the provided computation power, so a new block is found every ~10 minutes.

## Mining transactions in blocks:

New transactions are constantly flowing into the network from user wallets and other applications. As these are seen by the bitcoin network nodes, they get added to a temporary pool of unverified transactions maintained by each node. As miners construct a new block, they add unverified transactions from this pool to the new block and then attempt to prove the validity of that new block, with the mining algorithm (*Proof-of-Work*).

As soon as miners receive the previous block, they start mining a new block, knowing they lost the previous round. Each miner includes a special transaction in their block, one that pays their own bitcoin address the block reward (currently 6.25 newly created bitcoin) plus the sum of transaction fees from all the transactions included in the block.

Each new block is built on top of the others and adds even more computation to the blockchain. This counts as an additional confirmation, thereby strengthening the trust in the transactions.

The more blocks are found, it becomes exponentially harder to reverse the transaction.

<span style="text-decoration: underline;">Sidenote:</span> The first Block, also known as *genisis block,* was mined on January 3, 2009.

This should cover up the basics. If you want to go further, I've written a [second part](/how-bitcoin-works-advanced/).