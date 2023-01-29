# Intro to Scalability

Ethereum gas fees have risen astronomically as the network becomes more popular. The ability of retail investors to participate in new Ethereum-based offerings like DeFi is circumscribed by the ever-increasing cost of entry into the space.

Three main challenges presented by the success of mainnet Ethereum:

1. Spiking gas costs **price-out market share and impact user experience**. Best case is loss of low-value transactions and poor UX due to stuck transactions. Worst case is compromising healthy market operation like [Black Thursday](https://insights.glassnode.com/what-really-happened-to-makerdao/){target=\_blank}.
2. **Block Latency** is problematic in some applications
3. Pushing gas costs to users creates friction and impacts user experience. User has to navigate rather **complex effects**.

As a result, some users and products are migrating to other chains that offer lower costs. Off-chain scaling is capable of solving these problems by providing higher throughput, faster state advancement and gas cost abstraction. It can be transformative for application UX, but other chains lack the network effects and security offered by Ethereum.

Layer 2 protocols, or "rollups" promise users the ability to reduce gas costs and increase transaction throughput without sacrificing Ethereum security. At their most basic, Layer 2 protocols batch many transactions together and submit them to mainnet, saving significantly on gas costs. As we'll see in this unit, the specifics of the protocols are quite a bit more complex, and multiple implementations of this idea exist.

Various rollups have a lot to offer dapp developers and users. Some examples: support for native gas cost abstraction, meta-transactions, account abstraction. Subsidized gas, or gas cost is paid in relevant tokens. Better native support for smart contract wallets and features like social recovery.

If Ethereum is to maintain its dominance and network effect, it must scale. Layer 2 protocols are a major part of this effort.

## Terminology

In the following sections, we're first going to go through some of the _types_ of Layer 2 solutions. Then walk through examples of popular Layer 2 solutions. We're then going to talk about crosschain and blockchain interoperability. Finally, we're going to have live sessions and presentations based around L2 platforms such as Polygon, Optimism and more.

In this section, we'll typically refer to mainnet Ethereum as Layer 1 or L1 and whatever the scaling solution is as a Layer 2 solution (L2), a sidechain, sidechannel or a bridge.

## Conclusion

These are exciting and very new topics, please be aware that they are considered _very_ cutting edge and you should be extremely careful when using them.

Most of the protocols that are live on mainnet have made some compromises around decentralization and security, and it is important to be aware whether their risk profile matches your risk appetite. A good resource for learning more about particular solutions is [L2 Beat](l2beat.com){target=\_blank}. Also, please know that the documentation changes very regularly and perhaps not perceptibly. If you're currently building on a Layer 2 solution, we recommend joining the project's Discord, or wherever the community gathers, and making sure to follow their developer updates.

Let's dive in!
