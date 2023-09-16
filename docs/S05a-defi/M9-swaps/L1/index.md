# Introduction to MetaMask Swaps

The previous section covered decentralized exchanges and briefly touched upon aggregators, which finds the best price between exchanges. We can go a step further and have aggregators of aggregators. The most popular aggregator of aggregators is MetaMask Swaps.

![metamask-swaps-aggregator](/docs/img/S05/metamask-swaps-aggregator.png)

## MetaMask Swaps addresses five issues

### 1 | Barrier to entry is high

Before interacting with different DeFi protocols, users must first familiarize themselves with those platforms and understand the pros and cons of each.

### 2 | Rates vary between protocols

Not all liquidity sources (DEX, DEX aggregators, and PMMs) are created equal. The rate that each protocol provides may depend on liquidity depth, pricing mechanism, and type of tokens.

### 3 | Gas usage differs between sources

The route and complexity of each Swap may differ, depending on the liquidity source. Some sources will require less gas, depending on the route.

### 4 | Liquidity is fragmented

Decentralization leads to liquidity fragmentation.

For some trades, splitting a Swap between multiple sources can result in the most favorable trade.

### 5 | Token approvals are messy and expensive

When Swapping ERC20 tokens, users must first approve individual tokens on each liquidity source.

![metamask-flow-cycle](/docs/img/S05/metamask-flow-cycle.png)

## MetaMask Swaps solves these issues with three things

### 1 | Best rates across DeFi

By requesting prices from all available DEXs, DEX aggregators, and individual market makers, we can guarantee that MetaMask users have access to the deepest liquidity, the largest selection of tokens, and the most competitive prices.

### 2 | Seamless and standardized UX

We’ve abstracted all the complexities, allowing MetaMask users to Swap > 1,000 unique tokens in three clicks.

### 3 | Approve once, Swap anywhere

No need to approve every token on multiple DEXs and aggregators for each trade. With Swaps, users only need to approve each token once, reducing gas costs and shortening the path to executing their trade.

![metamask-swaps-order-flow](/docs/img/S05/metamask-swaps-order-flow.png)

## Additional Material
- [Users Guide to Swaps (Metamask)](https://metamask.zendesk.com/hc/en-us/articles/4405093054363)
