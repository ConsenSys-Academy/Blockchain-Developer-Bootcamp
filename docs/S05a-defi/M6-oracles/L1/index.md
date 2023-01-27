# Oracles in DeFi

[Oracles](https://ethereum.org/en/developers/docs/oracles/){target=\_blank} are an essential part of DeFi since finance cannot exist in a vacuum without information. Oracles are bridges between a blockchain and the real world. They are used as queryable on-chain APIs to get information into smart contracts. The data could be anything from price information, weather reports, random numbers or more. Oracles can also be bi-directional and can "send" data out to the real world. They are [further described here](https://www.gemini.com/cryptopedia/crypto-oracle-blockchain-overview#section-inbound-versus-outbound-oracles){target=\_blank}.

Many top DeFi applications by [total value locked](https://coinmarketcap.com/alexandria/glossary/total-value-locked-tvl#:~:text=To%20put%20it%20simply%2C%20total,specific%20application%20by%20DeFi%20completely.){target=\_blank} use oracles in some manner. Some of the most popular use cases are collecting pricing data, event-driven decentralized execution, and random number generation.

Some popular oracle sources are [Chainlink](https://chain.link/){target=\_blank} and [Tellor](https://tellor.io/){target=\_blank}. Chainlink is described [here](https://www.gemini.com/cryptopedia/what-is-chainlink-and-how-does-it-work){target=\_blank}. Protocols like [Uniswap](https://uniswap.org/){target=\_blank} and [Maker](https://makerdao.com/en/){target=\_blank} can also act like oracles, since they can provide data from their feeds. In fact [Compound Finance uses Uniswap v2 data in conjunction with Chainlink](https://compound.finance/docs/prices){target=\_blank}.

Oracles in DeFi are used for a wealth of different reasons:

1. To get the value of underlying collateral (such as [Aave](https://aave.substack.com/p/pop-the-champagne-aave-protocol-is){target=\_blank}, [Synthetix](https://github.com/Synthetixio/synthetix/issues/293){target=\_blank}, [Compound](https://compound.finance/governance/proposals/47){target=\_blank})
2. To generate a random lottery winner (such as [PoolTogether](https://medium.com/pooltogether/improving-pooltogether-with-chainlink-vrf-dcf1a3d6ea){target=\_blank})
3. Margin Trading (such as [SushiSwap](https://medium.com/sushiswap-org/sushi-integrates-chainlink-price-feeds-to-secure-kashi-lending-and-margin-trading-markets-c1bdfc83b623){target=\_blank})
4. [Execute decentralized event-driven tasks, so that your contracts react to events](https://chain.link/solutions/keepers){target=\_blank}! The oracle can execute your contracts if a certain event happens.
5. [Verify a stablecoin's collateral](https://blog.chain.link/verify-stablecoin-collateral-with-chainlink-proof-of-reserve/?_ga=2.24406969.244707306.1629653336-101434453.1626273933){target=\_blank}
6. [Fetch Cryptocurrency prices](https://blog.chain.link/fetch-current-crypto-price-data-solidity){target=\_blank}
7. And more.

For many of these DeFi services to work and not be exploited, they need to be connected to the real world to operate correctly. As a result, oracles are used within the popular lending or swaps protocol infrastructure—for example, Bancor [uses Chainlink to mitigate impermanent loss](https://finematics.com/bancor-v2-explained/){target=\_blank}.

## Oracle Attacks in DeFi

When looking to get the price of assets, many DeFi users mistake using their own liquidity pools to price an asset or using a poor oracle source. An architecture where a protocol relies on itself to get the value of an underlying asset is a target for attack. Attackers can use [flash loans to manipulate the price in their liquidity pools](https://insights.glassnode.com/defi-attacks-flash-loans-centralized-price-oracles/){target=\_blank}, and therefore ruin any computation using the liquidity pools for pricing. Flash loans are discussed later in the DeFi Lending lesson.

Decentralized exchange data can be manipulated, so they are not good decentralized data sources and don't work as decentralized oracles. However, there are exceptions. For example, Uniswap takes the average price across a time period of around 30 minutes and uses that as the price. This is known as getting the TWAP (Time Weighted Average Price).

Using a more robust decentralized solution like [Chainlink](https://docs.chain.link/data-feeds/price-feeds){target=\_blank} will protect you from these oracle manipulation / flash loan attacks.

## A further look into Oracles

You can [create your own oracles](https://cryptozombies.io/en/lesson/19){target=\_blank}. To understand how to use oracles in general, [here is a good starter tutorial](https://www.toptal.com/ethereum/ethereum-oracle-contracts-tutorial-pt1){target=\_blank}. Check out [Chainlink's tutorial for a deeper dive (understand and use)](https://docs.chain.link/getting-started/other-tutorials){target=\_blank} and [their video walk through](https://www.youtube.com/watch?v=K4MP-HSUa74){target=\_blank}.

Creating a highly robust oracle requires much thought because oracle data inputs directly determine the consuming smart contracts' outputs. This leads to the [Oracle Problem](https://github.com/ethhub-io/ethhub/blob/master/docs/built-on-ethereum/oracles/what-are-oracles.md){target=\_blank}. Hence, oracles need to be as decentralized, secure and reliable as the blockchain networks that run them. If not, it's pointless to use a blockchain network. Single centralized nodes are subject to single points of failure if a node becomes corrupted or goes offline. Decentralization and having multiple data providers is essential since it's difficult to know if a provider is trustworthy, introducing risk. The data source could go offline or deliver bad data. You can get [a pretty comprehensive look into decentralized oracles here](https://medium.com/fabric-ventures/decentralised-oracles-a-comprehensive-overview-d3168b9a8841){target=\_blank}.

## Indexers

As mentioned, Oracles can provide data about the real world. Yet smart contracts can create data themselves, which may be important to a protocol. With all this internal chain data, how do you organize and find it? We use Indexers, which are decentralized methods to collect, organize and query information. Think of them as what Google does for information, but for on-chain data. This allows for the easy querying of data.

Ethereum is a networked decentralized database. Yet to query data, we have to look at event logs. Wouldn't it be better if we had a language we could query data with easier? We can now use [The Graph Protocol](https://thegraph.com/){target=\_blank}, a decentralized protocol for indexing and querying blockchain data that uses GraphQL as query language. Think of it as the "Google of blockchains" since indexing and sorting are what search engines do. The Graph [solves the problem of querying on-chain data as dapps grow in size](https://ethereum.org/en/developers/tutorials/the-graph-fixing-web3-data-querying/#the-decentralized-future){target=\_blank}. The Graph Protocol [is explained very well here](https://www.youtube.com/watch?v=7gC7xJ_98r8){target=\_blank}.

[GraphQL](https://graphql.org/){target=\_blank} allows for an [easier way of querying of data compared to REST APIs](https://www.rubrik.com/blog/technology/19/11/graphql-vs-rest-apis){target=\_blank}. Instead of getting the whole dataset, GraphQL allows for tailoring. GraphQL enables you to send queries to [get precisely the data you're looking for in one request instead of working with strict server-defined endpoints](https://www.apollographql.com/blog/graphql/basics/graphql-vs-rest/){target=\_blank}. Luckily, it builds upon knowledge of REST, and [the basics picked up quickly](https://egghead.io/courses/graphql-query-language){target=\_blank}.

You can [learn how to use The Graph protocol via their developer docs](https://thegraph.com/docs/){target=\_blank} and [developer academy](https://thegraph.academy/){target=\_blank}.

## Indexers and Oracles

You can use The Graph and Chainlink described [Chainlink's description](https://www.youtube.com/watch?v=HOS9g0rKP24){target=\_blank}, [EthGlobal's The Graph Protocol workshop](https://www.youtube.com/watch?v=tvo8WzAkPQc){target=\_blank} and [The Graph's blog](https://thegraph.com/blog/the-graph-chainlink-oracles){target=\_blank}.

## Additional Resources

- [77+ Smart Contract Use Cases Enabled By Chainlink](https://blog.chain.link/smart-contract-use-cases/){target=\_blank}
- [Aave Oracles](https://docs.aave.com/developers/core-contracts/aaveoracle){target=\_blank}
- [The Importance of Data Quality for DeFi Smart Contracts](https://blog.chain.link/the-importance-of-data-quality-for-defi/){target=\_blank}
- [Flash Loans and Tamper Proof Oracles](https://chain.link/education-hub/flash-loans){target=\_blank}
- [The Graph Academy](https://thegraph.academy/){target=\_blank}
- [GraphQL tutorial via EggHead.io](https://egghead.io/q/graphql){target=\_blank}
- [Article: Chainlink basic request model tutorial](https://igudar.medium.com/chainlink-local-development-truffle-ganache-kubernetes-185a8cc2fda0){target=\_blank}. Tutorial demonstrating Chainlink basic request model locally using Truffle, Ganache, Solidity and Kubernetes.
- [Article: Chainlink decentralized data model tutorial](https://igudar.medium.com/chainlink-decentralized-data-model-truffle-rinkeby-kubernetes-ec90802bd259){target=\_blank}. Deep dive tutorial on Chainlink decentralized data feed.
