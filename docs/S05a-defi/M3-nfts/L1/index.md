# NFTs: More than Solidity Code

## What are NFTs

An engineer walks into a meetup. How do we explain the significance of NFTs? Why are NFTs useful? Let's explain!

Non-fungible tokens or NFTs are more than just code. NFTs are smart contract representations of unique and non-fungible items. [Fungibility](https://www.investopedia.com/terms/f/fungibility.asp){target=_blank} is characterized by goods being uniform in their properties, interchangeable, and indistinguishable from each other. Examples of fungibility include US Dollars or Coca-Cola bottles.

NFTs can represent ownership of digital scarce goods like [art](https://nypost.com/2021/08/23/visa-buys-digital-artwork-token-cryptopunk-for-150k/){target=_blank}, [collectables](https://dappradar.com/blog/how-to-value-sorare-nfts){target=_blank} or any unique non-fungible item. They can also represent [unique trading positions on a bonding curve like Uniswap v3](https://www.theblockbeats.com/en/news/24141){target=_blank}, [intellectual property](https://medium.com/molecule-blog/ip-nfts-for-researchers-a-new-biomedical-funding-paradigm-91312d8d92e6){target=_blank}, [licenses](https://blog.oceanprotocol.com/nfts-ip-3-combining-erc721-erc20-b69ea659115e){target=_blank}, [insurance](https://docs.yearn.finance/resources/defi-glossary#yinsure){target=_blank}, options, bonds, real estate, [game items](https://www.lexology.com/library/detail.aspx?g=73db4ff0-c146-4f7c-9ccf-1dd621aeef17){target=_blank}, deeds, [domain names](https://unstoppabledomains.com/blog/what-are-blockchain-domain-nfts-a-full-introduction){target=_blank} and more. Even when considering two identical collectables, other factors can make them unique, like their [provenance](https://www.nationalgallery.org.uk/paintings/glossary/provenance#:~:text=Provenance%20refers%20to%20the%20history,themselves%20and%20auction%20sale%20catalogues.){target=_blank}, history, year of production and more.

NFTs are created with the [ERC-721](https://ethereum.org/en/developers/docs/standards/tokens/erc-721/){target=_blank} standard. Popularized by CryptoKitties in 2017, they share these properties:

- Unique, with their particular qualities usually stored in the metadata
- Indivisible since they cannot be split up.
- Provably scarce. Usually, one or a limited number of NFTS and can be verified on-chain
- Provable ownership, since you check on-chain
- Fraud proof. They can't be faked. We will cover some issues around this later.
- Easily transferable

[ERC-1155](https://enjin.io/about/erc-1155){target=_blank} further builds upon ERC-721 and allows for mixed-use of fungible and non-fungible tokens, [among other features](https://enjin.io/about/erc-1155){target=_blank}. You can [explore the difference between 721 and 1155 here](https://www.numbrs.com/tech/2021/04/28/ethereums-standards-for-non-fungible-tokens-erc-721-and-erc-1155/){target=_blank}. You can also [see the difference between all three standards and their use cases](https://academy.ivanontech.com/blog/non-fungible-tokens-explaining-nfts-erc-721-and-erc-1155){target=_blank}. ERC-1155 was created by [Enjin](https://enjin.io/about/erc-1155){target=_blank} and can be used in gaming, so non-fungible items like a player or item can hold fungible assets like gold or coins. We will see later on how this is applicable.

## NFT Hype via Art

Maybe you have heard of [Crypto Punks](https://www.christies.com/features/10-things-to-know-about-CryptoPunks-11569-1.aspx){target=_blank}, [Disaster Girl NFT](https://www.npr.org/2021/04/30/992383825/disaster-girl-the-stuff-of-memes-sells-for-nearly-500-000-as-nft){target=_blank}, [Beeple’s 69 million dollar NFT](https://www.theverge.com/2021/3/11/22325054/beeple-christies-nft-sale-cost-everydays-69-million){target=_blank}, [Damien Hirst’s NFTs](https://consensys.net/blog/press-release/palm-a-new-nft-ecosystem-and-studio-for-creators-announces-launch-of-first-project-with-damien-hirst/){target=_blank}, [Bored Yacht Club](https://www.benzinga.com/markets/cryptocurrency/21/08/22606848/logan-paul-chris-camillo-buy-bored-ape-yacht-club-nfts-floor-rises-what-investors-should-k){target=_blank}, [RarePizzas](https://www.rarepizzas.com/){target=_blank}, [Pudgy Penguins](https://www.coindesk.com/pudgy-penguins-bored-apes-nft-new-boom){target=_blank}, [EulerBeats](https://eulerbeats.com/){target=_blank} and [pplpleasr](https://foundation.app/@pplpleasr){target=_blank}? Even [Edward Snowden](https://foundation.app/@Snowden/stay-free-edward-snowden-2021-24437){target=_blank} and [others](https://opensea.io/){target=_blank} have found a new market for their art. Haven’t heard of them? You can get hip to it on [CryptoTwitter](https://consensys.net/blog/news/i-read-crypto-twitter-for-hours-daily-here-are-the-40-accounts-that-really-matter/){target=_blank}, sign up for [Bankless’s MetaVersal newsletter ](https://metaversal.banklesshq.com/?utm_source=substack&utm_medium=menu){target=_blank}or use [Non-fungible.com](https://nonfungible.com/){target=_blank} for real time digital asset tracking to help you to navigate NFT markets.

![Disater Girl NFT](https://lh6.googleusercontent.com/egaC09kd_93f6IMFPs3-6O8SxndpXrcDR7HW8SiW7584esRHV6wwFmDee_MG9qajbO7GgiI2KTj92Xf1JQB7afjlULIRRXH1h4J9ICdPT7wCRtz3j_okYKDyqsj-KELmzaDgS_nR=s0){target=_blank}

What's the deal with the hype? Why is this so important? First, you may want to learn the quick [History of NFTs via Potion](https://blog.portion.io/the-history-of-nfts-how-they-got-started/){target=_blank}. Then, two highly recommended videos on NFTs that can explain more are [The Defiant Guide to Digital Art and NFTs](https://www.youtube.com/watch?v=XqveU599ojg){target=_blank} and [The Greatest NFT Film Ever Made by The Defiant](https://www.youtube.com/watch?v=cY9lM73ie0Q){target=_blank}.

The most prolific and accessible usage of NFTs is art and gaming. What is art? According to Andy Warhol, "Art is what you can get away with". The [message can be the medium](https://en.wikipedia.org/wiki/The_medium_is_the_message){target=_blank} as [Andy Wahorl proved by using mass production and consumerism in his art](https://emptyeasel.com/2007/05/22/andy-warhol-mass-produced-art-with-popular-appeal/){target=_blank}.

How are they a better way than just releasing art on the internet?

## Why NFTS

### Telephone problem: Provenance

Ethereum also solves the "telephone problem", where information is changed over time. Since Ethereum has an immutable ledger, one could track changes to historical digital artefacts over time. Most importantly, it can track provenance for items, whether cultural or utilitarian, like olive oil. This is important because Ethereum can be used as a store of historical value, like culture.

### Zero costs, zero pricing

The internet of information allowed anyone to disseminate culture. Easy copying means that due to the near-zero cost of replicating information, the value of any art that could be digitized is reduced close to zero. Additionally, any value accrued was captured by the middlemen who controlled the servers and could set the market rules. Even with strong branding and engagement, the middlemen can extract large amounts of value, as we will see in the following section.

### Power through markets

The properties of Ethereum change this. The commoditization of network servers and databases through a single world computer allows the artist to move between providers. Enforced digital scarcity limits authentic copies and enforces legitimacy and social signalling. Programmable smart contracts enable creators to set the rules of the game for their art and capture value how they see fit. In theory, this means being paid every time the art changes owners, not just on the first sale. It also means that the art can carry its own set of tokenomics, creating hype via price action.

Ownership means that the asset can be used as collateral, rented, or licensed in a digitally enforced manner. These are unique only to blockchain-based networks. With [EIP-2981- The Royalty Standard](https://eips.ethereum.org/EIPS/eip-2981){target=_blank}, creators can enable universal support for [royalty payments](https://consensys.net/blog/blockchain-explained/can-nfts-crack-royalties-and-give-more-value-to-artists/){target=_blank} across all NFT marketplaces and ecosystem participants. This solves the problem of being tied to any NFT marketplace, which we will discuss later. In addition, creators can leverage [EIP-2615 - The Non-Fungible Token with mortgage and rental functions](https://eips.ethereum.org/EIPS/eip-2615){target=_blank} to turn their NFTs into streams of income. These EIPs can be helpful in art markets as well as gaming economies, as we shall see.

There are [various ways users and artists can make money off NFTs](https://consensys.net/blog/codefi/roi-opportunities-for-nfts/){target=_blank}. Services like [reNFT](https://www.renft.io/){target=_blank} allow users to rent their NFTs. [NFTfi](https://nftfi.com/){target=_blank} enables users to use them as collateral. This solves the issue of using assets with potentially illiquid markets for collateralized loans. Don't know what NFT to buy or don't have enough cash to buy a whole one? [NFTx](https://nftx.org/){target=_blank} allows users to mint and buy into decentralized NFT index funds that fractionalize NFTs into ERC-20 tokens.

Platforms like [Rariable](https://rarible.medium.com/introducing-rari-the-first-governance-token-in-the-nft-space-5dbcc55b6c43){target=_blank} and [Unicly](https://www.unic.ly/){target=_blank} even engage in a liquidity mining program to incentivize users to buy and sell NFTs in exchange for tokens. These can be used for governance or sold on open markets.

Ethereum can help decentralize art markets and games, giving artists and users/collectors a more direct connection, reducing dominant brokers' cartel-like behaviour. It also unites fragmented markets by placing them on the internet [and helping to bring a new crowd to Ethereum](https://consensys.net/blog/news/why-nfts-not-defi-brought-ethereum-to-the-mainstream/){target=_blank}. In the process, users begin to understand decentralization and are exposed to DeFi-like mechanics.

## Myths: Legitimacy and Coordination

Why is disseminating culture important? Myths are all around us. They inform and are part of the substrate of our belief and value systems. Pragmatically speaking, it's why people attach value to Yeezys or Balenciaga. Or why they choose Harvard over their local state college. It's why Jordans have a better cultural cache than Shaqs. According to [Yoval Noah Harari in his book Sapiens](https://fs.blog/2016/01/why-humans-dominate-earth/){target=_blank}, myths are social fiction that allows humans to scale collaboration from small tribes to millions of people.

Legitimacy is what separates the in-group from the outgroup. It keeps the imposters who wish to mimic and gain a group's benefits without the costs. [Legitimacy underpins social signalling, which allows for coordination between groups](https://vitalik.ca/general/2021/03/23/legitimacy.html){target=_blank}. We find [social signalling](<https://en.wikipedia.org/wiki/Signalling_(economics){target=_blank}>){target=_blank} in economics and [evolutionary biology](https://psychology.wikia.org/wiki/Signalling_theory){target=_blank}. On a practical level, NFTs make it easier to call out posers. Or as they say, "You gotta pay the cost to be da boss". Being provable scarce allows for legitimacy to be enforced. However, this is not to say that the technology is perfect. There are some issues with using NFTs to prove outright authenticity, as [fraudsters try to impersonate others and reupload their works](https://www.theverge.com/2021/3/20/22334527/nft-scams-artists-opensea-rarible-marble-cards-fraud-art){target=_blank}.

Myths > values > choice > signalling > legitimacy > coordination.

![myths-quote](/docs/img/S05/myths-quote.png)

[@punk6929 in this tweet thread 🧵 ](https://twitter.com/punk6529/status/1424127515476598796){target=_blank} beautifully sums up the role of NFTs in creating culture, myths and scaling human collaboration.

Myth Building, or "branding and marketing", allows companies to place a logo on an item and charge the idea. It allows celebrities to earn hefty sums of money for a brand's association with them. Myths underpin even cryptocurrencies if we take a look at Bitcoin or Dogecoin.

![jordan-nft-quote](/docs/img/S05/jordan-nft-quote.png){target=_blank}

Myths inform branding, which informs a user's choices based on their values. Creators can be artists or scientists. NFTs can even give control to creators of [scientific intellectual property](https://medium.com/molecule-blog/ip-nfts-for-researchers-a-new-biomedical-funding-paradigm-91312d8d92e6){target=_blank}. Ultimately, NFTs give the economics and control of these myths to their creators 💪.

They can be used in conjunction with DAO to create art to fund causes like how [Rare Pizzas](https://www.rarepizzas.com/){target=_blank} uses [NFTs to fund free pizza for people on Bitcoin Pizza Day](https://thespoon.tech/the-creators-behind-rare-pizzas-want-to-use-pizza-art-nfts-to-fund-a-global-real-world-pizza-party/){target=_blank}. Or [FlamingoDAO to fund NFTs](https://flamingodao.xyz/){target=_blank}.

## How to get NFTs

There are various places where you buy or sell NFTs. Check out the links for guides on leading platforms [OpenSea](https://consensys.net/blog/metamask/explore-the-vast-ocean-of-nfts-with-opensea/){target=_blank}, [Foundation](https://consensys.net/blog/metamask/how-to-buy-nfts-on-foundation-using-metamask/){target=_blank}, [Rarible](https://newsletter.banklesshq.com/p/how-to-make-money-with-digital-art){target=_blank}, [Zora](https://metaversal.banklesshq.com/p/how-to-mint-nfts-on-zora){target=_blank}, [SuperRare](https://newsletter.banklesshq.com/p/how-to-make-money-on-digital-art){target=_blank}, [Mintable](https://www.youtube.com/watch?v=oZgobGr77NI){target=_blank}, or [Palm NFT Sidechain](https://palm.io/studio/palm-token-bridge/){target=_blank}. Get a [deep dive into the status of the industry here](https://consensys.net/blog/codefi/how-nft-art-marketplaces-are-merging-with-defi/){target=_blank}.

As convenient as these platforms are, [there are issues with them](https://blog.portion.io/the-pitfalls-of-centralized-nft-platforms/){target=_blank}. Some of these issues relate to centralization risk, which increases censorship or your assets being deleted. Some platforms control your keys, which means you don't really own the NFT. There is a lack of data portability fragments markets and limits royalties between platforms. Finally, there is a centralization risk with any data which underpins the NFT could also be stored on a centralized server.

In the next part, we will see how to create an NFT and leverage tools to decentralize your assets.

## Creating NFTs

You can create your own NFTs! Learn how to [create your own NFT via Ethereum.org](https://ethereum.org/en/developers/tutorials/how-to-write-and-deploy-an-nft/){target=_blank}. Furthermore, you can host them on a decentralized file storage solution like [NFT.storage](https://nft.storage/){target=_blank}. It’s powered by [IPFS](https://ipfs.io/){target=_blank} and [Filecoin](https://filecoin.io/){target=_blank}. To set up, go through the [nft.storage](https://nft.storage/#docs){target=_blank} instructions. Want to learn more? Go to [nftschool.dev](https://nftschool.dev/){target=_blank} to learn about best practices. Feel free to check out the [Filecoin Truffle Box](https://github.com/truffle-box/filecoin-box){target=_blank} and [these set up instructions](https://docs.google.com/presentation/d/1n3ZgZ-b5P6B_fRhKP5t7evPxZJuLC3cnRqMQMduAbTk/edit#slide=id.p){target=_blank}.

But what about art? You can use Adobe Photoshop or open-source tools like [GIMP](https://www.gimp.org/){target=_blank} image editor or [Blender](https://www.blender.org/){target=_blank} for 3D creation. Pro tip: you can check out the Decentraland Discord and ask what tools developers use to build things.

Want to go the programmatic route to create NFTs like [this generative art example](https://www.reddit.com/r/NFT/comments/mu1azt/my_first_generative_art_mint_on_foundation_made/){target=_blank} or [this example](https://www.reddit.com/r/NFTsMarketplace/comments/mu6gz3/my_first_generative_art_mint_on_foundation_made/){target=_blank}? [Generative Art](https://en.wikipedia.org/wiki/Generative_art#:~:text=Generative%20art%20refers%20to%20art,made%20directly%20by%20the%20artist.){target=_blank} let's the code create the art. Use [P5.js](https://p5js.org/){target=_blank}, the JavaScript library, for creating coding. It focuses on making coding accessible for artists, designers, beginners and anyone else! See a [great example of generative art here](https://www.youtube.com/watch?v=me04ZrTJqWA){target=_blank}.

[Dan Shiffman](https://shiffman.net/){target=_blank}, the creator of [The Coding Train](https://thecodingtrain.com/){target=_blank}, has [the most comprehensive videos on how to use P5.js on the internet](https://www.youtube.com/watch?v=HerCR8bw_GE&list=PLRqwX-V7Uu6Zy51Q-x9tMWIv9cueOFTFA){target=_blank}. He also has some of the best and most ENTERTAINING videos on learning to code. In addition, he wrote a fantastic book called [The Nature of Code](https://natureofcode.com/book/){target=_blank}, which shows you how to model nature with JavaScript. The book has a [video series](https://www.youtube.com/watch?v=70MQ-FugwbI&list=PLRqwX-V7Uu6ZV4yEcW3uDwOgGXKUUsPOM){target=_blank} you can follow along. If you can support his channel, please donate to support his work ♥️.

You can combine [P5.js with physics libraries](https://www.youtube.com/watch?v=wB1pcXtEwIs){target=_blank} like [Matter.js](https://www.youtube.com/watch?v=urR596FsU68){target=_blank} or PhysicsJS. For a 3D library, you can try out ThreeJS. You can check out [this tutorial to see how to create generative art using P5.js and React, mint an NFT and host it on your website](https://www.youtube.com/watch?v=3obwBHN4RgA){target=_blank}. Also, check out [BeyondNFT to learn how to build interactive NFTs with p5JS and ThreeJS](https://beyondnft.io/create){target=_blank}.

How about using [TensorFlowJS](https://www.youtube.com/watch?v=Qt3ZABW5lD0){target=_blank} to get user input and try to figure out how to get interactions with your NFTs. Maybe, they can "learn" from their users and record some version of that data on-chain 🤷‍♂️.

You can also [explore how to add royalties for various platform secondary sales with this tutorial](https://medium.com/aisthisi/aisthisi-technical-deep-dive-part-2-5250b0d71ee){target=_blank}.

What if you can go beyond NFTs and create in-game assets that can make money?

![|250x249](https://lh5.googleusercontent.com/Z6s1gBKrQnWP1LcqdfkMf342woynzwOcv4krmajmlRWqgXvYf3sOXdE9ajuSfeCJggmdPb3Ac4iCHd3wKiMSG-Vqkn643yNkCoyXnuoJ-XBwCuv_6VMp69JbIouZrGpQ0JSLzskI=s0)

## The MetaVerse: Gaming and NFTs

Fun fact: the genesis of Ethereum sort of started with games. Vitalik Buterin discovered [the evils of centralized entities after losing his World of Warcraft assets](https://cointelegraph.com/ethereum-for-beginners/who-is-vitalik-buterin){target=_blank}. The [first NFTs were created by a blockchain-based game called CryptoKitties](https://blog.portion.io/the-history-of-nfts-how-they-got-started/){target=_blank}. Enjin created the ERC1155 standard for gaming applications.

Turns out, [NFTs are a crucial building block](https://www.yahoo.com/now/blockchain-games-nfts-integral-part-153545092.html){target=_blank} to the [metaverse](https://en.wikipedia.org/wiki/Metaverse){target=_blank} and in-game economies. AXIE Infinity is proving to [be the killer app of Gaming and NFTs](https://decrypt.co/76333/crypto-game-axie-infinity-has-generated-84-9m-one-month){target=_blank}, with [more revenue than Uniswap and even Ethereum itself](https://thedefiant.io/axie-infinity-revenue-beats-ethereum/){target=_blank}. Gaming is the best place due to feedback loops and the utility of the NFT. In-game items can be represented as NFTs. A game's feedback loop keeps the users engaged and can give added value to the NFTs. Straight out of the book [Ready Player One](https://en.wikipedia.org/wiki/Ready_Player_One){target=_blank}, play-to-earn is an emerging phenomenon where [people playing games are earning more than the average income in some developing nations](https://www.youtube.com/watch?v=Yo-BrASMHU4){target=_blank}.

![|479x217](https://lh4.googleusercontent.com/8A6Ev7tzhnfhtkQG-dygcY5omyMlkoKY43mQAE7R6woVV0HOhd6GVAVJHxuTUCHo0vMgqj052Dh8b-j8wQoM31Od7f6y8juanQKtmFuF82tOAVz9750gUjU-iBLxsSsmhnQjzzkz=s0)

Massively multiplayer online role-playing games like [Everquest](http://www.todayifoundout.com/index.php/2019/03/that-time-a-video-game-had-an-economy-almost-as-strong-as-russia/){target=_blank}, [World of Warcraft](https://joshkaufman.net/everything-i-know-about-business-i-learned-from-world-of-warcraft/){target=_blank}, [EVE Online](https://www.youtube.com/watch?v=ijhAILUNz_s){target=_blank}, have already had internal game economies for years. [Fortnite](https://www.investopedia.com/tech/how-does-fortnite-make-money/){target=_blank} and [Roblox](https://www.statista.com/statistics/1190638/quarterly-revenue-roblox-corporation/){target=_blank} make massive amounts of money. These game economies can [yield interesting data](https://conf.splunk.com/files/2020/slides/PLA1729C.pdf){target=_blank}. However, centralization plagues the game creators and players themselves. Game developers can act as central banks and skew imperfect "markets". Game developers themselves have to fork over tons of money to app stores. Worst of all, markets don't exist since players can't trade with each other.

![|624x89](https://lh3.googleusercontent.com/XJJ_9gM0HJdRbsLA8TVIgoLQv4dkAsxT3Ashp0I_75FFx_yR0hh_8k4xGDplzStqsLXjZwtV7f4jOkAHsMGO5MCv4d8wBE6_U0kK6yin4ulQ9coZVSDNGh1vunJg8a1PinU5JwWM=s0)

## Blockchains are the new app stores

Fortnite, Roblox, and other games have to pay massive fees to centralized app store providers for all the money they make. [Roblox pays 24%](https://developer.roblox.com/en-us/articles/developer-economics){target=_blank} of all money generated to App Stores. [Fortnite famously sued Google and Apple for the large cut they took](https://www.cnn.com/2021/02/10/tech/tim-sweeney-epic-games-risk-takers/index.html){target=_blank}.

![|624x271](https://lh4.googleusercontent.com/YUjZ2E_LErKoSUdy_sAFcv16vj9FQO34TE1hQZsNExiCY5IpUNrFHryYFjssC-QjXjDB5oQJhd0cQNO8FUGgQf6lJOdn3IBEPs7h6F9mX-oEizHE4cvKma7HW7T6hTbCsYEQevbq=s0)

See [Chiris Dixon's thread 🧵](https://twitter.com/cdixon/status/1427452472046493704){target=_blank}

Blockchain-based games can solve a lot of market-based problems caused by centralized games for users and games. Costly fees could be avoided. Better [player-led internal economies where users own their assets forever](https://blog.godsunchained.com/ethereum-is-the-future-of-gaming%E2%80%8A-%E2%80%8Aand-wed-like-to-prove-it/){target=_blank} and freely trade with each other. Games and assets can be transferred between platforms. Third-party developers won't have to worry about changing in-game economics.

## DeFi within Gaming economies

Games like [AXIE Infinity](https://www.decentralised.co/the-economics-behind-axie-infinity/){target=_blank}, [Decentraland](https://tokeneconomy.co/decentraland-lords-9953d0de1e5c){target=_blank},and [Gods Unchained](https://godsunchained.com/){target=_blank} build [actual in-game economies](https://andrewsteinwold.substack.com/p/-the-scarce-web){target=_blank} where players can trade. Decentralized App stores like [MetaZone](https://metazone.io/){target=_blank} are emerging where users can create assets for open-world games. By using DeFi patterns like AMMs, lending markets, index funds, using assets as collateral, users can help manage their economies. Emerging standards around rental, royalty will expand the ways users can play games to earn money. That way, the rewards of this cultural product can go to the creators and players, not just the game companies.

These in-game economies grow because of the demand for scarce assets. Internal economies can use the existing DeFi patterns we have seen to help this. However, different games will have fragmented liquidity and assets since they would conceivably use their own custom EVM compatible chain. Using cross-chain lending markets and yield farming for in-game assets sounds familiar to cross-chain yield farming or lending markets in DeFi. Projects like Yield Guild are looking to help fix this issue. Worst case scenario, all these assets can convert to ETH, and we would see network effects between games and other ecosystems.

We have already seen tokenized real estate in games like Decentraland. Out of this is [emerging rental agreements](https://metaverse.properties/rent-in-decentraland/){target=_blank}, which could eventually be applied in other scenarios. Rental income can allow for usage of NFT to earn a yield and split the income to the originator. Say if one rents a plot of land on a digital game like Decentraland, and an NFT represents that plot. Lending markets would allow players to rent assets and share the profits, or XP points can be another application. You can even [buy ad space within Decentraland](https://nftplazas.com/promotion/){target=_blank}.

Over time, it will be easy to see how game guilds could transform into DAO managing, trading, collaborating, and competing over resources. This sounds a lot like modern companies. And it all happened with memes and magical internet money.

## Additional Resources

- [NFT School via nftschool.dev](https://nftschool.dev/){target=_blank}

- [The History of NFTs via Potion](https://blog.portion.io/the-history-of-nfts-how-they-got-started/){target=_blank}

- [The Defiant Guide to Digital Art and NFTs](https://www.youtube.com/watch?v=XqveU599ojg){target=_blank}

- [The Greatest NFT Film Ever Made by The Defiant](https://www.youtube.com/watch?v=cY9lM73ie0Q){target=_blank}

- [Mark Cuban on Digital Collectables via The Defaint](https://www.youtube.com/watch?v=GdGseBuuq_I&t=2329s){target=_blank}

- [The Most Important Scarce Resource is Legitimacy by Vitalik Buterin](https://vitalik.ca/general/2021/03/23/legitimacy.html){target=_blank}

- [Legitimacy | Vitalik Buterin via Bankless](https://www.youtube.com/watch?v=mr_Xc_a1mKI&t=5262s){target=_blank}
