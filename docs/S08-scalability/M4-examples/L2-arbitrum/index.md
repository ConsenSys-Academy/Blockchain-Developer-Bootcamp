# Arbitrum Example

In this lesson, we're going to walkthrough setting up a development environment for the optimistic rollup protocol [Arbitrum](https://developer.offchainlabs.com/){target=\_blank}, built by Offchain Labs.

As we've discussed before, optimistic rollups offer an easier path to scaling in certain situations since they leverage much of the same toolkit as EVM development. Out of the box, Arbitrum supports [Solidity](https://developer.offchainlabs.com/solidity-support){target=\_blank} as well as [Truffle, Hardhat, The Graph, etc](https://developer.offchainlabs.com/getting-started-devs){target=\_blank}. You can see the differences between Ethereum and Arbitrum [here](https://developer.offchainlabs.com/arb-specific-things){target=\_blank}.

Like Optimism, Arbitrum's consensus layer is a dispute-based one, using a process called interactive challenges. With the release of Arbitrum Nitro, the newest iteration of the Arbitrum Optimistic Rollup protocol, the Validator set (those able to pose challenges) is whitelisted. Over time, Arbitrum intends to remove the whitelist and open validation to everyone.

Arbitrum <--> Mainnet bridging is live, and the Arbitrum documentation has some information for how to implement bridging in your project. See the current capabilities [here](https://developer.offchainlabs.com/asset-bridging){target=\_blank}.

**Again, we want to stress how new this technology is. You should be extremely cautious when working with it and be aware that documentation may not be up to date.**

The requirements and setup for Arbitrum are very similar to the previous lesson on Optimism. We'll also be using our `SimpleStorage.sol` contract as a generic stand-in for your dapp's contract. Feel free to swap it out!

## Requirements

- Node.js 10.x or later
- NPM version 5.2 or later
- [docker](https://docs.docker.com/get-docker/){target=\_blank}, version 19.03.12 or later
  [docker-compose](https://docs.docker.com/compose/install/){target=\_blank}, version 1.27.3 or later
- Recommended Docker memory allocation of >=8 GB.

You'll also need to setup an Arbitrum project on your Infura account. You don't have to update your account, right now access is being offered at the "core" level for free up to 100,000 daily requests. You must enable the Arbitrum Rollup ADD-ON under the billing section under Manage Add-Ons in your Infura account Settings for the API requests to work properly. When setting up your project, be sure to select the "Ethereum" network. Then, under settings, select the "Arbitrum Goerli" testnet, as shown below:

![Setting up an Infura project for Arbitrum testnet](../../../img/S08/arbitrum-tutorial-1.png)

You'll also need to have Goerli test ETH for the project if you'd like to run it on a public testnet. Follow the steps on the Goerli testnet faucet [here](https://goerli-faucet.pk910.de/){target=\_blank} to get some.

Once you have Goerli test ETH, you'll need to bridge it to Arbitrum testnet. Follow these steps:

1. Add Arbitrum Ethereum as a Custom RPC to your Metamask wallet, using [the information here](https://developer.offchainlabs.com/public-chains){target=\_blank}, except set the RPC URL to `https://arbitrum-goerli.infura.io/v3/" + infuraKey`
2. Go to [this site](https://bridge.arbitrum.io/){target=\_blank} and bridge your Goerli ETH to Arbitrum Nitro Goerli ETH
3. Ensure that your `arbitrum_testnet` network in `truffle-config.arbitrum.js` is the mnemonic associated with your Arbitrum Nitro Goerli MetaMask wallet we just bridged.

Let's get started! (For more detail, you can find the tutorial this lesson is based on [here](https://www.trufflesuite.com/boxes/arbitrum){target=\_blank}.)

## Setup

From a new directory, `unbox` the Arbitrum box:

```bash
truffle unbox arbitrum
```

You will need at least one mnemonic to use with the network. The `.dotenv` npm package has been installed for you, and you will need to create a `.env` file for storing your mnemonic and any other needed private information.

The `.env` file is ignored by git in this project, to help protect your private data. In general, it is good security practice to avoid committing information about your private keys to github. The `truffle-config.arbitrum.js` file expects a `MNEMONIC` value to exist in `.env` for running commands on each of these networks, as well as a default `MNEMONIC` for the Arbitrum network we will run locally.

If you are unfamiliar with using `.env` for managing your mnemonics and other keys, the basic steps for doing so are below:

1. Use `touch .env` in the command line to create a `.env` file at the root of your project.
2. Open the `.env` file in your preferred IDE
3. Add the following, filling in your own Infura project key and mnemonics:

    ```bash
    MNEMONIC="jar deny prosper gasp flush glass core corn alarm treat leg smart"
    INFURA_KEY="<Your Infura Project ID>"
    GOERLI_MNEMONIC="<Your Goerli Mnemonic>"
    MAINNET_MNEMONIC="<Your Arbitrum Mainnet Mnemonic>"
    ```

    _Note: the value for the `MNEMONIC` above is the one you should use, as it is expected within the local arbitrum network we will run in this Truffle Box._

4. As you develop your project, you can put any other sensitive information in this file. You can access it from other files with `require('dotenv').config()` and refer to the variable you need with `process.env['<YOUR_VARIABLE>']`.

### Some Differences

You may notice some differences in the workflow from our typical Truffle environment. For example, a new configuration file exists in this project: `truffle-config.arbitrum.js`. This file contains a reference to the new file location of the `contracts_build_directory` and `contracts_directory` for Arbitrum contracts and lists several networks for running the Arbitrum Layer 2 network instance.

Please note, the classic `truffle-config.js` configuration file is included here as well, because you will eventually want to deploy contracts to Ethereum as well. All normal truffle commands (`truffle compile`, `truffle migrate`, etc.) will use this config file and save built files to `build/ethereum-contracts`. You can save Solidity contracts that you wish to deploy to Ethereum in the `contracts/ethereum` folder.

Another difference: When you compile or migrate, the resulting `json` files will be at `build/arbitrum-contracts/`. This is to distinguish them from any Ethereum contracts you build, which will live in `build/ethereum-contracts`. As we have included the appropriate `contracts_build_directory` in each configuration file, Truffle will know which set of built files to reference.

## Compiling

To compile your Arbitrum contracts, run the following in your terminal:

```bash
npm run compile:arbitrum
```

This script lets Truffle know to use the `truffle-config.arbitrum.js` configuration file, which tells Truffle where to store your build artifacts. When adding new contracts to compile, you may find some discrepancies and errors, so please remember to keep an eye on [differences between ethereum and Arbitrum](https://developer.offchainlabs.com/arb-specific-things){target=\_blank}.

## Migration

Now that we've compiled the contract for Arbitrum, we can migrate it to the Arbitrum Nitro Layer 2 network. First, let's just try to our local Ganache, which will be almost similar to a normal Ethereum ganache instance:

```bash
npm run migrate:arbitrum --network=ganache
```

This may be a bit underwhelming! However, if we have loaded in our Infura Arbitrum Goerli network endpoint and have enough Arbitrum Goerli ETH in the wallet tied to the `.env` mnemonic, we can also run:

```bash
npm run migrate:arbitrum --network=arbitrum_testnet
```

Like standard Truffle, if you would like to migrate previously migrated contracts on the same network, you can run `truffle migrate --config truffle-config.arbitrum.js --network=(arbitrum_local | arbitrum_goerli | arbitrum_mainnet)` and add the `--reset` flag if you have previously run these migrations.

Following the above steps should allow you to deploy to the Arbitrum Layer 2 chain. This is only the first step! Once you are ready to deploy your own contracts to function on Layer 1 Ethereum using Layer 2 Arbitrum, you will need to be aware of the ways in which [Layer 1 and Layer 2 interact in the Arbitrum ecosystem](https://developer.offchainlabs.com/docs/bridging_assets){target=\_blank}.

Furthermore, keep an eye out for new developments in Truffle tooling to assist with bridging L1-L2 data and execution.

## Additional Material

- [Docs: Arbitrum Quickstart](https://developer.offchainlabs.com/docs/developer_quickstart){target=\_blank}
- [Tutorial: Truffle's Pet Shop Box on Arbitrum](https://github.com/OffchainLabs/arbitrum-tutorials/tree/master/packages/demo-dapp-pet-shop){target=\_blank}
