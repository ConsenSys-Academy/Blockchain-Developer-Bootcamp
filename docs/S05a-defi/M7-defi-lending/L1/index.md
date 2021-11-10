# DeFi Lending Markets

## The Use of Lending Markets

Lending is a fundamental financial mechanism in finance and DeFi. Lending helps take excess capital from savers and allocates it to borrowers, putting the funds to productive use. This helps create economic growth while generating a return for savers. It's also used for hedging and mitigating risk. On the other hand, lending creates debt, which, if not properly managed, can cause instability to cascade through connected markets, leading to economic and market contractions. These issues are magnified in DeFi because networks are interdependent and open to anyone.

![debt-cycle.gif](../../../img/S05/debt-cycle.gif)

[DeFi lending markets](https://www.leewayhertz.com/how-defi-lending-works/){target=\_blank} allow users to become borrowers and lenders in a decentralized way without giving up custody of their funds. It is more efficient since it enables permissionless and programmatic access to capital without a credit check. Being on Ethereum means that any program can access these markets, providing a money lego around lending. Using a peer to contract pattern, lenders and borrowers can interact with the contract and simplify negotiating loan terms or managing counterparty risk themselves. This lowers frictions costs and while being scalable.

## Overcollateralization as a DeFi Primitive

Since DeFi protocols are open and pseudonymous, uncollateralized loans are not possible. You have to put up assets to get funds. Providing collateral ensures the counterparty cannot steal the funds or default on a loan. Due to the volatility risk of crypto assets used as collateral, over-collateralization is required. Issuing [debt via over-collateralization is a typical pattern in DeFi](https://forum.openzeppelin.com/t/introduction-to-the-overcollateralized-loan-pattern-defi-primitive-and-its-security-considerations/2141){target=\_blank}. The pattern can also [help limit the amount of leverage](https://www.steemleo.com/defi/@culgin/overcollateralization-in-defi-is-it-good-or-bad){target=\_blank}, and [control risk for a protocol](https://docs.aave.com/risk/asset-risk/adding-an-asset){target=\_blank} since assets need to be greater than liabilities.

![solvency.gif](../../../img/S05/solvency.gif)

The level of over-collateralization is represented by the loan-to-collateral ratio stated by the protocol. The loan-to-collateral ratio is the percentage you can borrow of an asset relative to the collateral deposited. Other names for the same idea include collateral factor, collateral ratio, cFactor or cRatio. Since we cannot borrow more than we deposit, the cFactor is always below 100%. Depending on the quality of the asset, the collateralization ratio is set.

![all-good-no-liquidation.gif](../../../img/S05/all-good-no-liquidation.gif)

Why collateral?

![why-collateral.gif](../../../img/S05/why-collateral.gif)

## Debt

The ability to add collateral and adjust a token's supply allows for issuing a debt token backed by collateral. This debt token can represent a utility token like a lending market position from [Compound.finance](https://medium.com/compound-finance/supplying-assets-to-the-compound-protocol-ec2cf5df5aa){target=\_blank} or Aave. For example, in Compound Finance, a DAI debt token would be cDAI, while in Aave aDAI. If DAI's collateral factor is 75%, then with $100 worth of collateral, you can borrow 75 DAI. Other DeFi 101 [lending concepts like the importance of price oracles to update price can be found here](https://forum.openzeppelin.com/t/defi-101-concepts-you-need-to-understand-before-using-a-defi-protocol/2577){target=\_blank}.

![debt-pattern](../../../img/S05/debt-pattern.gif)

## Loans and Incentives

[Why would anyone take out an over collateralized loan](https://indexcoop.substack.com/p/introduction-1-compound-finance){target=\_blank}? Why not just sell the assets? One reason is to avoid or delay paying [capital gains taxes](https://en.wikipedia.org/wiki/Capital_gains_tax){target=\_blank} when selling. If the user has excess capital, the user can earn interest on their stablecoin. Or to increase their liquidity without having to sell their assets and only having to pay the interest. This liquidity can be used as leverage to short an asset or to fund an unexpected expense.

A user can profit by leveraging a long position or shorting on an asset through lending markets. Going long means expecting the asset's price to appreciate. If the user expects ETH to go up in value, they can deposit their ETH to borrow USDC. Then use USDC to buy more ETH. The user gets exposure to more ETH minus the interest rate. Say the collateral factor is 50% on a deposit of $1000 worth of ETH. The borrower receives 500 USDC and then can buy more ETH. So they can leverage themselves to $1,500 worth of ETH. To turn a profit, the appreciation of ETH should exceed the interest and gas fees required to pay back the loan.

![going-long.gif](../../../img/S05/going-long.gif)

Going short means expecting the asset will lose value in price. If the user expects ETH to depreciate, they can deposit USDC to borrow ETH. Then sell the ETH and repurchase it later at a lower price, making a profit in the difference. Say ETH is at $1000 when the user sells it. Later, they buy the asset back at $300. They get to pocket $700 minus the interest payment and gas fees.

![going-short.gif](../../../img/S05/going-short.gif)

## Liquidation and Incentives

Liquidation involves a user's position being closed to pay the debt incurred. This happens if the collateral's value drops below the acceptable collateral ratio. Lending protocols often use an Oracle service like [ChainLink](http://chainlink){target=\_blank} and the price feed of a major exchange like Uniswap to provide real-time data about a collateral's value.

![liqudation.png](../../../img/S05/liqudation.gif)

Since smart contracts cannot act without being called, liquidation occurs by offering incentives to an external entity called a "keeper". The keeper can liquidate the position and keep a percentage fee. Then, the collateral is auctioned off or via a decentralized exchange at market price.

<!-- 🖼 Halting problem -> contracts need to be called -> incentive to call -> keeper to liquidate -->

In some protocols, everything is auctioned off. In others, the remaining collateral is left in the original contract. An example can be if the collateralization ratio is 200% and the user only placed the bare minimum. If the asset drops 1%, the protocol will liquidate 2% of the collateral. Since liquidation is costly, some protocols allow users to add additional collateral if needed, similar to a [margin call](https://www.investopedia.com/terms/m/margincall.asp){target=\_blank}. It is wise to add a margin of safety in addition to the collateral ratio.

![volatility-margin-of-safety.gif](../../../img/S05/volatility-margin-of-safety.gif)

Applications: Compound Finance and Aave

An application of lending markets are money markets. Within DeFi open-source algorithmic money market protocols allow anyone to borrow or lend cryptocurrency assets by only providing collateral. These lending markets connect lenders who wish to earn [interest](https://www.investopedia.com/terms/i/interest.asp){target=\_blank} and borrowers who want to borrow for various reasons and pay interest. Users can provide assets with d liquidity like ETH, WITH, DAI, USDT, USDC, LINK, etc.

The two leading platforms are [Compound.finance](https://compound.finance/documents/Compound.Whitepaper.pdf){target=\_blank} and [Aave](https://github.com/aave/aave-protocol/blob/master/docs/Aave_Protocol_Whitepaper_v1_0.pdf){target=\_blank} ([ghost in Finnish](https://aave.com/branding/){target=\_blank}). Explained in the links, [Compound Finance](https://www.gemini.com/cryptopedia/what-is-compound-and-how-does-it-work){target=\_blank} and [Aave](https://docs.aave.com/developers/v/1.0/developing-on-aave/the-protocol/lendingpool){target=\_blank} work by using [lending pools](https://finematics.com/lending-and-borrowing-in-defi-explained/){target=\_blank}. A lending pool locks up capital and generates an algorithmically determined interest rate based on supply and demand. You can learn how to use [Aave](https://www.youtube.com/watch?v=IDzdrM4xjYw){target=\_blank} and Compound.

## Interest and Lending

Lending requires borrowers and lenders. Borrowers pay interest while lenders earn interest. Whether you borrow or lend, you must lock up capital into a lending pool inside a contract. In return, you earn a debt token, in Compound's case a cToken, derived from the asset in question. DAI, you get cDAI, BAT renders cBAT and so on. This token accrues interest over time and can be traded or used as collateral in other protocols. For the lender to unlock their collateral, they must pay the interest accrued plus the collateral. For both Aave and Compound, there is no time period to close the loan.

Lending can occur with variable rate interest based on market demand or fixed interest rates. Variable interest rates adjust due to the demand and supply for the asset in question. The key to note is that the borrow interest rate is always higher than the supply rate.

![interest-rates.gif](../../../img/S05/interest-rates.gif)

Lending protocols operate in real-time. Rates are adjusted, and interest is accrued every new Ethereum block. Interest is typically [accrued to the debt token](https://medium.com/compound-finance/faq-1a2636713b69){target=\_blank} or accounts tied to the lending pool. Aave lets users redirect their stream of interest to other contracts. This allows for interesting applications where pools of money can be programmatically deployed to earn interest. One can seperate the marketing logic form the interest earning logic.

An example of this can be PoolTogether which is a no loss lottery where the winner wins the interest accumulated and doesn't sacrifice the principal. A similar project could focus on the marketing of new application of lending pools, like no loss poker, and leverage Aave's money lego to deal with the interest.

Aave offers a [stable interest rate](https://docs.aave.com/faq/borrowing#:~:text=The%20variable%20rate%20is%20the,rate%20depending%20on%20market%20conditions.){target=\_blank}, which means it's fixed for a short term and can change depending on borrowing and lending dynamics of the pool. [Other platforms](https://messari.io/article/fixed-income-protocols-the-next-wave-of-defi-innovation){target=\_blank} offer fixed interest rates, like [Notional](https://notional.finance/){target=\_blank}, [88mph](https://88mph.app/){target=\_blank} and [Barnbridge](https://barnbridge.com/){target=\_blank}.

Typically, the longer the loan, the higher the risk, the higher the interest rate. On Ethereum, we measure time in blocks. What if we went in reverse? If a loan and a position could be executed in the same block, what happens? We get flash loans!

![flash-loan-interest-risk.gif](../../../img/S05/flash-loan-interest-risk.gif)

## Flash Loans as a DeFi Primitive

DeFi allows the creation of something called [Flash Loans](https://www.gemini.com/cryptopedia/aave-flashloans#section-aave-flash-loans){target=\_blank}. Introduced by Aave, flash loans are the first uncollateralized loans that can be accessed in a permissionless way. This means that anyone anywhere can access large sums of capital. They are [explained here](https://finematics.com/flash-loans-explained/){target=\_blank}.

Flash Loans only have one condition: Payback the loan within 1 Ethereum block. Since all protocols share the same database on Ethereum, flash loans can interact with various protocols in one block to find opportunities. The loan only goes through if the transaction results in the loan being repaid. If not, the entire transaction reverts, like it was never sent!

A cool application of [Flash Loans](https://medium.com/@bneiluj/flash-boys-arbitrage-dao-c0b96d094f93#:~:text=About%20ArbitrageDAO%20%7C%20Flash%20Boys&text=It%20uses%20a%20combination%20of,in%20the%20decentralized%20finance%20ecosystem.){target=\_blank} is the ability to do Flash Swaps. Learn how to create [Flash Swaps with Infura here.](https://blog.infura.io/build-a-flash-loan-arbitrage-bot-on-infura-part-i/){target=\_blank} This can be used to hedge against liquidation risk by swapping a volatile asset into a stable asset!

## Risks

With DeFi Lending Markets, there is zero counterparty risk. However, smart contract risk always exists. Duration risk comes in borrowers being hit with spiking variable borrowing APY rates if they are not paying attention. This can cause a user to get liquidated by having to repay more than expected. When hedging, there is the risk of the trade going the other way.
