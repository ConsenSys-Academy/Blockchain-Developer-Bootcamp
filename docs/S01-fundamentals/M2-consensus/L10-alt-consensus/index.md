More Forms of Consensus
=======================

We've spoken mainly about Proof of Work, since it's the current consensus mechanism for Bitcoin and Ethereum, as well as other blockchains. However, there are other consensus protocols being used by blockchain networks, such as:

- **[Proof of Stake](https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/){target=_blank}** A consensus protocol based on financial holdings of validator nodes in the network (similar to miner nodes in Proof of Work). Proof of Stake requires much less energy to run than Proof of Work and, for this reason, Ethereum is currently working towards this consensus mechanism.
- **[Delegated Proof of Stake](https://www.gemini.com/cryptopedia/proof-of-stake-delegated-pos-dpos#section-delegated-proof-of-stake){target=_blank}** This is a variant of the Proof of Stake protocol in which stakeholders can elect validators to represent them in the system.
- **Proof of Authority** This is a more traditional consensus mechanism like Raft's leader-led consensus in which only certain nodes are allowed to produce blocks at their discretion. It's meant for smaller, perhaps private networks where the participants all know each other or for lower-stake networks such as [testnets](https://en.wikipedia.org/wiki/Testnet){target=_blank} or networks securing trivial amounts of value.

 

Why would we need another consensus mechanism for blockchains, if Proof of Work is so innovative? A few reasons: 
- **Accessibility** The barriers to entry to becoming a PoW miner are high. Proof of Work chains require a substantial amount of energy to maintain. A miner must purchase, set up, and maintain all the necessary hardware to run a PoW mining rig. Additionally, PoW mining is extremely energy-intensive.
- **Centralization** Barriers to entry for mining can have the adverse secondary effect of greater centralization of miners. As it gets more costly and less profitable to become a miner, the network naturally sees a concentration of mining into two categories. First, large mining conglomerates that operate in areas with low electricity costs and cold weather (to reduce the cost of manually cooling mining hardware) such as Mongolia and Siberia. Second, mining power is centralized in the hands of mining pools. As it becomes less profitable for most people to mine individually, they buy hash power from a mining pool, which operates as a single mining entity. By the end of 2019, over 50% of blocks on Ethereum were mined by just two mining pools.

 

Proof of Stake
--------------

Proof of Stake is a different kind of consensus mechanism blockchains can use to agree upon a single true record of data history. Whereas in Proof of Work miners expend energy (electricity) to mine blocks into existence, in Proof of Stake validators commit stake to attest (or ‘validate’) blocks into existence.

**Validators** are the participants on the network who run nodes (called **validator nodes**) to propose and attest blocks on a Proof of Stake network. They do so by staking crypto on the network and make themselves available to be randomly selected to propose a block. Other validators then “attest” that they have seen the block. When a sufficient number of attestations for the block has been collected, the block is added to the blockchain. Validators receive rewards both for successfully proposing blocks (just as they do in Proof of Work) and for making attestations about blocks that they have seen.

The crypto-economic incentives for Proof of Stake are designed to create more compelling rewards for proper behavior and more severe penalties for malicious behavior. The core crypto-economic incentive boils down to the requirement that validators stake their own crypto––i.e. money––on the network. Instead of considering the secondary cost of electricity to run a Proof of Work node, validators on Proof of Stake chains are forced to directly deposit a significant monetary amount onto the network. 

Validators accrue rewards for making blocks and attestations when it is their turn to do so. They are penalized for not following through with their responsibilities when it is their turn to do so – i.e. if they are offline. Penalties for being offline are relatively mild and equate to about the same as the expected rewards over time. So, if a validator is participating correctly more than half the time then her rewards will be net positive. 

Should a validator attempt to attack or compromise the blockchain by trying to propose a new set of data history, however, a different penalty mechanism kicks in: a substantial portion of their staked amount will be slashed (possibly up to the whole amount of stake) and they will be ejected from the network. The result is a tremendous financial risk of a failed attack by a validator. To draw an analogy to Proof of Work, it would be as if a miner who failed an attack on a PoW chain was forced to burn down her entire mining rig instead of just eating the cost of the electricity she spent on a failed attack. Furthermore, this architecture places the security of the network directly in the hands of those maintaining the network and holding its native crypto-asset in the protocol itself.

Proof of Stake is used most notably in Ethereum 2.0 (more on that later) and other blockchain networks such as [Cardano](https://www.gemini.com/cryptopedia/cardano-ada-staking-blockchain){target=_blank}, [EOS](https://www.gemini.com/cryptopedia/eos-crypto-enterprise-blockchain-eosio){target=_blank} and [PolkaDot](https://www.gemini.com/cryptopedia/polkadot-crypto-dot-coin){target=_blank}. It's also used in Layer 2 solutions such as [Polygon Proof of Stake](https://consensys.net/blog/blockchain-explained/analyzing-polygons-proof-of-stake-network/){target=_blank} (we'll discuss Layer 2 solutions later as well)

It's important to note that a blockchain network does not have to use Proof of Work in their consensus mechanism. Bitcoin and Ethereum currently use it, but that does not mean it's the only game on the block!

Additional Material
-------------------

* [Wiki: Consensus Mechanisms (Ethereum.org)](https://ethereum.org/en/developers/docs/consensus-mechanisms/){target=_blank}
* [Article: What is Proof of Stake (ConsenSys)](https://consensys.net/blog/blockchain-explained/what-is-proof-of-stake/){target=_blank}
