# Oracles

In our discussion blockchain primitives, we discussed how public blockchain networks coordinate these powerful tools to create a network state that can be established and maintained by network participants.

However, that network state only holds true within the boundaries of the network itself. We can only guarantee the state transitions of the network participants running our blockchain client software. What about data that exists outside this network, specifically what about "real world" data, such as weather reports, incident details or stock prices? 

Additionally, what if we'd like to interact with external computation in the outside world? A machine learning algorithm, a random number generator, or an event-driven task automation would all be examples of external computation that would be essential to building feature rich smart contracts. 

Such data and external computation exist but they are beyond the _trust boundary_ established by our blockchain protocols.

One way blockchain developers have tried to bridge the gap is through what are called **off-chain [oracles.](https://en.wikipedia.org/wiki/Blockchain_oracle)** Off-chain oracles are agents that find and verify real-world information and submit them to the blockchain to be used by smart contracts. They can trigger smart contract executions when the data is obtained or predefined conditions are meet (e.g. time, weather, tracking, payments). Off-chain oracles are provided by organizations like [Provable Things](https://provable.xyz/){target=_blank}, [Chainlink Labs,](https://chain.link/){target=_blank} and more.

Please note that DeFi has led to on-chain oracles, particularly dealing with token prices, which we will discuss more in the section on DeFi. Such examples of on-chain oracles are [Chainlink's Data Feeds](https://docs.chain.link/docs/get-the-latest-price/){target=_blank}, Uniswap's [Observations](https://docs.uniswap.org/protocol/concepts/V3-overview/oracle){target=_blank}, and MakerDAO's [Feeds](https://developer.makerdao.com/feeds/){target=_blank}.

A smart contract using oracles in some facet is often referred to as a [Hybrid Smart Contract](https://blog.chain.link/hybrid-smart-contracts-explained/){target=_blank}.

## Trust

It's extremely important to understand oracles like the ones we're discussing here can require trust. Understanding where the data is coming from is essential to running a decentralized smart contract. When using oracles, it's important to build in smart contract mechanisms that can anticipate errors or possible corruption, as oracles can succumb to many attack vectors.

Having a single oracle or a single data source delivering your data or executing your computation creates a single source of failure for your smart contract, and means your decentralized application isn't actually decentralized. You'll want to make sure the oracle network you're working with is executing in a context as decentralized as possible. For example, if you want pricing data, you get the pricing data from many exchanges, and many independent blockchain oracles deliver this data. 

It's important to know, that just setting up an oracle service yourself can mean your application is centralized, and possibly doesn't have the highest quality data or execution. So we want to avoid setting these up ourselves, but also do our due diligence to make sure the system we are working with is decentralized. 

Services such as Chainlink have built more decentralized networks to hedge against the centralization of trust, you can read more about how Chainlink does that [here](https://docs.chain.link/docs/architecture-decentralized-model/){target=_blank} and see an overview of decentralized oracles [here.](https://medium.com/fabric-ventures/decentralised-oracles-a-comprehensive-overview-d3168b9a8841){target=_blank}

## Basic Oracle Mechanism

At its most basic, a smart contract using an oracle needs to implement a method to:

1.  Make the request to the oracle, and
2.  Receive the oracle's response from a callback method

This is often known as the [request and receive](https://docs.chain.link/docs/architecture-request-model/){target=_blank} model of oracles. Unless you've setup the service yourself, external calls to oracles typically require a fee attached to provide the data to your contract.

There are multiple ways to achieve this; let's look at a simplified version of this [example](https://github.com/provable-things/ethereum-examples/blob/c0431a147f24519a135d07f9d5c17db73498e0e7/solidity/DieselPrice.sol){target=_blank} using [Provable](https://docs.provable.xyz){target=_blank} below:

<pre>import "github.com/provable-things/ethereum-api/provableAPI.sol";

contract DieselPrice is usingProvable {
    uint dieselPriceUSD;

    constructor() public {
        provable_query("URL", "xml(https://www.fueleconomy.gov/ws/rest/fuelprices).fuelPrices.diesel");
    }

    function __callback (bytes32 myid, string result) public {
        require(msg.sender == provable_cbAddress());
        dieselPriceUSD = parseInt(result);
    }
}
      </pre>

In this code, we're calling the Provable API for the price of diesel when we create the contract. The first query is free, but we'll have to provide ETH to pay for our requests moving forward. The call triggers an event, which lets the Provable contract pull from its off-chain data feed and provide our contract the result. The contract stores that value in `dieselPriceUSD`.

The overall model is for your contract to emit an event, either to another contract or simply in the block its created. The oracle service will detect that event, pull the desired data, and respond back to your contract. The oracle services require you to have a standard method, like `__callback`, that its transaction can target when responding to your oracle query.

## Decentralized Oracle Mechanism

In the above example, we looked at pulling data from a single source and provider. Stringing requests like this together can make us have a more decentralized application, but we would still be routing it through the same organization.

Let's look at another example of pulling data in a decentralized context, for example, from a [Chainlink data feed.](https://docs.chain.link/docs/using-chainlink-reference-contracts/){target=_blank}

You can see the most up to date version of this code in the [Chainlink documentation.](https://docs.chain.link/docs/get-the-latest-price/){target=_blank}

<pre>

pragma solidity ^0.6.7;

import "@chainlink/contracts/src/v0.6/interfaces/AggregatorV3Interface.sol";

contract PriceConsumerV3 {

    AggregatorV3Interface internal priceFeed;

    /**
     * Network: Kovan
     * Aggregator: ETH/USD
     * Address: 0x9326BFA02ADD2366b30bacB125260Af641031331
     */
    constructor() public {
        priceFeed = AggregatorV3Interface(0x9326BFA02ADD2366b30bacB125260Af641031331);
    }

    /**
     * Returns the latest price
     */
    function getThePrice() public view returns (int) {
        (
            uint80 roundID, 
            int price,
            uint startedAt,
            uint timeStamp,
            uint80 answeredInRound
        ) = priceFeed.latestRoundData();
        return price;
    }
}

</pre>

In this example, we are pulling the price of Ethereum in terms of the United States Dollar into our smart contract. We do this by querying another contract that has already followed the basic request model among many different oracles and data providers. It's important that the network is using different data providers and oracles so that there is never a single authority point. 

You can see a visualization of this contract and the different nodes gathering the data for them at [data.chain.link.](https://data.chain.link/ethereum/mainnet/crypto-usd/eth-usd){target=_blank}

## Summary 

The oracle ecosystem is growing as fast as blockchain, and we'll touch on it more later in the course. For now, it's important to see how oracles allow us to cross the "trust boundary" of blockchains, what trust assumptions that requires, and the basic design pattern for incorporating this data stream.
## Additional Material

*[Wiki: Oracles (Ethereum.org)](https://ethereum.org/en/developers/docs/oracles/){target=_blank} A great overview of oracles on Ethereum with demo code for Chainlink
*[Wikipedia: Blockchain Oracle](https://en.wikipedia.org/wiki/Blockchain_oracle){target=_blank}
*[Docs: Chainlink](https://docs.chain.link/){target=_blank} A really well-curated series of docs outline how to get started with Chainlink and the different services and networks available.
*[Tutorial: Implementing a Blockchain Oracle on Ethereum](https://medium.com/@pedrodc/implementing-a-blockchain-oracle-on-ethereum-cedc7e26b49e){target=_blank}
* [Code: Provable Things Ethereum Examples](https://github.com/provable-things/ethereum-examples/tree/master/solidity){target=_blank} A collection of examples from Provable Things, a bit dated but can still provide a source of reference.
* [Academic Article: A Study of Blockchain Oracles](https://arxiv.org/pdf/2004.07140.pdf){target=_blank} A technical examination of blockchain oracles referenced in the blockchain oracles Wikipedia page.
*[Article: So You Want to Use a Price Oracle](https://samczsun.com/so-you-want-to-use-a-price-oracle/){target=_blank} Interesting article (albeit about on-chain oracles) discussing attack vectors.
