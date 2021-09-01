# Automated Market Makers - AMM

An [automated market maker (AMM)](https://academy.binance.com/en/articles/what-is-an-automated-market-maker-amm) is a smart contract that holds assets and is always willing to quote you a price between two assets. You can trade against the AMM's capital in the smart contract instead of between peers. It uses the trades to update the size of the assets and update their price accordingly. The AMM can always guarantee liquidity by raising the price for an asset according to market demand.

There are [various ones](https://cipher.substack.com/p/an-introduction-to-automated-market){target=\_blank}, however we will focus on the most important features popularized by UniSwap. [Haseeb Qureshi explains UniSwap](https://medium.com/dragonfly-research/what-explains-the-rise-of-amms-7d008af1c399){target=\_blank} well here. We will cover another type of DEX protocol in a later section.

This section will give an overview of two key concepts that make AMMs possible.

## Liquidity Pools

Automated Market Makers rely on [liquidity pools](https://finematics.com/liquidity-pools-explained/){target=\_blank} to source capital. Liquidity pools are collections of tokens locked into a smart contract. This allows for decentralized capital formation. They are used to facilitate trading by providing liquidity, defined as the ability to convert an asset into cash or its equivalents without greatly affecting its market price. This is important because an asset's value is determined by what others are willing to pay for it and how easily it can be bought or sold.

The main ideas behind liquidity pools are:

- They are used to source capital which is used to provide liquidity.
- Liquidity is the ability to convert an asset into cash without affecting its price.
- They are useful because [order book models](https://www.investopedia.com/terms/o/order-book.asp){target=\_blank} are not feasible on-chain completely since market makers cannot update prices all the time due to gas fees and Ethereum's throughput being too slow.
- Liquidity pools source capital from anyone and are used to allow anyone to trade against the smart contract. Liquidity providers earn a fee for doing so in the proportion of capital they provide to the pool.
- To become a liquidity provider, users must deposit equal amounts of token based on their price into a pool. If they don't, they risk being arbitraged by traders who find a good deal.
  -AMMs like UniSwap hold liquidity pools in token pairs. An example can be the ETH - DAI or CRV - COMP (Curve to Compound Finance).

**The downside**:

- Because trades happen on-chain, bots can [front-run transactions and attempt other sorts of attacks](https://coinmarketcap.com/alexandria/glossary/front-running){target=\_blank}. This results in a user paying more than they intended.
- [Front running](https://www.youtube.com/watch?v=Wd0at2Pu6xY){target=\_blank} occurs when bots read Ethereum's current set of unprocessed pending transactions called [the mempool](https://www.blocknative.com/blog/mempool-intro){target=\_blank} and find an opportunity to outbid a transaction to be processed by the network miner (or validator after ETH 2.0). The bots get ahead of the line, which results in a better price for them at the expense of the other traders.
  -This stems from the [Miner Extractable Value](https://research.paradigm.xyz/MEV){target=\_blank}, where a miner can dictate when, how and where a transaction will go into an Etheruem block. When a transaction large enough to create slippage is sent to the network, bots will notice and set off a bidding war to capture the stop and front-run.

## Bonding Curves

The other key to Automated Market Makers is the bonding curve. A [bonding curve](https://yos.io/2018/11/10/bonding-curves/){target=\_blank} is a mathematical formula used to describe the relationship between the price and the supply of an asset. This can be thought of as a deterministic pricing formula. This formula is called the [**Constant Product Formula**](https://medium.com/bollinger-investment-group/constant-function-market-makers-defis-zero-to-one-innovation-968f77022159){target=\_blank} in UniSwap. This curve can be represented in a smart contract that can buy or sell the underlying token. Bonding Curves emerge out of the ability to escrow funds in a smart contract.

The main ideas behind the Constant Product Formula are:
-To always ensure liquidity for any asset by modelling the demand curve in the smart contract.

- Users trade against the smart contract, not between each other.
  k always has to stay the same number, no matter what x or y does. The price quoted is directly dependent on the size of the order.
- The trade-off for assured liquidity is slippage, also known as getting less for more.

x \* y = k

x = supply of asset 1
y = supply of asset 2
k = Fixed Size of Pool

![](../../../img/S05/uniswap-market-graph.png)

The downside:

- Note that the further one moves along the curve, the less they get.
- In UniSwap, the slippage starts to seriously affect orders; around 2% of the liquidity of a token is traded against. A good description of this can be found via [this article](https://medium.com/scalar-capital/uniswap-a-unique-exchange-f4ef44f807bf){target=\_blank} and most recently [here](https://research.paradigm.xyz/amm-price-impact){target=\_blank}.

Different AMMs have variations of this deterministic pricing formula depending on their need. [Curve](https://curve.readthedocs.io/exchange-overview.html){target=\_blank} implements a special formula to allow stablecoins trades for assets that are a stable representation of each other, which results in a narrow trading band. An example of this is trading between ETH and sETH (synthetic ETH) or USDC and DAI, which should both be pegged close to the US Dollar.

## Synching Prices Across Markets

With Automated Market Makers similar to UniSwap v2, prices are synched with outside markets via arbitrageurs who spot price differences between exchanges. These exchanges can be other DEXes or centralized exchanges. Arbitrageurs capture the profit, which is the difference in price between the two markets.

A consequence of this is [impermanent loss](https://coinmarketcap.com/alexandria/glossary/impermanent-loss){target=\_blank} for liquidity providers, the difference between holding an asset and providing liquidity. This is similar to an opportunity cost which if realized turns into a real loss. Impermanent loss is also described in [this animated video](https://finematics.com/impermanent-loss-explained/){target=\_blank} and article and [here](https://academy.binance.com/en/articles/impermanent-loss-explained){target=\_blank}.

[Uniswap V3](https://finematics.com/uniswap-v3-explained/){target=\_blank} has other features like Range Orders and Limit Orders which you can explore. Some AMMs can hold more than two assets, namely Balancer, but these are more sophisticated and rely on [Bonding Surfaces](https://medium.com/balancer-protocol/bonding-surfaces-balancer-protocol-ff6d3d05d577){target=\_blank}.

## Additional Resources

[DeFi and the Future of Finance](https://poseidon01.ssrn.com/delivery.php?ID=468065099084001018003001097015123074002033009058089053073089097071090006069068127090056119012045118056006023019023064027115112050004033058059085029023094127080025065057006114025116096023021080002103109117106113005025070080109097094005091097004025&EXT=pdf&INDEX=TRUE){target=_blank} (section 4.7.2)
[DeFi and the Future of Finance](https://poseidon01.ssrn.com/delivery.php?ID=468065099084001018003001097015123074002033009058089053073089097071090006069068127090056119012045118056006023019023064027115112050004033058059085029023094127080025065057006114025116096023021080002103109117106113005025070080109097094005091097004025&EXT=pdf&INDEX=TRUE){target=_blank} (section 6.2)
[Graphical Guide for Understanding Uniswap via EthHub](https://docs.ethhub.io/guides/graphical-guide-for-understanding-uniswap/){target=\_blank}
