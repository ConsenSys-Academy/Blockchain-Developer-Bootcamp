  Consensus Conclusion
====================

  Hopefully by now you feel like you have a sense of how distributed consensus works in a traditional network and how blockchains have innovated consensus protocols. While cryptographic primitives allow blockchain users to secure and validate current transactions, blockchain consensus protocols allow for a blockchain network to maintain a public ledger (the global state of the blockchain) in a decentralized way.

 Challenges of Consensus in Distributed Networks
-----------------------------------------------

 While blockchain consensus protocols have made great strides in decentralized networks, there are still some unsolved issues they're facing. Some of these (like the CAP theorem and forks) affect all general distributed networks while others, like Miner Extracted Value and 51% attacks, are specific to public blockchains. Here's a sampling and brief description of these challenges.

 * **Forks** As we mentioned in a previous section, Proof of Work and other blockchain consensus mechanisms can lead to network forks (Note: In general computing networking, forks are also called *partitions*). Some of these forks are voluntary (such as network upgrades), accidental (a node receives two valid but different new blocks) or adversarial (network participants purposefully breakaway from the main network to create a separate chain). While forks are common in all distributed systems, with blockchain networks they can be particuarly painful despite also serving as necessary update mechanisms.
* **Network Size** The [Scalability Trilemma](https://vitalik.ca/general/2021/04/07/sharding.html){target=_blank} details the different elements a blockchain needs to balance when it grows. Maintaining scalability and security relies on keeping the network size manageable. If the network size is too large, the equipment needed to run a full node is too much for an individual and leads to the enormous mining rigs we now see with Proof of Work blockchains. There are developments with Ethereum clients, like Geth's [snapshots](https://blog.ethereum.org/2021/03/03/geth-v1-10-0/){target=_blank}, which reduce the amount of space needed for clients. There is also a push for [light clients,](https://www.reddit.com/r/ethereum/comments/m0tqz5/making_the_ecosystem_more_lightclient_friendly/){target=_blank} or clients that can run on mobile phones or a browser.
* **[CAP Theorem](https://en.wikipedia.org/wiki/CAP_theorem){target=_blank}** This is a fairly technical concept and can be challenging to understand. To put it simply, the CAP Theorem states that when a distributed network forks (also called a *[partition](https://en.wikipedia.org/wiki/Network_partition){target=_blank}*), the network must either sacrifice consistency or availability. For example, if a blockchain network forks / partitions into two separate chains, you cannot expect those chains to both continue to mine new transactions (*Availability*) and stay consistent (*Consistency*) with each other. You don't need to be an expert in the CAP theorem, really just be aware of its existence and generally how it affects distributed networks. If you'd like to learn more, please see the links in "Additional Material" below.
* **Scalability** As we've mentioned before, blockchain consensus mechanisms, particularly Proof of Work, are limited by the amount of transactions they can process. If the block size (the amount of transactions processed) increases, then mining will become more centralized and only available to those with significant resources. However, the current transaction throughput (the amount of transactions processed) is not enough to compete against current mainstream financial payment mechanisms. There are significant challenges, mainly how to make Ethereum more light-client friendly. Meaning: how can we reduce the amount of resources needed to provide decentralized consensus?
* **51% attacks** In "11. Calculations" of the Bitcoin whitepaper, Nakamoto discusses the possibility of something called a "51% attack". This is the mathematical possibility of a malicious actor, who controls 51% or more of the network's hash rate, to both reorder some recent blocks and create a new, valid block including those tampered transactions. To be clear, this has not happened with Bitcoin or any major network, but it does exist as a possibility. Also, controlling 51% of a network's hash rate is only the entrance fee for doing such an attack. It also requires an enormous amount of coordination and subversion to make sure the attack is not noticed. Last, Proof of Work provides an economic incentive for the malicious actor with over 51% of the mining rate to actually produce *valid* blocks, rather than trying a re-organization attack.
* **Miner Extracted Value** This is a more recent concern in the Ethereum community and may be too technical for this part of the course so no worries if you don't get this yet. Put simply, a user may increase the miner's fee of a transaction to entice a miner to include the transaction in a block. That user can use this "frontrunning" effect to target users making sophisticated trades. With the increasing sophistication of Ethereum transactions, many feel MEV poses as serious issue to the ecosystem. Please see links below for more resources if you're interested.

 Conclusion
----------

 Blockchain consensus protocols, as kicked off by Proof of Work but including Proof of Stake and others, are the last primitive we need in our mental model to complete our blockchain framework. Now that we have both cryptography and distributed computing in our toolkit, we will now see how we can build a generalizable framework to understanding almost any blockchain network we encounter.

 Additional Material
-------------------

### Introductory

 * [Article: The Meaning of Decentralization](https://medium.com/@VitalikButerin/the-meaning-of-decentralization-a0c92b76a274){target=_blank}
* [Article: Sharding](https://vitalik.ca/general/2021/04/07/sharding.html){target=_blank} Discusses the scalability trilemma
* [Release Notes: Geth 1.10.0](https://blog.ethereum.org/2021/03/03/geth-v1-10-0/){target=_blank} Describes the snapshot feature implemented in Geth
* [Reddit: Making Ethereum More Lightclient Friendly](https://www.reddit.com/r/ethereum/comments/m0tqz5/making_the_ecosystem_more_lightclient_friendly/){target=_blank}
* [Article: The CAP Theorem (Dean Eigenmann)](https://dean.eigenmann.me/blog/2020/02/17/cap-theorem/){target=_blank} Another great post from the Distributed Systems newsletter describing the CAP theorem in a general way. Dean discusses how CAP theorem is particularly important with e-commerce like Amazon.
* [Article: The CAP FAQ](https://www.the-paper-trail.org/page/cap-faq/){target=_blank} A nice introductory article requiring some network knowledge.
* [Article: Eth2 Vision: The Challenge of Decentralized Scaling](https://ethereum.org/en/eth2/vision/){target=_blank} Scroll down a bit to see a diagram showing the "scalability trilemma"
* [Forum: How to Make the Ecosystem more Light-Client Friendly](https://www.reddit.com/r/ethereum/comments/m0tqz5/making_the_ecosystem_more_lightclient_friendly/){target=_blank} A Reddit discussion about Ethereum light-clients from 2021.
* [Article: What Everyone Gets Wrong about 51% Attacks (Dankrad Feist)](https://dankradfeist.de/ethereum/2021/05/20/what-everyone-gets-wrong-about-51percent-attacks.html){target=_blank} General discussion around 51% attacks, what they are, what they're not, and how Proof of Stake creates checkpoints which could avoid an adversarial re-organization attack.
* [Article: Flashbots: Frontrunning the MEV Crisis](https://medium.com/flashbots/frontrunning-the-mev-crisis-40629a613752){target=_blank} A great introductory discussion by the Flashbots research group dedicated to issue of Miner Extracted Value.
* [Interactive: Explore MEV in Real-time](https://explore.flashbots.net/){target=_blank} A visualization put together by Flashbots to document what they call MEV in real-time.
* [Article: Why Ethereum’s MEV Problem Is Way Worse Than You Think](https://www.coindesk.com/ethereum-mev-frontrunning-solutions){target=_blank} Opinion article describing the potential future problems facing Ethereum if it doesn't address Miner Extracted Value issues.
* [Video: WTF is MEV?](https://youtu.be/s3nACF7uVZw?t=405){target=_blank} Introduction to Miner Extracted Value from Charlie Noyes at a MEV Summit. This video starts at his talk but also includes the rest of the summit, which you don't have to watch!
* [Video: MEV Walkthrough with FlashBots](https://www.youtube.com/watch?v=lXq0eU8viFQ){target=_blank} Another walkthrough of MEV from Flashbots

### Advanced: Distributed Systems

 * [Wiki: Distributed Systems Reading List](https://dancres.github.io/Pages/){target=_blank} Strong technical and academic discussion around distributed systems
* [Article: How Complex Systems Fail](https://how.complexsystems.fail/){target=_blank} A series of simple statements referring to the management of chaos in complex systems. Highly generalized, but still has a number of gems.
* [Tutorial: Building a Distributed Turn-Based Game System](https://fly.io/blog/building-a-distributed-turn-based-game-system-in-elixir/){target=_blank} Fun tutorial around using distributed system language Elixir.
* [Wikipedia: Beer Distribution Game](https://en.wikipedia.org/wiki/Beer_distribution_game){target=_blank} A cute, general educational game teaching about the challenges of a distributed system using a common supply chain scenario.
* [Wiki: Sharding FAQ (Ethereum Foundation)](https://eth.wiki/sharding/Sharding-FAQs){target=_blank} First mention of the "scalability trilemma" a bit technical, however!
* [Article: You Can't Sacrifice Partition Tolerance](https://codahale.com/you-cant-sacrifice-partition-tolerance/){target=_blank}
* [Code: "11. Calcuations" Bitcoin whitepaper](https://bitcoin.org/bitcoin.pdf){target=_blank} The section where Nakamoto describes the race conditions needed to achieve a 51% attack.
* [Academic Article: Flash Boys 2.0](https://arxiv.org/abs/1904.05234){target=_blank} An in-depth discussion of the Miner Extracted Value theory.
* [Wiki: Resources from Flashbots about MEV](https://github.com/flashbots/pm#resources){target=_blank}
* [Article: Ethereum is a Dark Forest](https://medium.com/@danrobinson/ethereum-is-a-dark-forest-ecc5f0505dff){target=_blank} A long narrative account describing white-hat hackers attempt to frontrun the frontrunners. A good primary account of the challenges of Miner Extracted Value.

 
