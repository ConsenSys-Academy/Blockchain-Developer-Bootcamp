# What are Stablecoins

A critical issue in cryptocurrencies is extreme volatility, especially when compared to fiat currencies. It’s hard to enter into any profitable financial agreement when prices can fluctuate wildly. Stablecoins were created to fix this issue.

Stablecoins are cryptocurrencies built using smart contracts on programmatic blockchains, which significantly reduces or eliminates price volatility by aiming to peg to a fiat currency like the US dollar. This gives users a tool for managing risk and allowing them to engage with DeFi protocols reliably. Stablecoins are one of the cornerstones of the DeFi industry, as a user cannot reliably enter or exit a protocol without a stable currency. They also provide access to stable currencies to [unbanked and underbanked people around the world](https://www.worldbank.org/en/news/press-release/2018/04/19/financial-inclusion-on-the-rise-but-gaps-remain-global-findex-database-shows){target=\_blank}, helping people to save, pay, invest and spend in more reliable ways. In addition, Stablecoins allows people to choose their economic policy based on their interests and objectives.

There are five types of stablecoins, each collateralized by different assets and its own complexity/centralization profile.

The types are ranked from most centralized/less complex to less centralized/more complex.

1. Fiat backed
2. Commodity backed
3. Crypto backed
4. Algorithmic
5. Central Bank Digital Currencies\*

A good mental model for a Stablecoin is the paper money you have in your pocket. Think of it as a programmable IOU that everyone in your community would accept as payment.

There are three things to consider when looking at stablecoins:

- Type of collateral
- Collateralization ratio
- Degree of centralization

A general mental model could be that the simpler the stablecoin is to understand, the more centralized it is. The exception would be Central Bank Digital Currencies which could be complex, opaque, and highly centralized due to political issues.

## Fiat Backed Stablecoins

These are backed by US dollars or a government currency in a bank account. These stablecoins are collateralized by US Dollars in bank accounts and are audited periodically to maintain their assurances. Examples include [Tether’s USDT](https://tether.to/){target=\_blank} and [Circle’s USDC](https://www.circle.com/en/usdc){target=\_blank}.

Fiat backed stablecoins are collateralized at 100% with dollars. In the case of Tether, it is collateralized with dollar and dollar equivalents (financial instruments that can be quickly turned to cash without losing much value). These are the simplest to understand since, from a technical perspective, the issuance is very simple. There is one dollar in a bank account for every token on the network. [USDT](https://dune.xyz/phabc/usdt---banned-addresses){target=\_blank} and [USDC](https://www.theblockcrypto.com/linked/102761/centre-consortium-blacklisted-seven-usdc-addresses-wednesday){target=\_blank} are by far the most popular stablecoins for their ease of use.

However, with this simplicity comes the centralization and the possibility of censorship. Both USDT and USDC can add users to blocklists and freeze their assets.

## Commodity backed Stablecoins

Backed by gold or another asset. An example includes [Paxos Gold](https://www.paxos.com/paxgold/){target=\_blank}. Every PAX Gold token is backed by an ounce of allocated gold. This type functions similar to fiat-backed stablecoins, including the ability for the issuer to place users on a blocklist.

Furthermore, there is the additional complexity of the volatility of the price of gold which is higher than the fiat currencies.

## Crypto Collateralized

Backed by crypto assets like ETH or other tokens as collateral. Due to the cryptocurrency’s volatility, these assets need over 150% collateral (250% recommended) to deal with volatility. The prominent example is [MakerDAO’s DAI](https://thedefiant.io/what-is-makerdao-and-how-does-dai-work/){target=\_blank}. Best known for introducing the [Collateralized Debt Position (CDP)](https://coinmarketcap.com/alexandria/glossary/collateralized-debt-position-cdp){target=\_blank}.

There are many advantages to crypto collateralized stablecoins. Because the asset lives on-chain, the [stablecoin can be audited by anyone at any time without permission](https://daistats.com/#/overview){target=\_blank}. Furthermore, DAI is an actual [money lego](https://future.a16z.com/how-composability-unlocks-crypto-and-everything-else/){target=\_blank} and can be built upon and easily integrated into any project. It can also generate interest. Along with transparency into its financial status, MakerDAO, the entity behind DAI, has a transparent governance system that allows the community members who hold MAKER tokens to vote on the management of the stablecoin. It’s also a [fully decentralized DAO](https://blog.makerdao.com/makerdao-has-come-full-circle/){target=\_blank}, short for [decentralized autonomous organization](https://ethereum.org/en/dao/){target=\_blank}.

## Algorithmic

### Rebase Tokens

Self-balancing through incentives and algorithms and non-collateralized. These use smart contract logic to expand and contract the supply of tokens to maintain their peg. Examples include [AmpleForth’s AMPL](https://www.ampleforth.org/){target=\_blank} & [Base Protocol's BASE](https://www.baseprotocol.org/){target=\_blank}.

One can get a [A Visual Explanation of Algorithmic Stablecoins by Haseeb Qureshi](https://medium.com/dragonfly-research/a-visual-explanation-of-algorithmic-stablecoins-9a0c1f0f51a0){target=\_blank}.

### Fractional Stablecoins

Partially backed by collateral at 100% or less and partially stabilized algorithmically. The purpose is to improve capital efficiency. Examples include [FRAX](https://frax.finance/){target=\_blank} and [Iron Finance’s IRON](https://frax.finance/){target=\_blank}. You can get a feeling for these via [A Visual Explanation of FRAX by Haseeb Qureshi](https://medium.com/dragonfly-research/a-visual-explanation-of-frax-bcce72c1730f){target=\_blank}.

Fractional stablecoins are a work in progress and have suffered from [“run on the bank”](https://cointelegraph.com/news/iron-finance-bank-run-stings-investors-a-lesson-for-all-stablecoins){target=\_blank}, shakes the market’s confidence. This causes a self-fulfilling prophecy of capital withdrawals at the same time. Like a game of musical chairs, someone will be left standing.

### Seigniorage

[Seigniorage](https://www.investopedia.com/terms/s/seigniorage.asp){target=\_blank} typically involves at least two tokens. One representing the stable token. While the other attempts to stabilize the token through actively adjusting the stables supply. The volatility, either through profit or loss, is passed on to the other token(s). A few examples of Seigniorage Stablecoins are Empty Set Dollar, Basis, and Terra. Out of these, Terra is the only one who has maintained its peg.

A typical, and often short-lived, mechanism employed is in the use of [Seigniorage Shares](https://smithandcrown.com/research/the-cryptoeconomics-of-seigniorage-shares-stablecoins-basis-and-carbon/){target=\_blank}. Often recognizable by the Stable Token and Bond Token.

## Central Bank Digital Currencies - CBDCs

These are government-issued fiat currencies that utilize distributed ledger technology like Ethereum. As of 2021, [China has begun to pilots for its Digital Yuan](https://www.cnbc.com/2021/03/05/chinas-digital-yuan-what-is-it-and-how-does-it-work.html){target=\_blank} and [five countries in the Caribbean have already launched them](https://www.crowdfundinsider.com/2021/08/178917-cbdcs-china-seems-intent-on-creating-digital-yuan-for-local-use-and-potential-global-transactions-report-reveals/){target=\_blank}. There are also currently CBDC pilots in 14 countries including Sweden, South Korea and China. You can see up to date information on CBDC’s via the [Atlantic Council’s CBDC tracker](https://www.atlanticcouncil.org/cbdctracker/){target=\_blank}.

There are some interesting DeFi primitives that make this technology possible. The first is the [ERC-20 standard](https://docs.openzeppelin.com/contracts/2.x/erc20){target=\_blank}, which standardizes fungible tokens. Next, the possibility of [escrow contracts](https://docs.openzeppelin.com/contracts/2.x/api/payment#Escrow){target=\_blank} allows for collateral to be deposited into a protocol, giving the protocol custody over those funds. Next, the ability to alter the supply is necessary. To expand the supply the protocol needs to [mint](https://docs.openzeppelin.com/contracts/2.x/api/token/erc20#ERC20Mintable){target=\_blank} tokens. To contract the supply, it needs to [burn](https://docs.openzeppelin.com/contracts/2.x/api/token/erc20#ERC20Burnable){target=\_blank} tokens.

An interesting DeFi primitive that has evolved from algorithmic stablecoins is the concept of [rebasing](https://www.ampleforth.org/technology/){target=\_blank}. The peg adjusts by expanding or contracting the supply of tokens depending on the price. For example, if the price goes up or down 10%, the supply will expand or contract 10%. Rebasing makes possible an [elastic supply of tokens](https://academy.binance.com/en/articles/elastic-supply-tokens-explained){target=\_blank} that change based on any condition, in this case, it being the market price.
