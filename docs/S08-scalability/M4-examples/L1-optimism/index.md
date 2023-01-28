# Optimism

Optimistic rollups are a great way to leverage all the tooling you've learned so far because they are generally compatible with the Ethereum Virtual Machine.

In the next few lessons, we're going to walk through some examples of how to actually use this new technology.

**Again, we want to stress how new this technology is. You should be extremely cautious when working with it and be aware that documentation may not be up to date.**

## Basic Mechanics

To create a sandboxed environment which guarantees deterministic smart contract execution between L1 and L2, Optimism uses an **Optimism Virtual Machine,** which replaces context-dependent EVM opcodes with their OVM counterparts. See a complete comparison of [the OVM vs EVM here](https://www.alchemy.com/overviews/optimistic-virtual-machine){target=\_blank}.

The OVM offers native account abstraction. This means the only type of account is smart contracts. This also means that all user wallets on Optimism are actually smart contracts. This is mostly not something to worry about, but it is worth noting that OVM transactions do not have a signature field, only a `to` address with a data payload.

To put it all together, the Optimism Rollup chain:

- Uses the OVM as its runtime/state transition function
- Uses Optimistic Geth as the L2 client with single sequencer
- Has solidity smart contracts deployed on Ethereum mainnet for data availability and dispute resolution/fraud proofs (you can read more about these "bridge" contracts [here](https://community.optimism.io/docs/protocol/protocol-2.0/#bridge-contracts){target=\_blank})

Top-level summary of how fraud proofs work:

1. Somebody will dispute a transaction if they disagree
2. They’ll publish all related state on Ethereum including a Merkle proofs for each piece of state
3. They will re-execute the state transition on-chain
4. They will be rewarded for correctly disputing, the malicious sequencer will get slashed, and the invalid state roots will be pruned guaranteeing safety

Optimism released an [EVM Equivalence Update](https://medium.com/ethereum-optimism/introducing-evm-equivalence-5c2021deb306){target=\_blank} in November 2021, and as a result there development team is redeveloping their fault proof process. The top-level view is unlikely to change, but fault proofs are currently disabled. Of note, this means that **users of the Optimism network currently need to trust the Sequencer node (run by Optimism PBC) to publish valid state roots to Ethereum**.

## Optimism Example

We'll be walking through the Optimism Truffle Box to show you how to deploy our SimpleStorage smart contract from previous lessons to Optimism!

After this example, you will be able to compile, migrate, and test Solidity code against a variety of Optimism test networks.

### Requirements

- Node.js 10.x or later
- NPM version 5.2 or later
- [docker](https://docs.docker.com/get-docker){target=\_blank}, version 19.03.12 or later
- [docker-compose](https://docs.docker.com/compose/install/){target=\_blank}, version 1.27.3 or later
- Recommended Docker memory allocation of >=8 GB.

You'll also need to setup an Optimism project from your Infura account. You don't have to update your account, right now access is being offered at the "core" level for free up to 100,000 daily requests. You must enable the Optimistic Ethereum ADD-ON under the billing section under Manage Add-Ons in your Infura account Settings for the API requests to work properly. When setting up your project, be sure to select the "Ethereum" network. Then, under settings, select the "Optimism Goerli" testnet, as shown below:

![Setting up an Infura project for Optimism testnet](../../../img/S08/optimism-tutorial-1.png)

You'll also need to have Goerli test ETH for the project if you'd like to run it on a public testnet. You can get some from this [Goerli testnet faucet](https://goerli-faucet.pk910.de/){target=\_blank}.

Once you have Goerli ETH, you'll need to bridge it to Optimism. After getting Goerli ETH, follow these steps:

1. Add Optimism Ethereum as a Custom RPC to your Metamask wallet, using [the steps here](https://help.optimism.io/hc/en-us/articles/6223777057179-Getting-started-with-MetaMask-and-Optimism){target=\_blank}, except set the RPC URL to `https://optimism-goerli.infura.io/v3/" + infuraKey`
2. Go to [this site](https://gateway.optimism.io){target=\_blank} and bridge your Goerli ETH to Optimism Goerli ETH
3. Ensure that your `optimistic_goerli` network in `truffle-config.ovm.js` is connected to your Optimism Goerli wallet.

_Note: You may get an error about your fee being too low when attempting to deploy to Optimistic Goerli. To bypass this error, you may need to increase the gas value in the optimistic_goerli network configuration in truffle-config.ovm.js to the value the error indicates. Gas price should be set at the transaction level, like so: `{ gasPrice: 15000000 }`._

Note, we'll also be building it locally so if you're having trouble finding Goerli ETH, you can start by running it locally.

Let's get started! (For more detail, you can find the tutorial this lesson is based on [here](www.trufflesuite.com/boxes/optimism){target=\_blank}).

## Setup

From a new directory, `unbox` the Optimism box:

```bash
truffle unbox optimism
```

You will need at least one mnemonic to use with the network. The `.dotenv` npm package has been installed for you, and you will need to create a `.env` file for storing your mnemonic and any other needed private information.

The `.env` file is ignored by git in this project, to help protect your private data. In general, it is good security practice to avoid committing information about your private keys to github. The truffle-config.ovm.js file expects a `GANACHE_MNEMONIC` and a `GOERLI_MNEMONIC` value to exist in `.env` for running commands on each of these networks, as well as a default `MNEMONIC` for the optimism network we will run locally.

If you are unfamiliar with using `.env` for managing your mnemonics and other keys, the basic steps for doing so are below:

Use touch `.env` in the command line to create a `.env` file at the root of your project.
Open the `.env` file in your preferred IDE
Add the following, filling in your own Infura project key and mnemonics:

```bash
MNEMONIC="candy maple cake sugar pudding cream honey rich smooth crumble sweet treat"
INFURA_KEY="<Your Infura Project ID>"
GANACHE_MNEMONIC="<Your Ganache Mnemonic>"
GOERLI_MNEMONIC="<Your GOERLI Mnemonic>"
```

_Note: the value for the `MNEMONIC` above is the one you should use, as it is expected within the local Optimism Ethereum network we will run in this Truffle Box._

As you develop your project, you can put any other sensitive information in this file. You can access it from other files with require('dotenv').config() and refer to the variable you need with `process.env['<YOUR_VARIABLE>']`.

### Some Differences

You may notice some differences in the workflow from our typical Truffle environment. For example, a new configuration file exists in this project: `truffle-config.ovm.js`. This file contains a reference to the new file location of the `contracts_build_directory` and `contracts_directory` for Optimism contracts and lists several networks for running the Optimism Layer 2 network instance.

Another difference: When you compile or migrate, the resulting `json` files will be at `build/optimism-contracts/`. This is to distinguish them from any Ethereum contracts you build, which will live in `build/ethereum-contracts`. As we have included the appropriate `contracts_build_directory` in each configuration file, Truffle will know which set of built files to reference.

## Compiling

The `SimpleStorage.sol` contract code is already in both the `ethereum` and `optimism` directories. To compile using the Optimism Virtual Machine compiler, run:

```bash
npm run compile:ovm
```

As we mentioned earlier, the OVM and EVM compiler are _slightly_ different, so keep an eye out for any issues or errors.

## Migration

Now that we've compiled the contract for Optimism, we can migrate it to an Optimism Layer 2 network. First, let's just try to our local Ganache, which will be almost similar to a normal Ethereum ganache instance:

```bash
npm run migrate:ovm --network=ganache
```

This may be a bit underwhelming! However, if we have loaded in our Infura Optimism Goerli network endpoint and have enough Optimism Goerli eth in the wallet tied to the `.env` mnemonic, we can also run:

```bash
npm run migrate:ovm --network=optimistic_kovan
```

Like standard Truffle, if you would like to migrate previously migrated contracts on the same network, you can run `truffle migrate --config truffle-config.ovm.js --network=(ganache | optimistic_ethereum | optimistic_goerli)` and add the `--reset` flag.

Following the above steps should allow you to deploy to the Optimism Layer 2 chain. This is only the first step! Once you are ready to deploy your own contracts to function on Layer 1 Ethereum using Layer 2 Optimism, you will need to be aware of the ways in which [Layer 1 and Layer 2 interact in the Optimism ecosystem](https://community.optimism.io/docs/developers/bridge/basics){target=\_blank}.

There is now a [Truffle Optimism Bridge Box](https://github.com/truffle-box/optimism-bridge-box) for those who would like to try out more advanced use cases with Optimism. A tutorial for the Bridge Box is [here](https://trufflesuite.com/blog/introducing-the-optimism-bridge-truffle-box){target=\_blank}.

## Additional Material

- [Optimism website](https://optimism.io){target=\_blank}
- [Docs: Optimism](https://community.optimism.io/docs){target=\_blank} Great documentation for different audiences, whether you want to learn about the infrastructure or deploy dapps.
- [Tutorial: Optimism Beginner Tutorial](https://github.com/ethereum-optimism/optimism-tutorial/blob/main/README.md){target=\_blank}
- [Article: Results of Optimism Smart Contract Audit by OpenZeppelin](https://blog.openzeppelin.com/optimism-smart-contracts-audit/){target=\_blank}
