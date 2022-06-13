Trustless Consensus
===================

  *Note: this section is fairly text heavy and may be difficult to understand at first. Not to worry! The two videos following this section cover similar material in a visual way. We'll also discuss this in our Office Hours or on Discord.* 

We've spent the past few sections learning about how consensus protocols work to make peer-to-peer distributed systems maintain state across time despite node failure. This is a general computer science concept that's used in building distributed networks that may be susceptible to machine failures, message duplications, message corruptions, etc. Since they are decentralized networks, public blockchains have to deal with this category of problems. But, they are also presented with an entirely new set of issues.

 Public blockchains introduce a specific challenge to agreeing on a state. In a non-blockchain distributed network, state is a set of data valuable really only to the private organization running the network. For example, in a digital streaming service, the state might contain where a user stopped watching a previous video. That way, if they start the video again and are served the content from a different network server, their place will be saved.

 The state of a public blockchain network, on the other hand, is the public, distributed ledger which contains the financial balances of everyone in the network. This has enormous value to many different organizations and individuals. In a way, everyone is incentivized to lie about the state of the network because it's directly tied to their net worth. Imagine if when you went to the bank, rather than a bank teller telling you your balance, *they* asked *you* for *your* balance. Most people would, at some point, be very tempted to lie and make up a number (Probably a very large number).

 This is the main element that distinguishes public blockchain networks from traditional distributed networks. The network state of a blockchain is one that contains economic value directly impacting the actors in the network. But, as we've seen studying traditional distributed systems, the blockchain network still needs those nodes (which have competing interests) to update and propagate the state.

 Enter **trustless consensus:** Bitcoin solves this issue by creating a consensus mechanism which can operate in an adversarial environment where the nodes have competing interests. Rather than assuming the state they are propagating is correct, Bitcoin's trustless consensus allows each individual node to verify the state themselves using cryptography. We'll walk through how Bitcoin and other proof of work blockchain networks achieve this feat by describing the underlying assumptions and the solutions.

 
> Quick aside: What about current traditional banks? Don't they have distributed networks that contain economic value among nodes (customers) with competing interests? Why don't we consider them as solving this issue? Yes, this is true that global financial companies or governments have built distributed networks that have similar conditions to what public blockchains are hoping to achieve. However, these traditional networks separate trust from distributed consensus in their networks. You can imagine it like a castle, with powerful fortifications, that contains a ledger containing all the assets in the kingdom. If you can breach the defenses and get into the castle, you'll have control over that ledger. Blockchain's theoretical innovation is baking the defense *into* the consensus mechanisms themselves so there are many different castles and, if one falls, it may temporarily impact the network but will not collapse the system. 

 In fact, because blockchains are removing trusted intermediaries (like a bank) the only way to make their network state secure is to assume that *everyone* is lying. With your trust assumptions low (assuming everyone is lying), you're protected against that behavior. How do you create a consensus protocol in these dire circumstances? Well, this is the incredible innovation that blockchains, beginning with Bitcoin, created. It not only built the ecosystem of blockchain networks we see in today's world, but it even solved a general distributed computing problem in the process.

Double Spend and Byzantine Generals Solution
--------------------------------------------

 The biggest issue facing digital money is what is called the ["double spend"](https://www.investopedia.com/terms/d/doublespending.asp){target=_blank} problem: Since digital files can be copied endlessly, how can you be sure whatever digital money you're paid with has not been previously spent?

 This is the critical issue Satoshi Nakamoto set out to solve in [the Bitcoin whitepaper](https://bitcoin.org/bitcoin.pdf){target=_blank}: 
>  We propose a solution to the double-spending problem using a peer-to-peer network. The network timestamps transactions by hashing them into an ongoing chain of hash-based proof-of-work, forming a record that cannot be changed without redoing the proof-of-work. The longest chain not only serves as proof of the sequence of events witnessed, but proof that it came from the largest pool of CPU power. As long as a majority of CPU power is controlled by nodes that are not cooperating to attack the network, they'll generate the longest chain and outpace attackers. The network itself requires minimal structure. Messages are broadcast on a best effort basis, and nodes can leave and rejoin the network at will, accepting the longest proof-of-work chain as proof of what happened while they were gone. 

 

Nakamoto Consensus, also called Proof of Work consensus, creates a consensus mechanism for a digital money system where each individual node does not have to blindly accept the network state.

 Elements of Proof of Work Consensus
-----------------------------------

In discussing the elements comprising Proof of Work consensus, we'll pull from concepts we mentioned previously in our discussion of traditionally distributed networks. Specifically, you'll need to remember the concept of **messages**, the concept of **nodes** and the **roles** they play as well as the concept of **time** and **periods** in distributed systems.

### Messages

In Proof of Work consensus, the fundamental message is a **transaction,** constructed using the public key cryptography and digital signatures primitives we discussed previously, "trustlessly" (cryptographically) ensuring the identity and integrity of the message.

Transactions in Proof of Work consensus are **[atomic,](https://en.wikipedia.org/wiki/Atomic_commit){target=_blank}** meaning the network either accepts or rejects the transaction, there is no in-between or halfway. If the network accepts the transaction, the network state then advances to incorporate the effects of the transaction.

For example, let's say an imaginary public ledger at `State-0` says Alejandro has `1 token` and Barbarella has `0 tokens`. Alejandro then submits a transaction to the network saying he would like to pay Barbarella `0.5 tokens`. The network accepts the transaction, which creates a new state, `State-1` in which the public ledger has been updated to show Alejandro now has `0.5 tokens` and Barbarella has `0.5 tokens`.

### Nodes and their Roles

In Proof of Work consensus, here are the roles nodes play: 
- **Miners** These are the nodes which are certifying which transactions are valid by including them in blocks and receiving the block reward. When a miner creates a valid block and propagates it throughout the network, the network state is advanced in a trustless way. (We'll examine in a moment how a miner can create a block in a trustless way.)
- **Full Nodes** These are the general network nodes which are creating transactions and passing along transactions created by other nodes in the network. They are also maintaining full network state when they receive valid blocks from Miner nodes. Each full node in the network checks the work of a block to ensure its validity.
- **Light Nodes** These are network nodes which are simply submitting transactions to the network and waiting for them to be accepted by the network. They do not participate in the process of checking the validity of the advancing network state and do not pass along messages.
- **Archive Nodes** Similar to a full node, it maintains and provides the current state, but also maintains and provides historical states. e.g. balance at x date.

 *Remember from the section on public key cryptography that nodes identify themselves in the network by using the peer-to-peer identity mechanism of public key cryptography.*

 

### Periods and Proof of Work

In Proof of Work consensus, there are two distinct periods in a network: 
* **Period of Block Production** This is the period in which Miner nodes validate transactions by bundling them all together and competing to produce a valid Proof of Work algorithm. It begins when the miner receives the latest valid block and stops when the miner solves their Proof of Work algorithm or receives a valid block from another miner.
* **Period of Block Propagation** This is the period in which a valid block gradually moves through the network. A full node or miner node will only propagate blocks that are valid, so the process of the network accepting a valid block (and accepted the new network state) is an emergent one.

  The following section will describe the process of creating a block and how blocks chained together create an immutable ledger that all network participants can validate on their own. This individual validation, without having to rely on trust, is how proof of work consensus maintains state in a distributed and safe way. 

Additional Materials
--------------------

### Introduction

 - [Video & Interactive Code: ETH.Build with Byzantine Generals' Problem](https://www.youtube.com/watch?v=c7yvOlwBPoQ&list=PLJz1HruEnenCXH7KW7wBCEBnBLOVkiqIi&index=7){target=_blank} Austin Griffith walks through a [hands-on implementation](https://sandbox.eth.build/build#3f3d25b54ec9fde9b34ba3a8cd505d8306f97eec4537cd707f7e92b5d9226bf4){target=_blank} of the Byzantine Generals' Problem with his amazing ETH.Build platform
 - [Article: What is the Byzantine Generals Problem?](https://river.com/learn/what-is-the-byzantine-generals-problem/){target=_blank}
 * [Interactive Code: Anders Blockchain](https://andersbrownworth.com/blockchain/){target=_blank} A great, web-based interactive tutorial going over fundamentals of Proof of Work consensus including [block production through hashing](https://andersbrownworth.com/blockchain/block){target=_blank} and [distributed blockchains](https://andersbrownworth.com/blockchain/distributed){target=_blank}
 * [Article: How Satoshi Nakamoto Solved the Byzantine Generals Problem](https://news.bitcoin.com/triple-entry-bookkeeping-how-satoshi-nakamoto-solved-the-byzantine-generals-problem/){target=_blank}
 * [Wikipedia: Directed Acyclic Graphs](https://en.wikipedia.org/wiki/Directed_acyclic_graph){target=_blank} Because each new block embeds the hash of the previous valid block, this creates a computer science data structure known as Directed Acyclic Graphs (similar to the way Git software works!).](https://ethereum.org/en/developers/docs/nodes-and-clients/#)

### Advanced

* [Code: Implementing Proof of Work](https://github.com/cooganb/bitcoin-whitepaper-exercises/blob/master/pow/README.md){target=_blank} A continuation of the series from Kyle Simpson
* [Code: Implementing Mining Protocol](https://github.com/cooganb/bitcoin-whitepaper-exercises/blob/master/incentives/README.md){target=_blank} A continuation of the series from Kyle Simpson

 

