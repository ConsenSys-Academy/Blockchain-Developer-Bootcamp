
  
  <!-- Title goes below: -->
# Introduction to Truffle Suite

<!-- Content here: -->

Before we go into the Solidity section, we want to make sure you have a place where you can play around with the Solidity code you're starting to learn. Enter <a href="https://www.trufflesuite.com" target="_blank" rel="noopener noreferrer">the Truffle Suite!</a>

Truffle is an excellent tool to learn Solidity development but, as we'll show later in the course, it's also got advanced features. Don't be deceived by how easy it is!

## History and Evolution

As with any emergent ecosystem, tooling in the early days of EVM-based dapp development was somewhat primitive. Developers were required to install and utilize multiple, disjointed tools and services making for a complex workflow with a steep learning curve.

Things have come a long way since then, with tools and services like Codefi, Infura, Metamask, and OpenZeppelin Contracts that simplify a significant number of smart contract software development lifecycle stages.

Despite these advancements, there are still numerous pitfalls, particularly related to the security of your contracts, which makes web3 development different to what you might be used to when building against a more centralized paradigms.

## Why Truffle Suite?

The Truffle Suite was built to streamline the smart contract development process. Out of the box it includes a large, and growing, collection of commands that you can execute as you write, troubleshoot, and maintain your smart contracts.

A good example of this is contract compilation (wherein you convert your high-level contract code to something that can be natively understood by an Ethereum-node). As part of this feature, Truffle can also intelligently download the necessary compiler version(s) and even enable you to write your contracts in different language versions.

Additional reasons why developers might use Truffle to build their dapps include the following...

- Built-in support for compiling, deploying and linking your contract</li>
- An automated contract testing framework built on Mocha and Chai</li>
- A built-in console that allows you to directly interact with your compiled contracts</li>

This is just scratching the surface; as you’ll see when we dive-in, the Truffle Suite and the broader tooling ecosystem makes your life as a dapp developer both productive and fun!

## Installation

The following walks you through installation of both Truffle CLI and Ganache.

Truffle CLI

The Truffle Suite requires the following...

- Node.js v12 or later
- Windows, Linux or Mac OS X

Truffle also requires that you have a running Ethereum client which supports the standard JSON RPC API (which is nearly all of them). While there are many clients, the Truffle Suite also ships with <a href="https://www.trufflesuite.com/ganache" target="_blank" rel="noopener noreferrer">Ganache,</a> essentially a one-click EVM-based blockchain node for local testing.

For installing Node, we highly recommend using `nvm`. Follow the instructions [here](https://trufflesuite.com/docs/truffle/getting-started/installation/) to download Truffle!

After downloading Truffle, you can run Truffle from your command line anywhere on your machine.

If you are having trouble with installation, please post in [GitHub discussions](https://github.com/orgs/trufflesuite/discussions)!

## Ganache

Ganache has the same requirements as Truffle (as specified above). In addition, it also comes in two flavors, both a standalone CLI for more intermediate-advanced users and a UI version which is great for users that are just starting out. It’s worth noting that a version of Ganache also ships directly with Truffle which can be instantiated with the `truffle develop` command.  

Ganache CLI can be installed via the following:

```bash
$ npm install -g ganache
```

Ganache UI is available as download <a href="https://www.trufflesuite.com/ganache" target="_blank" rel="noopener noreferrer">here.</a>

Congratulations! You've just successfully installed Truffle and Ganache and are ready to get started developing.

## Introducing the Truffle Suite

Now that we have Truffle and Ganache installed, we’re nearly ready to begin diving in and writing our first smart contract. We'd like to cover a few more things before diving in.

### Network Support

As we discussed previously in the course, we are living in an increasingly multi-chain world. There are multiple popular public blockchain networks, and Truffle Suite aims to serve as many of these as is realistic.

At the time of writing, Truffle Suite supports development on networks that are EVM compatible and requires the network be Ethereum JSON-RPC compatible. Examples include:

- Ethereum
- Quorum
- Hyperledger Fabric
- Filecoin
- Polygon
- Arbritrum
- Optimism PBC
- Avalanche
- Aurora for NEAR

That said, Truffle’s richest support is for that of EVM (Ethereum Virtual Machine) based blockchains.

Given the above, the bulk of this section of the course will be specifically focused on EVM based chains (unless specified otherwise).

### Language Support

As highlighted earlier, amongst many other things, Truffle handles the compilation of your contracts from that of a higher-level language to Ethereum bytecode, which is the language “spoken” by the nodes on the network.

Out of the box, Truffle supports the following:

- Solidity
- Vyper
- <a href="https://docs.soliditylang.org/en/v0.8.6/yul.html" target="_blank" rel="noopener noreferrer">Yul</a> (experimental and not for beginners)
  
At the time of writing, Solidity is by far the most popular language for writing smart contracts, and as with everything in the space, things have been moving rapidly and have now witnessed some major projects built using Vyper.  

### Core Truffle Commands

Truffle is built around a large collection of commands that are used as a part of the contract development workflow. Examples of these include:

- `truffle init`
- `truffle compile`
- `truffle test`
- `truffle debug`
- `truffle migrate`

Note that you can see a complete list of the available commands by running `truffle help`.

As you can likely infer from the commands, they map to key stages of the development lifecycle. More on this in the upcoming section!

## Truffle Boxes

Up until now we’ve been writing all the code, scripts, and config ourselves, and while this follows the mantra of “learning by doing”, there’s another great resource at your disposal and that is <a href="https://www.trufflesuite.com/boxes" target="_blank" rel="noopener noreferrer">Truffle boxes</a>.

### Learning with Truffle boxes

As per the description, boxes are “helpful boilerplates” that comprise of sample contracts, front-end code (using a variety of different frameworks), and applied boxes that focus on a particular theme or protocol such as L2. From a learning standpoint they’re a useful to way to augment your learning by immediately getting hands-on. 

At the time of writing, here are some good boxes:

- Layer 2 (examples targeting <a href="https://www.trufflesuite.com/boxes/optimism" target="_blank" rel="noopener noreferrer">Optimism </a> and <a href="https://www.trufflesuite.com/boxes/arbitrum" target="_blank" rel="noopener noreferrer">Arbitrum</a>)
- <a href="https://trufflesuite.com/boxes/react/" target="_blank" rel="noopener noreferrer">React box example</a>

Installing a box is simply a case of using the unbox command, for example:

    $ truffle unbox optimism <directory path>


Beyond this, simply follow along with the <a href="https://github.com/truffle-box/optimism-box" target="_blank" rel="noopener noreferrer">optimism box readme</a>. You can find an example of how to use the Optimism box to build an NFT marketplace [here](https://trufflesuite.com/guides/nft-marketplace/).

We'll discuss boxes more when we dive deeper into developer tooling and more advanced Truffle, but feel free to explore available boxes.

In the next section, we'll take a simple smart contract and use it to explore the initial commands for developing using Truffle.