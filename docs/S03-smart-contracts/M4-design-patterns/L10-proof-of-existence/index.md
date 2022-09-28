# Writing a Smart Contract (Proof of Existence Exercise)

This walkthrough is based on [this Medium post](https://blog.zeppelin.solutions/the-hitchhikers-guide-to-smart-contracts-in-ethereum-848f08001f05) by Manuel Araoz.

## What is Proof of Existence?

Proof of Existence is a service that verifies the existence of a document or file at a specific time via timestamped transactions. PoE utilizes the one-way nature of cryptographic hash functions to reduce the amount of information that needs to be stored on the blockchain.

In this walkthrough, we are going to introduce some basic Ethereum smart contract development best practices by creating a simple proof of existence contract and interacting with it on the blockchain.

## Set up the Environment

### Installing NodeJS

For this example we need NodeJS installed on your machine. There are several ways to get it, but we recommend using NVM (Node Version Manager). This way we can execute `npm install -g` without needing `sudo`, which can be dangerous. 

[Here are the official instructions for all operating systems](https://github.com/nvm-sh/nvm#install--update-script).

### Connect to a Blockchain

To develop Ethereum applications, you will need a client to connect to an Ethereum blockchain. You can use [Geth](https://geth.ethereum.org/docs/getting-started), [Parity](https://www.parity.io/) or a development blockchain such as [Ganache](http://truffleframework.com/ganache/).

In this walkthrough we will be using the Ganache command line interface, `ganache`. You can find the documentation on `ganache` [here](https://github.com/trufflesuite/ganache).

You can install ganache with the following command:

    $ npm install -g ganache

And start ganache with

    $ ganache

When ganache starts, you can see that it starts with 10 accounts. Each of those accounts comes prefunded with Ether so we do not need to mine or acquire funds from a faucet.

`ganache` starts a development blockchain that needs to be running while developing the application, so leave it running while we continue working on the application.

### Truffle Development Framework

Solidity is the most popular programming language for writing smart contracts in Ethereum. We will be using Solidity throughout this course.

[The Truffle development framework](http://trufflesuite.com/) is one of the most popular development tools for writing Solidity smart contracts for Ethereum. Truffle will help us compile, deploy, and test our smart contracts once they are written.

To install truffle

    $ npm install -g truffle

<span style="background-color: rgb(209, 213, 216);">`$ npm install -g @truffle/hdwallet-provider`</span>

Create a project directory and set up truffle

    $ mkdir proof-of-existence
    $ cd proof-of-existence/
    $ truffle init

Truffle sets up a contracts directory where we will write our contracts, a migrations directory where we will write scripts to deploy our contracts, and a test directory where we will write tests to make sure that our contracts work as expected.

In `truffle-config.js` we need to specify the network that we will be using.

In the module.exports object, add the following information:  

_Note: This information is cooked in when we initialized truffle, head over the truffle.config.js file, and view the commented out code under networks._

    module.exports = {
        networks: {
            development: {
                host: 'localhost',
                port: 8545,
                network_id: '*'
            }
        }
    };

We use this information because `ganache` is running our development blockchain on `localhost:8545`, and this is what we want to connect to. Specifying `network_id` as `*` means that any truffle will deploy to any network running at `localhost:8545`.

## Writing the Smart Contract

Run the following command in the terminal in your project directory:

    $ truffle create contract ProofOfExistence1

This command will create a Solidity file in the contracts directory called `ProofOfExistence1.sol` and set up the boilerplate code for the contract, a contract definition, and a contract constructor. Open `ProofOfExistence.sol` in your text editor.

Update your `ProofOfExistence1.sol` file so that it looks like [this](https://github.com/ConsenSys-Academy/proof-of-existence-exercise/blob/master/contracts/ProofOfExistence1.sol).

We are starting with something simple, and we are going to work towards a more complex contract.

Our contract has a state and two functions. This contract actually has two different kinds of functions, a transactional function `notarize` and a read-only, or `view`, function `proofFor`. Transactional functions can modify state whereas read-only functions can only read the state and return values.

Let’s deploy this contract to our test network.

Create a new migrations file in the migrations directory called `1_deploy_contracts.js`. In this file add the following:

    const ProofOfExistence1 = artifacts.require('ProofOfExistence1.sol');

    module.exports = function(deployer) {
        deployer.deploy(ProofOfExistence1);
    };

This script tells Truffle to get the contract information from `ProofOfExitence.sol` and deploy it to the specified network. Now we just need to tell Truffle to run the deployment.

Run the following command in the terminal in your project directory:

    $ truffle migrate

In the terminal output you should see that Truffle compiled `ProofOfExistence.sol`. Then, it runs the migrations using the network ‘development’ that we specified in truffle-config.js.

Truffle remembers which contracts it has migrated to the network. So, if the contract has not changed and we want to run the migration again on the same network, we need to use the `--reset` option like so:

    $ truffle migrate --reset

You can find more information about truffle migrations [here](https://truffleframework.com/docs/truffle/getting-started/running-migrations).

## Interacting with your Smart Contract

Our contract is now on the development blockchain, so we can interact with it. We can read the contract state from the blockchain and update the state by calling the notarize function. We can do this using the Truffle console.

Bring up the truffle console with the command:

    $ truffle console

You should see

    truffle(development)>

On the first line enter:

    const poe = await ProofOfExistence1.deployed()

This line says that the variable `poe` is an instance of our deployed `ProofOfExistence1.sol`.

You can see the address by entering

    truffle(development)> poe.address
    '0xc490df1850010ea8146c1dd3e961fedbf6b85bef'

To call the notarize function, we call it like any other javascript function.

    truffle(development)> await poe.notarize('Hello World!')
    { tx: '0x60ae...2643cbea65',
      receipt: …
    }

This function causes a state change, so it is a transactional function. Transactional functions return a Promise that resolves to a transaction object.

We can get the proof for the string with

    truffle(development)> poe.proofFor('Hello World!')
    ‘0x7f83b...126d9069’

And check that the contract’s state was correctly changed

    truffle(development)> poe.proof()
    '0x7f83b...126d9069'

The hashes match!

## Iterating on the code

Our contract works! But it can only store one proof at a time. Let’s change that.

Exit the Truffle console and create a new file called ProofOfExistence2.sol:

    truffle(development)> .exit
    $ truffle create contract ProofOfExistence2

Update the ProofOfExistence2 contract to match [this contract](https://github.com/ConsenSys-Academy/proof-of-existence-exercise/blob/master/contracts/ProofOfExistence2.sol).

The main changes between the first version and this version are that we changed the `proof` variable to a bytes32 array called `proofs` and made it private. We also added a function called `hasProof` to check if a proof has already been stored in the array.

Update the migration script `1_deploy_contracts.js` to deploy the new contract and deploy it to the development blockchain.

    const ProofOfExistence2 = artifacts.require('ProofOfExistence2.sol');

    module.exports = function(deployer) {
        deployer.deploy(ProofOfExistence2);
    };

Then, migrate the contracts:

    $ truffle migrate

Launch the console to interact with the new contract.

    $ truffle console

Save the deployed contract

    truffle(development)> const poe = await ProofOfExistence2.at(ProofOfExistence2.address)

We can check for a proof.

    truffle(development)> poe.checkDocument('Hello World!')
    false

It returns false because we haven’t added anything yet. Let’s do that now.

    truffle(development)> await poe.notarize('Hello World!')
    { tx: '0xd6f72...10a6e',
      receipt: 
       { transactionHash: ...
      logs: [] }

    truffle(development)> poe.checkDocument('Hello World!')
    true

We can check to make sure that our contract will store multiple proofs.

    truffle(development)> await poe.notarize('Hello Consensys!')
    { tx: '0x8b566...091ace',
      receipt: 
       { transactionHash: ...
      logs: [] }

    truffle(development)> poe.checkDocument('Hello Consensys!')
    True

Looping over arrays in smart contracts can get expensive as arrays get longer. Using a mapping is a better solution.

Let’s create a final version in `ProofOfExistence3.sol` using mappings. You can use [this code](https://github.com/ConsenSys-Academy/proof-of-existence-exercise/blob/master/contracts/ProofOfExistence3.sol) for the contract.

Modify the deployment script to deploy the new contract and test it in the console to make sure that it behaves just like `ProofOfExistence3.sol`.

## Deploying to the Testnet

From here, we are going to deviate from the Zeppelin Solutions walkthrough. If you want to learn how to deploy contracts using the geth console (which requires syncing with the testnet), you can consult the Zeppelin Solutions walkthrough.

The first step in our alternate deployment method is to get an Ethereum account on Metamask. On the landing page, click “Get Chrome Extension.”

Once the extension is installed, accept the terms of use and enter a password for your account.

You will be shown 12 words that can be used to restore your wallet. A word of caution, do **NOT** publish these words anywhere public. Anyone that has these 12 words has access to your wallet.  

Now, you have two ways to deploy to a testnet: via a `.env` file or with Truffle dashboard!

Deploying the contract requires us to make a transaction on the testnet, so we need some ether to pay for the transaction. You can get free Goerli ether by going to [this website](https://goerli-faucet.mudit.blog/) and following the instructions. Make sure you enter the Ethereum address for your 1st Metamask account.

Now that we have a testnet account with Ether, we need to configure Truffle to be able to deploy the contract.

### Deploy with Truffle Dashboard

Our recommended way of deploying contracts is through Truffle dashboard, which allows you to deploy contracts and sign transactions using your MetaMask wallet! You can watch a walkthrough on YouTube!

<iframe width="560" height="315" src="https://www.youtube.com/embed/AnprU4z-q0k" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

To deploy via dashboard, call `truffle dashboard` in another terminal. This should open up the dashboard on `localhost:24012`. Make sure you are connected to the Goerli network on your MetaMask wallet.

Then, to migrate, call `truffle migrate --network dashboard`. A prompt to sign the transaction should show up in your dashboard view. Click confirm to deploy!

### Deploy using `.env`

To deploy automatically without having to accept a transaction in dashboard, you'll need to put your 12 word private key from MetaMask into a separate `.env` file.

Additionally, to deploy contracts to the testnet without having to sync a local node, you can use Infura. Infura allows you to access a fully synced Ethereum node via their API. We will use their API to deploy our contracts to the Goerli testnet.

Go to the [Infura website](https://infura.io/) and sign up for a free account and create a project. Then, get the API key - this will be your project id.

Create a `.env` file in your directory and add your private key and project id as follows:

    MNEMONIC =<Your 12 phrase mnemonic>
    PROJECT_ID =<Your Infura project id>

Then, uncomment lines 44-47

    require('dotenv').config();
    const { MNEMONIC, PROJECT_ID } = process.env;

    const HDWalletProvider = require('@truffle/hdwallet-provider');

For Truffle to derive our ethereum address from the mnemonic, we need to install the Truffle HD wallet provider and dotenv. In the terminal located in the proof-of-existence project root run:

    npm i @truffle/hdwallet-provider
    npm i --save-dev dotenv

Then, uncomment lines 85 - 91:

    goerli: {
        provider: () => new HDWalletProvider(MNEMONIC, `https://goerli.infura.io/v3/${PROJECT_ID}`),
        network_id: 5,       // Goerli's id
        confirmations: 2,    // # of confirmations to wait between deployments. (default: 0)
        timeoutBlocks: 200,  // # of blocks before a deployment times out  (minimum/default: 50)
        skipDryRun: true     // Skip dry run before migrations? (default: false for public nets )
    },

Now, all you need to do is specify the `goerli` network to migrate!

    $ truffle migrate --network goerli

The terminal prints the addresses of the deployed contract as well as the transaction hashes of the deployment transactions. This information can also be referenced in the contract artifacts, which are stored in proof-of-existence/build/contracts/. Deployment information is found at the bottom of each JSON file. If you have the Truffle VS Code extension installed, you can see the build files in the Truffle VS Code view.

You can view your deployed contracts at [https://goerli.etherscan.io/](https://goerli.etherscan.io/). Paste in the deployed contract address to have a look you yourself, you can now interact with the deployed contract on the Goerli test network!
