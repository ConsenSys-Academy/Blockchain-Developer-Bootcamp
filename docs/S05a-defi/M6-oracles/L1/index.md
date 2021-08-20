# Oracles in DeFi

Oracles are an essential piece of DeFi. A majority of the top DeFi applications by total locked value use oracles in some way, with some of the most popular use case being around collecting pricing data, event-driven decentralized execution, and random number generation. 

In a previous section, we explored some of the oracles that are powering the top DeFi protocols today, such as [Chainlink](https://chain.link/){target=\_blank}, [Uniswap](https://uniswap.org/){target=\_blank}, and [Maker](https://makerdao.com/en/){target=\_blank}. 

Oracles in DeFi are used for a wealth of different reasons:

1. To get the value of underlying collateral (such as [Aave](https://aave.com/){target=\_blank}, [Synthetix](https://synthetix.io/){target=\_blank}, [Compound](https://compound.finance/){target=\_blank})
2. To generate a random lottery winner (such as [PoolTogether](https://pooltogether.com/){target=\_blank})
3. Margin Trading (such as [SushiSwap](https://sushi.com/){target=\_blank})
4. Execute decentralized event-driven tasks

And more.

As we go into lending, swaps, and more of the infrastructure behind DeFi, we'll start to see that in order for a lot of these services to work, they need to be connected to the real world to operator correctly. 

## Oracle Attacks in DeFi

A common issue in DeFi that a lot of users take when looking to get the price of assets is using their own liquidity pools to price an asset, or use a poor oracle source. An architecture where a protocol relies on itself to get the value of an underlying asset is a surefire way to be a target for attack. Attackers can use a device called a flash loan to manipulate the price in their liquidity pools, and therefor ruin any computation that is using the liquidity pools for pricing. 

In this regard, decentralized exchanges are exactly that, decentralized exchanges. They are not good sources of decentralized data and don't work as a decentralized oracles. There are exceptions, for example, Uniswap takes the average price across a time period of around 30 minutes and uses that as the price. This is known as getting the TWAP (Time Weighted Average Price). 

Using a more robust decentralized solution like [Chainlink](https://docs.chain.link/docs/get-the-latest-price/){target=\_blank} will protect you from these oracle manipulation / flash loan attacks.

## Additional Resources

[77+ Smart Contract Use Cases Enabled By Chainlink](https://blog.chain.link/44-ways-to-enhance-your-smart-contract-with-chainlink/){target=\_blank}
[Aave Oracles](https://docs.aave.com/developers/the-core-protocol/price-oracle){target=\_blank}
[The Importance of Data Quality for DeFi Smart Contracts](https://blog.chain.link/the-importance-of-data-quality-for-defi/){target=\_blank}
[Flash Loans and Tamper Proof Oracles](https://blog.chain.link/flash-loans-and-the-importance-of-tamper-proof-oracles/){target=\_blank}
