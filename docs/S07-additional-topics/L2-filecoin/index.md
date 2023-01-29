# Filecoin

[Protocol Labs](https://protocol.ai/){target=\_blank}, who built [IPFS](https://ipfs.tech/){target=\_blank}, have developed an entire network for decentralized filesharing called Filecoin. In this section, we'll go through a [Truffle Box](https://trufflesuite.com/boxes/){target=\_blank} which sets up a Filecoin environment on your computer.

The context of the box is that of a decentralized art gallery. It comprises both Lotus and IPFS nodes (simulating the process of creating a storage deal), an Ethereum node (for the deployment of the [OpenZeppelin-based ERC-721](https://docs.openzeppelin.com/contracts/4.x/){target=\_blank} based NFT contracts) and a front-end for viewing the gallery and the decentrally stored assets.

## Using the Filecoin Truffle Box

This guide uses an pre-existing project to provide the base Truffle project structure and example contracts.
In your workspace directory, run the following commands:

```bash
mkdir filecoin-example
cd filecoin-example
truffle unbox filecoin
```

## Environment Setup

The following steps guide you through getting the Filecoin environment set up on your computer.

### Running Filecoin-flavored Ganache

The easiest way to run a Filecoin environment locally is via [Filecoin-flavored Ganache](https://github.com/trufflesuite/ganache-ui/releases/tag/v2.6.0-beta.3){target=\_blank} (which runs both a local IPFS and Lotus node). To download, select the appropriate build for your OS from the **Assets** list at the bottom of the [release page](https://github.com/trufflesuite/ganache-ui/releases/tag/v2.6.0-beta.3#user-content-2.6.0-beta.3-How-to-Upgrade){target=\_blank}.

This creates 10 accounts, each loaded with 100 FIL, and displays both their account addresses and associated private keys (which can be accessed by clicking on the key icon on the right-hand side).

![Ganache GUI](../../img/S07/ganache-1.png)

It also starts the Lotus and IPFS daemons running over `http` and `ws` respectively:

```bash
Lotus RPC listening on 127.0.0.1:7777
IPFS  RPC listening on 127.0.0.1:5001
```

### Running the Filecoin Network Explorer

The following steps guide you through setting up Filecoin Network Inspector utility which enables you to upload files to the IPFS node and create a Filecoin storage deal.

```bash
git clone https://github.com/trufflesuite/filecoin-network-inspector
cd filecoin-network-inspector
git checkout ganache-changes
npm install
npm run start
```

### Running Ethereum Ganache

The following command starts a local [Ganache](https://trufflesuite.com/ganache/){target=\_blank} instance that we'll be deploying our smart contracts to:

```bash
npx ganache
```

Awesome! All going well you've now got your environment setup and ready to simulate creating your first storage deal.

## Creating Storage Deals

A storage deal is an agreement between a client and a storage miner to store some data in the network for a given duration. Note that while in the case of Filecoin's mainnet, a deal must be secured with a miner before data is stored, in Filecoin Ganache a deal is reached automatically. Via the Filecoin Network Explorer:

1. Open the Filecoin Network Explorer and navigate to the "Market" tab
1. Select a file by clicking "Choose File" followed by "Upload to the Filecoin Network"
1. Optionally add all the files from the `/assets` directory (note that these are already on IPFS so the application still work if you don't do this step)

As you add files, if you open Ganache, you should see both the files themselves (under the Files tab) and the accompanying storage deals (under the Deals tab) show up. This is of course just a simulation of the process, but it's a good way to get a feel for how it works. More information on storage and retrieval deals can be found in the [Filecoin Docs](https://filecoin.io/blog/posts/how-storage-and-retrieval-deals-work-on-filecoin/){target=\_blank}.

## Minting an NFT

In the example below, we've already created a deal for the 3 assets (metadata, thumbnail, and the original asset respectively) that comprise our NFT. These are as follows, with their corresponding CIDs.

- metadata [QmS4t7rFPxaaNriXvCmALr5GYRAtya5urrDaZgkfHutdCG](https://ipfs.io/ipfs/QmUWFZQrJHfCVNHXVjjb2zeowVvH7dC6rKpbdHsTdnAgvP){target=\_blank}
- thumbnail [QmbAAMaGWpiSgmMWYTRtGsru382j6qTVQ4FDKX2cRTRso6](https://ipfs.io/ipfs/QmbAAMaGWpiSgmMWYTRtGsru382j6qTVQ4FDKX2cRTRso6){target=\_blank}
- asset - [QmbAAMaGWpiSgmMWYTRtGsru382j6qTVQ4FDKX2cRTRso6](https://ipfs.io/ipfs/QmS4t7rFPxaaNriXvCmALr5GYRAtya5urrDaZgkfHutdCG){target=\_blank}

Assuming the local Ethereum Ganache node is running, you'll be able to open a console and mint a new NFT with the following steps. As the base URL is set to that of an IPFS gateway, we'll just need to pass in the CID to the asset metadata.

```bash
truffle migrate
truffle console
truffle(development)> const gallery = await MyGallery.deployed()
truffle(development)> gallery.mint(accounts[0], "QmS4t7rFPxaaNriXvCmALr5GYRAtya5urrDaZgkfHutdCG")
```

In the above example the owner of the NFT is set (via `accounts[0]`) to that of the first account generated by the mnemonic. If we want to transfer it to a new owner, we'll be able to do so with the following.
Transferring Ownership

```bash
truffle console
truffle(development)> gallery.transferFrom(accounts[0], accounts[1], 1)
```

## Gallery UI

A sample gallery interface is provided as a means of viewing all the assets (and their associated deals) you've just uploaded. Use the following steps to run this locally:

```bash
cd ui
npm install
npm run start
```

![Ganache GUI](../../img/S07/gallery-1.png)

All going well, you should now be able to view the gallery at [http://localhost:3000](http://localhost:3000){target=\_blank}.
