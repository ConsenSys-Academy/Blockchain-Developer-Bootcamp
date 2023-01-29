# Crosschain Communication and Blockchain Interoperability

In this section, we're going to discuss about why blockchain networks might want to communicate to each other and how that occurs. We mentioned way back in the "Blockchain Fundamentals: Network Configurations" section about the compatibility of certain blockchains and how they might link together. We're going to spend this lesson discussing this in more detail

## Why?

From [Peter Robinson](https://twitter.com/drinkcoffee2010){target=\_blank}:

> [T]here is no one blockchain to rule them all. There are public permissionless blockchains such as Ethereum Mainnet, Bitcoin, and Filecoin. There are many instances of permissioned, consortium blockchains such as Enterprise Ethereum / Quorum, Corda and Hyperledger Fabric. Within the public permissionless Ethereum space, Sidechains and Roll-ups (L2s) are emerging to improve scalability. All of these technologies need Crosschain Communications to allow them to communicate. Even if the world settled on one blockchain technology platform, all data and all functionality is unlikely to reside on just one instance of the blockchain platform.

Crosschain communications allows data (state) and functionality (execution) that resides on one blockchain to be accessible from another blockchain.

The seeds of crosschain communication can be found in the Bitcoin whitepaper. Under the section, "Simplified Payment Verification," Nakamoto writes:

> It is possible to verify payments without running a full network node. A user only needs to keep a copy of the block headers of the longest proof-of-work chain, which he can get by querying network nodes until he's convinced he has the longest chain, and obtain the **Merkle branch linking the transaction to the block it's timestamped in.** He can't check the transaction for himself, but by linking it to a place in the chain, he can see that a network node has accepted it, and blocks added after it further confirm the network has accepted it.

![Diagram of a Simplified Payment Verification from Bitcoin whitepaper](../../../img/S08/spv-1.png)

This "light" process proves the validity of a transaction by including the verified (mined) block header hash it appeared in as well as [the Merkle Proof](https://blog.ethereum.org/2015/11/15/merkling-in-ethereum){target=\_blank} showing how the individual transaction is included in that hash.

Developers realized they could use this implementation to build something that would validate Bitcoin payments on another chain entirely, and used it to build one of the first blockchain bridges, [BTC Relay](https://buildmedia.readthedocs.org/media/pdf/btc-relay/latest/btc-relay.pdf){target=\_blank}.

![Simplified notion of BTC Relay](../../../img/S08/btc-relay-1.png)
_Simplified Diagram of BTC Relay using transactions mined on Blockchain A to validate action on Blockchain B_

BTC Relay used the Simplified Payment Verification to move Ether from one account to the other using a Bitcoin transaction. Transactions could only be validated if the block header they relate to is on the longest chain and if at least six block headers have been posted on top of the block header that the transaction relates to. As attackers can not produce a longer chain than the main Bitcoin blockchain due to the mining difficulty, they are unable to confirm transactions based on a malicious fork.

Other mechanisms of doing similar crosschain action include [Hash Time Locked Contracts](https://en.bitcoin.it/wiki/Hash_Time_Locked_Contracts){target=\_blank}. These simple constructions allow two parties to exchange tokens on two separate blockchains without trusting each other.

## How?

Crosschain communication relies on the concept of **Atomicity.** We previously spoke about atomicity in "Trustless Consensus." An [atomic](https://en.wikipedia.org/wiki/Atomic_commit){target=\_blank} message is accepted or rejected by a network, there is no in-between or halfway.

Let's take a look at what that means:

![Crosschain Atomic Communication](../../../img/S08/atomic-1.png)

In the image above, a user submits a transaction that calls the `crossSwap` function on the `Cons` contract on the `Source Blockchain`. The function uses the message sender as the account to transfer from. The account to transfer to and the amount are specified by the `to` and the `val` parameters. If the user’s account doesn’t have a large enough balance then the transaction terminates with a revert error. Otherwise, the `to` and `from` account balances are updated and a crosschain function call is executed to execute the destination blockchain part of the crosschain transaction.

Along with Atomicity, crosschain communication also requires **Liveness** of the networks involved. This means that the network is progressing in a stable, safe way. For example, the BTC Relay only works if the Ethereum network keeps up with the blocks being mined on Bitcoin. Only a series of uninterrupted Bitcoin blocks transmitted to the Ethereum smart contract ("liveness") will allow the Simplified Payment Verification to work.

Without liveness, the networks involved cannot capture the crosschain communication and incorporate it into their respective global states.

## Events

Many EVM-based protocols rely on transferring information between blockchains using [Events](https://ethereum.org/en/developers/tutorials/logging-events-smart-contracts/){target=\_blank}. Transactions that trigger events programmatically generate log events that are stored in transaction receipts.

The transaction receipts for all transactions in a block are stored in a modified Merkle Patricia Tree. The root hash of this tree is stored in the Ethereum block header. The log event information includes: the address of the contract that emitted the event, an identifier known as a topic that specifies the type of event that is emitted, and a data blob containing the encoded event parameters. This ability to programmatically produce events can be used to produce information on a source blockchain that can be consumed on a destination blockchain.

## Examples of Crosschain and Blockchain Interoperability

- [Celo Optics by cLabs](https://medium.com/celoorg/announcing-optics-a-gas-efficient-interoperability-standard-for-cross-chain-communication-e597163b2){target=\_blank} Validators sign and transfer state roots to destination blockchains. Validators can be slashed on the source chain for signing invalid state roots.
- [Cross-Chain Interoperability Protocol by Chainlink](https://blog.chain.link/introducing-the-cross-chain-interoperability-protocol-ccip/){target=\_blank}
- [Connext's Noncustodial Xchain Transfer Protocol (NXTP)](https://medium.com/connext/nxtp-a-simpler-xchain-protocol-88760697ea04){target=\_blank} Uses HTLCs as the underlying crosschain consensus mechanism.
- [Cosmos Inter-Blockchain Communication (IBC)](https://github.com/cosmos/cosmos/blob/master/WHITEPAPER.md){target=\_blank} A multi-blockchain system in which blockchains called Zones communicate transactions via a central blockchain called a Hub. The Zones and the Hub typically use [Tendermint](https://tendermint.com/ibc/){target=\_blank} a type of Practical Byzantine Fault Tolerance consensus algorithm.
- [Rainbow Bridge by NEAR Protocol](https://near.org/blog/eth-near-rainbow-bridge/){target=\_blank} Uses NEAR's Rust execution environment to power crosschain Simplified Payment Verification transactions with a threshold number of validators to attest.
- [Polkadot](https://polkadot.network/technology/){target=\_blank} Uses a relay chain to coordinate information across many ["parachains"](https://wiki.polkadot.network/docs/learn-architecture){target=\_blank}. The parachains can also "connect with external networks via bridges."
- [BSC's Binance Bridge](https://www.bnbchain.org/en/bridge){target=\_blank} This is a two-way bridge between Binance's Smart Contract network (which is EVM-compatible) and Ethereum mainnet.

## Additional Material

- [Video: Building Bridges, Not Walled Gardens](https://www.youtube.com/watch?v=ZQJWMiX4hT0){target=\_blank} An argument for bridges and crosschain communication from James Prestwich of cLabs.
- [Academic Article: Survey of Crosschain Communications Protocols (Peter Robinson)](https://arxiv.org/abs/2004.09494){target=\_blank} A comprehensive technical overview of the requirements and characteristics of crosschain communication.
- [Academic Article: General Purpose Atomic Crosschain Transaction protocol](https://arxiv.org/abs/2011.12783){target=\_blank} A standardized, composable way to conduct crosschain transactions across EVM blockchains.
- [Article: Logging Events Using Smart Contracts (Ethereum.org)](https://ethereum.org/en/developers/tutorials/logging-events-smart-contracts/){target=\_blank}
- [Wiki: Chainlist](https://chainlist.org/){target=\_blank} A list of EVM-compatible networks
<!-- TODO: The document is not publicly available. Either make it accessible or remove this entry. -->
- [Wiki: Crosschain Comparison (Peter Robinson)](https://docs.google.com/spreadsheets/d/1bEJRcAM7ahBZK21zmDAH5mJoLM6wE0lG1IsySm-CCqk){target=\_blank}
- [Article: Blockchain Interoperability: An Overview Of The Current Research (ConsenSys)](https://consensys.net/blog/news/blockchain-interoperability-an-overview-of-the-current-research/){target=\_blank}
- [Article: Build {on} bridges, not [behind] walls (Andrew Hong)](https://ath.mirror.xyz/Y2XBh3HRu5B0S3qw974txvIv0JDz7Tu-yIKVTes7DUU){target=\_blank} An analysis of the current state of bridges in blockchain networks.
