#StarkNet Example

## Background

StarkNet is a permissionless decentralized Validity-Rollup. It is not an EVM compatible chain.

StarkNet operates as an L2 network over Ethereum, enabling a dApp to achieve unlimited scale for its computation without compromising Ethereum’s composability and security. To achieve this StarkNet relies on the safest and most scalable cryptographic proof system, ZK-STARKs.

A ZK-STARK is a ***Z***ero-***K***nowledge ***S***calable ***T***ransparent ***AR***gument of ***K***nowledge.

ZK-STARKs allow StarkNet to move computations to a single off-chain STARK prover and then verify the integrity of those computations using an on-chain STARK Verifier.

StarkNet uses the [Cairo](https://github.com/starkware-libs/cairo-lang/) programming language both for its infrastructure and for writing StarkNet contracts. Cairo is a programming language for writing provable programs, where one party can prove to another that a certain computation was executed correctly. While it is possible to write smart contracts in Solidity to be deployed on StarkNet, they must first be transpiled to Cairo before deployment with a tool such as [Warp](https://github.com/NethermindEth/warp). 

**Again, we want to stress how new this technology is. You should be extremely cautious when working with it and be aware that documentation may not be up to date.**

Since the StarkNet protocol is not EVM-compatible, most Ethereum tooling you are used to will not work by default. For this reason, the Truffle StarkNet Box provides helpful instructions and scripts for getting started with StarkNet compilation, deployment, and testing.

The details of how to use the Truffle StarkNet Box are available [here](https://github.com/truffle-box/starknet-box/). Here, we will just go over the basics to help you get started.

## Setup

### Requirements
- [Node.js](https://nodejs.org/) 14.18.2 or later
- [NPM](https://docs.npmjs.com/cli/) version 6.14.15 or later
- [docker](https://docs.docker.com/get-docker/), version 20.10.10 or later
- Recommended Docker memory allocation of >=8 GB.
- Windows, MacOS or Linux

To get started using the Truffle StarkNet Box, run the following in your terminal: 

```bash
truffle unbox starknet
```

Once you have succesfully run the unbox command, you may choose to run the StarkNet devnet for a local network to test with. The command do so is as follows: 

```bash
npm run starknet:start_devnet
```

### Docker

The Truffle StarkNet Box uses two Docker images to compile and test StarkNet contracts. Accordingly, Docker must be installed on the host machine to make use of this box. The Docker images do not need to exist on the host machine prior to use - they will be pulled from the Docker Hub if they are not already available locally. Docker Desktop can be downloaded from the Docker website. We suggest that you read the [Docker installation guide](https://docs.docker.com/get-docker/) to suit your operating system.

### Configuration

As with the Optimism and Arbitrum Truffle Boxes, the Truffle StarkNet Box comes with a separate configuration file, `truffle-config.starknet.js`, containing network information, contract directory information, and compiler settings.

## Compiling

To compile all StarkNet contracts in your project, run the following: 

```bash
npm run starknet:compile
```

StarkNet has account abstraction (as you may recall, this means that an account is stored in a smart contract rather, and that all user wallets on StarkNet are actually smart contracts). In order to compile only your StarkNet account contracts, run the following in your terminal:

```bash
npm run starknet:compile --account
```

## Migration/Deployment

To deploy an account: 

```bash
npm run starknet:deploy_account
```

To deploy a contract:

```bash
npm run starknet:deploy --contract=contract 1000
```

## Endpoints

Note that you may configure **either** an [Infura](https://infura.io/) RPC endpoint or a Sequencer endpoint to access a network. All networks do not need to have the same type of endpoint configured. You may use an RPC endpoint with one network and a Sequencer endpoint with another if you wish. If an RPC endpoint configuration is present for a given network, it will be used rather than any Sequencer endpoint that may also be configured. If you wish to configure both types of endpoints for a network, you can simply comment out the endpoint configuration that you don't need. See the Truffle StarkNet Box for more detail. 

## Additional Functionality

The Truffle StarkNet Box offers additional functionality to make developing your dapp easier, like scripts to check your transaction status, call or invoke a contract method, and run unit tests. See the full StarkNet Box readme for additional details.

## Wallets

MetaMask does not work with StarkNet by default, but there is a [MetaMask Snap](https://consensys.net/blog/metamask/metamask-integrates-starkware-into-first-of-its-kind-zk-rollup-snap/) that allows for this functionality. 

If you choose, you may also try a different wallet to connect with StarkNet, such as [Argent](https://www.argent.xyz/argent-x/)

## Additional Materials
- [StarkNet and Cairo documentation](https://starknet.io/docs/index.html)
- [Information on Connecting to StarkNet With Infura](https://infura.io/networks/ethereum/starknet)
- [Using the StarkNet MetaMask Snap to Connect to StarkNet](https://consensys.net/blog/metamask/metamask-integrates-starkware-into-first-of-its-kind-zk-rollup-snap/)
