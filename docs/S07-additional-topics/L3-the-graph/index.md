# The Graph

[The Graph](https://thegraph.com/) is a decentralized protocol for indexing and querying data on public blockchain infrastructure. The Graph organizes and makes it easy to query on-chain data in a way that was not possible in the past, with GraphQL. Querying blockchain data is difficult. Node clients can be inconsistent, application developers are required to write proprietary code and build centralized servers for ingesting the data, and they need to manage their own APIs for uptime and optimal UX. The Graph aims to solve this problem by abstracting the back-end, pre-aggregate data and making it significantly more efficient for developers to retrieve on-chain data. See video below:

<!-- blank line -->
<figure class="video_container">
  <iframe src="https://www.youtube.com/embed/X_2ln79Qb-Q" frameborder="0" allowfullscreen="true"> </iframe>
</figure>
<!-- blank line -->

GRT is the native Graph token that is used to coordinate Indexers, Curators and Delegators around providing on-chain data to applications. Node operators, called Indexers, stake and earn GRT for indexing subgraphs and processing queries for dApps, such as querying for aggregate trade volume on DEXs. Delegators contribute to the security of the network by delegating their GRT stake to Indexers and also earning a portion of query fees. Delegation enables Indexers to grow in proportional size on the network and increase their indexing operation to serve more applications. Anyone can delegate GRT to Indexers to secure the network and earn rewards. Curators organize data on The Graph by signaling GRT on useful APIs, called subgraphs. Indexers look out for subgraph signal to understand which subgraphs should be prioritized based on the collective sentiment and aggregate signal.

Signaling on a subgraph is a mechanism similar to leaving Yelp reviews, whereby all participants are curating the quality of the ecosystem. Indexers, Delegators, and Curators work together to organize the data for the crypto economy and maintain a useful global API for DeFi and Web3.

## What is a Subgraph?

In the traditional web stack, databases, servers, and APIs query, filter, sort, paginate, group, and join data before it is returned to some client application usually via some type of http request. These types of data transformations are not possible when reading data directly from Ethereum or other blockchains. In the past, developers were getting around this by building their own centralized indexing servers - pulling data from blockchains, storing it in a database, and exposing it over an API. This required significant engineering and hardware resources that broke the important security properties required for decentralization.
Through The Graph’s protocol, developers can deploy subgraphs (open source APIs) to query on-chain data, for dapps like DeFi aggregators, wallets and NFT marketplaces. Alternatively, developers would need to build their own proprietary servers and act as a potential central point of failure for their dapp.

See the video below on why subgraphs are important to the dApp ecosystem:

<!-- blank line -->
<figure class="video_container">
  <iframe src="https://www.youtube.com/embed/NlmkqQQko5U" frameborder="0" allowfullscreen="true"> </iframe>
</figure>
<!-- blank line -->

## Why do we care about Subgraphs (dApp perspective)

Subgraphs enable blockchain data to be accessible via performant and open APIs with rich querying capabilities like enabling filtering, relationships, and full text search. They are a way to define which data you want to get indexed and how to store it. Subgraphs can be built to do pre-aggregations or calculations on their mappings, some are just used to organize on-chain event data. Then, an entity queries that data. This entity could be a dApp (company/developer, etc), or could be a telegram bot, or a discord bot or even a simple user doing a query to find information.

The value of using a subgraph when building a dApp is that your application data will always be indexed by a network of indexers, so that users can easily query your smart contract. This means that your API cannot be taken down and ensuring a decentralized network of Indexers and Curators will always serve your dapp’s queries. This also limits the risk of central points of failure. Imagine that no one knows what Wikipedia is because Wikipedia has not built a code to interact with Google’s index, therefore anyone querying searching information will not turn up any results from Wikipedia.

It is vital and in the best interest of the dApp team to develop a subgraph so that information is easily accessible to other developers in the Ethereum community. For example, the Uniswap subgraph is used by Uniswap.info as well as many other projects that are interested in querying Uniswap data such as trade volumes, prices or assets. Subgraphs are written in TypeScript and GraphQL SDL and queried using GraphQL. To learn more about GraphQL and how it will power the decentralized web as a data interoperability layer, read [this blog post](https://medium.com/graphprotocol/graphql-will-power-the-decentralized-web-d7443a69c69a) written by The Graph Co-founder and former Research Lead, Brandon Ramirez. Feel free to also check out The Graph's network documentation for [more details](https://thegraph.com/docs/about/introduction). 

Video explainer below:

<!-- blank line -->
<figure class="video_container">
  <iframe src="https://www.youtube.com/embed/DjnApXmdAKg" frameborder="0" allowfullscreen="true"> </iframe>
</figure>
<!-- blank line -->

## How to build a Subgraph

For a step by step guide on how to build a Subgraph, check out [this guide](https://thegraph.com/blog/building-with-subgraph-studio) written by DevRel lead, Nader Dabit at Edge & Node.

For a video guide, watch below!

<!-- blank line -->
<figure class="video_container">
  <iframe src="https://www.youtube.com/embed/HfDgC2oNnwo" frameborder="0" allowfullscreen="true"> </iframe>
</figure>
<!-- blank line -->

For a more general guide on how to get started with web3, check out [this guide](https://dev.to/dabit3/the-complete-guide-to-full-stack-ethereum-development-3j13).

## Querying from a Frontend Application

Follow [the guide in Gitpod](https://github.com/graphprotocol/full-stack-graph-app) and [video](https://www.youtube.com/watch?v=PjyKPMpahuc) below:

<!-- blank line -->
<figure class="video_container">
  <iframe src="https://www.youtube.com/watch?v=PjyKPMpahuc" frameborder="0" allowfullscreen="true"> </iframe>
</figure>
<!-- blank line -->

## API Key Management

Regardless of whether you’re a dApp developer or a subgraph developer, you’ll need to manage your API keys. This is important for you to be able to query subgraphs because API keys make sure the connections between application services are valid and authorized. This includes authenticating the end user and the device using the application.

The [Subgraph Studio](https://thegraph.com/studio/) will list out existing API keys, which will give you the ability to manage or delete them. For more details, follow along in the video below:

<!-- blank line -->
<figure class="video_container">
  <iframe src="https://www.youtube.com/embed/UrfIpm-Vlgs" frameborder="0" allowfullscreen="true"> </iframe>
</figure>
<!-- blank line -->

## The Graph Explorer

The Graph Explorer is a developer's decentralized portal into the world of subgraphs and network data. The Graph Explorer consists of multiple parts where developers can interact with other subgraph developers, dApp developers, Curators, Indexers, and Delegators. For a general overview of the Graph Explorer, check out the video below or read The Graph's documentation [here](https://thegraph.com/docs/explorer).

<!-- blank line -->
<figure class="video_container">
  <iframe src="https://www.youtube.com/embed/u224xf7rEBY" frameborder="0" allowfullscreen="true"> </iframe>
</figure>
<!-- blank line -->
