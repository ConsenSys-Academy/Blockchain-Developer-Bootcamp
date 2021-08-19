There are a variety of common JavaScript libraries that you can use to connect to Ethereum. Many of the libraries serve the same purpose and have the same functionality, but the syntax differs for each.

The purpose of this lesson is to show the similarities and differences between the libraries so you gain a better understanding of what these libraries do a general level and how each one does it.

If you are using the Brave browser, you may encounter conflicts with the built-in Ethereum wallet and Metamask. If this happens, try using a different browser with Metamask installed.

## Truffle

Truffle is the framework that we have covered in the most depth so far in the course. Truffle will connect to a running blockchain specified in the truffle-config.js file, manage deployments via migration scripts and information stored in the truffle artifacts and abstracts away much of the complexity of interacting with contracts (via [contract abstractions](https://trufflesuite.com/docs/truffle/reference/contract-abstractions)).

Other libraries handle these in different ways and have different APIs that are useful to review.

## Web3.js

Web3.js is one of the most popular JavaScript libraries in Ethereum dApp development. Unfortunately there are two versions of web3.js in use right now. Web3.js 1.x is in development, [you can visit the documentation for 1.x here](https://web3js.readthedocs.io/en/1.0/). The latest stable version at the time of this writing is web3.js 0.2x.x, and [you can see those docs here](https://github.com/ethereum/web3.js/blob/0.20.7/DOCUMENTATION.md). As you can see, the APIs for these versions are different, so pay attention to which version you are using.

Web3.js is the library that is injected by Metamask. If you have Metamask installed in your browser, you can see the web3 object by opening your browser developer tools (ctrl shift i in Chrome) and typing web3 in the console. As you go through this workshop, if you encounter problems, try refreshing your browser and repeating the necessary steps.

![](https://files.cdn.thinkific.com/file_uploads/205430/images/f17/ef7/eb7/1595392058270.jpg)

You can see the current version is "0.20.x", in the "version" property of the web3 object. This web3 object is connected to the Ethereum network through a service provided by Metamask. Metamask uses [Infura infrastructure](https://infura.io/) as the gateway to  Ethereum.

We have included a version of the newer web3.js API in the page as well, so by entering `web3 = new Web3(web3.currentProvider)` in the browser console, you can get an instance of the web3.js version 1.x. For the remainder of this lesson, we will be using the [web3.js v1.x beta API](https://web3js.readthedocs.io/).

![](https://files.cdn.thinkific.com/file_uploads/205430/images/fbf/90b/f00/1595392058818.jpg)

### A Side note about Metamask

If you are following along in your browser, you will also see that in the "currentProvider" property, the "selectedAddress" is undefined or null. Metamask does not provide access to the account address by default. If you type `ethereum.enable()` in the console, Metamask will pop open asking you if you'd like to connect.

Connecting will make this account information accessible to the current page.

![](https://files.cdn.thinkific.com/file_uploads/205430/images/3a9/4c5/3f8/1595392059315.jpg)

Connect to Ganache GUI

Let's connect to Ganache GUI and send a transaction via the API in the console. Start [Ganache GUI](https://truffleframework.com/docs/ganache/overview) and connect Metamask (Ganache GUI defaults to port 7545). Use the Ganache GUI "Quickstart" option to follow along with the same account addresses that I use in this explanation. To connect to Ganache GUI, click "Custom RPC" in the Network drop down and then enter the network information.

     ![](https://files.cdn.thinkific.com/file_uploads/205430/images/8f5/d67/387/1595392057199.jpg)              ![](https://files.cdn.thinkific.com/file_uploads/205430/images/f10/099/f6c/1595392059118.jpg)

You can easily import Ganache GUI accounts into Metamask by importing via the private key. Click the key icon on the right side of Ganache GUI to get the associated account private key. To import the account into Metamask, select "Import Account" in the Metamask accounts dropdown, and paste in the private key.

![](https://files.cdn.thinkific.com/file_uploads/205430/images/b32/51d/630/1595392067077.jpg)                ![](https://files.cdn.thinkific.com/file_uploads/205430/images/ba1/88e/3a1/1595392059006.jpg)

### Checking the account

Once you are connected to Ganache GUI through Metamask, you can send transactions on the Ganache GUI network through the injected web3 object in the browser console. Typing `web3.currentProvider.selectedAddress` should return your current account address.

# ![](https://files.cdn.thinkific.com/file_uploads/205430/images/1bc/2e0/b89/1595392059501.jpg)

### Sending a Transaction

Use the following code snippet as your transaction information.

<pre>var transaction = {
from: web3.currentProvider.selectedAddress,
to: "0xce573835eB9ca38454f97D103Ca46b7e8aDF617f",
value: web3.utils.toWei("1", "ether")
}</pre>

Th "to" account is the second account that is generated by the Quickstart in Ganache GUI.

In the console, it look like this:

![](https://files.cdn.thinkific.com/file_uploads/205430/images/139/18a/245/1595392060307.jpg)

Now sending a transaction is as easy as entering `web3.eth.sendTransaction(transaction)` in the console and Metamask will pop up, asking you to sign the transaction. If you get an error, you may need to reset the web3 provider. You can do that with this line of code `web3.setProvider(web3.currentProvider)`.

![](https://files.cdn.thinkific.com/file_uploads/205430/images/9b8/1ea/5f4/1595392060592.jpg)

### Nonce Mismatch Errors

If you use Metamask accounts on different development blockchains, the nonce counts may get out of sync, in which case you will see an error when trying to execute a transaction. Metamask tracks the account nonce independently so this can get out of sync with the account nonce on the blockchain network that you are trying to interact with.

![](https://files.cdn.thinkific.com/file_uploads/205430/images/093/061/1f9/1595392063094.jpg)

If this happens, it is a simple fix. Open Metamask and click the account icon on the upper right and select "Settings". In the "Advanced" area, select "Reset Account". 

![](https://files.cdn.thinkific.com/file_uploads/205430/images/6e5/703/5bf/1595392061452.jpg)                     ![](https://files.cdn.thinkific.com/file_uploads/205430/images/e7a/aaa/8c7/1595392061366.jpg)

If you were seeing this error, reset your account and try sending the transaction again. Metamask will get the correct account nonce from the blockchain network. When the transaction succeeds, you should see the new account balances reflected on Ganache GUI.

You can check the balance of these accounts with the line `await web3.eth.getBalance(address)` where address is any Ethereum address. Try it with "`await web3.eth.getBalance(web3.currentProvider.selectedAddress)`".

This is just a quick intro to sending transaction with web3.js v1.0\. You can learn more about how to use it via the docs and specifically about [how to connect to a contract via this section.](https://web3js.readthedocs.io/en/1.0/web3-eth-contract.html#web3-eth-contract) 

Keep in mind that this library is still in development, so if you run into any bugs, please report them!

## Ethers.js

Let's try connecting to a different library. [The ethers.js library](https://docs.ethers.io/v5/) is also included on this page and is accessible via the browser JavaScript console. We will continue to use Metamask as the account signer for the accounts on the development blockchain.

### Connect to the Web 3 provider

In the browser console, you can connect ethers.js to the current network by accessing the provider given by Metamask, then set it is as the "signer". Metamask injects the provider as "web3.currentProvider", but since we changed the web3 object to use web3.js v1.0, the provider is accessible at "web3.givenProvider".

<pre>// MetaMask injects a Web3 Provider as "web3.currentProvider", so
// we can wrap it up in the ethers.js Web3Provider, which wraps a
// Web3 Provider and exposes the ethers.js Provider API.

const provider = new ethers.providers.Web3Provider(web3.currentProvider);

// There is only ever up to one account in MetaMask exposed
const signer = provider.getSigner();</pre>

Now that Metamask is set as the signer, you can send a transaction. [Check the "signer" API of ethers.js to see how to send a transaction.](https://docs.ethers.io/v5/api/signer/#Signer) Something like "signer.sendTransaction(transaction)" should work, but what does a transaction look like in ethers.js?

<pre>{
    // Required unless deploying a contract (in which case omit)
    to: addressOrName,  // the target address or ENS name

    // These are optional/meaningless for call and estimateGas
    nonce: 0,           // the transaction nonce
    gasLimit: 0,        // the maximum gas this transaction may spend
    gasPrice: 0,        // the price (in wei) per unit of gas

    // These are always optional (but for call, data is usually specified)
    data: "0x",         // extra data for the transaction, or input for call
    value: 0,           // the amount (in wei) this transaction is sending
    chainId: 3          // the network ID; usually added by a signer
}</pre>

[You can check the docs here.](https://docs.ethers.io/v5/api/providers/types/#providers-TransactionRequest)

For a simple ether transfer, you can get away with:

<pre>var transaction = {
    to: "0xce573835eB9ca38454f97D103Ca46b7e8aDF617f",
    value: ethers.utils.parseEther("1")
}</pre>

And to send it, enter  `signer.sendTransaction(transaction)` in the browser console.  

![](https://files.cdn.thinkific.com/file_uploads/205430/images/298/fe3/19b/1595392061279.jpg)

Confirm the transaction and verify that the account balances have changed in Ganache GUI.

[Please explore the Ether.js documentation to see all of the things that it can do.](https://docs.ethers.io/v5/api/)

## Summary

As a developer, you can use different JavaScript libraries to interact with Ethereum blockchains. Many of the JavaScript libraries do many of the same things, but they may handle transaction signers or providers differently or have different ways of connecting to contracts and listening to events. The library you choose is primarily a matter of personal preference.  
We focus on using web3.js in this course, but introduce ethers.js because it is a popular alternative.

## Additional Material
- <a href="https://blog.infura.io/ethereum-javascript-libraries-web3-js-vs-ethers-js-part-i/" target="_blank" rel="noopener noreferrer">Article: Web3 vs ethers Part I</a> and <a href="https://blog.infura.io/ethereum-javascript-libraries-web3-js-vs-ethers-js-part-ii/" target="_blank" rel="noopener noreferrer">Part II</a> by Academy's own Tom Hay and Robbie K.
- <a href="https://www.chainshot.com/learn/ethers" target="_blank" rel="noopener noreferrer">Course: Learn Ethers.js (Chainshot)</a> Use Chainshot's excellent interactive interface to learn more about ethers.js