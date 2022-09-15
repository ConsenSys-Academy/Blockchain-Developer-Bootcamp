This lesson is meant to directly follow the previous lesson. If you have not gone through that lesson yet, please go back and do that one first to avoid confusion and potential errors.

In this lesson we are going to use web3.js in the browser console again. This time to connect to a SimpleStorage.sol contract that is deployed on the Rinkeby testnet. You can view the code for the contract [on GitHub here](https://gist.github.com/ConsenSys-Academy/6d93a805ce0e90d8a793a4eb6e69b4c5) and on [etherscan here](https://rinkeby.etherscan.io/address/0x49bb098e781ed5c50d85e82d85cba1a6f03fd3e6#code).

## Connect to the network and load Web3.js

First, make sure that Metamask is connected to the Rinkeby network.

Next, we'll have to add the Web3.js library to this site. Since MetaMask does not inject it anymore, let's add it ourselves using the following steps (from last tutorial, but we need to redo it because we changed pages!):

1. Open your browser's developer console. [See this article for how to do it](https://support.happyfox.com/kb/article/882-accessing-the-browser-console-and-network-logs/){target=_blank} for major browsers in each major operating system.
2. In the Console, add the following series of Javascript code. Press enter after each line of code:

```
var script = document.createElement('script');
script.type = 'text/javascript';
script.src = 'script.js';
script.src = 'https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js';
document.head.appendChild(script);
```

## Connect MetaMask

Again, we need to connect our `web3` object to our MetaMask account. We do that by running the following commands:

```
web3 = new Web3(window.ethereum)
```

## Initialize the contract

Before we can interact with the contract, we need to initialize an instance of the SimpleStorage contract using web3.js. In this step we are going to provide web3.js with the ABI and the contract address, so it knows what functions are available at the address that we provide. The SimpleStorage.sol contract is deployed at address 0x49Bb098E781eD5C50D85E82d85cbA1a6F03FD3e6.   

Let's set the address in the console: 

<pre>const SSaddress = "0x49Bb098E781eD5C50D85E82d85cbA1a6F03FD3e6"</pre>

Let's set the ABI in the console with:

<pre>const ABI = [
        {
                "constant": false,
                "inputs": [
                        {
                                "internalType": "uint256",
                                "name": "x",
                                "type": "uint256"
                        }
                ],
                "name": "set",
                "outputs": [],
                "payable": false,
                "stateMutability": "nonpayable",
                "type": "function"
        },
        {
                "anonymous": false,
                "inputs": [
                        {
                                "indexed": false,
                                "internalType": "uint256",
                                "name": "newValue",
                                "type": "uint256"
                        },
                        {
                                "indexed": false,
                                "internalType": "address",
                                "name": "updatedBy",
                                "type": "address"
                        }
                ],
                "name": "storageUpdate",
                "type": "event"
        },
        {
                "constant": true,
                "inputs": [],
                "name": "get",
                "outputs": [
                        {
                                "internalType": "uint256",
                                "name": "",
                                "type": "uint256"
                        }
                ],
                "payable": false,
                "stateMutability": "view",
                "type": "function"
        }
]</pre>

To create a new contract instance we run `const simpleStorage = new web3.eth.Contract(ABI, SSaddress)`.

We can see that the simpleStorage contract object now has events, methods and an address that we provided with the ABI and contract address. We just need to set the web3 provider for the contract, which we can do with `simpleStorage.setProvider(web3.givenProvider)`. Now we can use this contract object to interact with the deployed contract.

![](https://files.cdn.thinkific.com/file_uploads/205430/images/c20/2ce/faf/1595392171288.jpg)

You will need some Rinkeby ETH to pay for gas to interact with the contract. You can get some via this link: [https://www.rinkeby.io/#faucet](https://www.rinkeby.io/#faucet).

## Read the contract state

Let's read the current value of the storedData. Since our contract object is saved as simpleStorage, run `simpleStorage.methods.get().call().then(console.log)`. This will print the current storedData value of the contract. Since this is just reading the contract, there is no transaction sent to the network and there is no cost associated with this action.

## Update the contract state

We update the contract by sending it a transaction to the "set()" function with the desired parameter. This action does cost gas, since we need to update the state of the contract on all of the network nodes. Feel free to update the value to whatever you want. `simpleStorage.methods.set(SET_YOUR_NEW_NUMBER_HERE).send({from: web3.givenProvider.selectedAddress})`

Running this code should trigger Metamask to ask you to sign a transaction. 

Once the transaction is mined, you can check for the transaction with simpleStorage.methods.get().call().then(console.log) or you can check the contract on a Rinkeby block explorer [like the one here.](https://rinkeby.etherscan.io/address/0x49bb098e781ed5c50d85e82d85cba1a6f03fd3e6){target=_blank}

## Watch for events

You can easily subscribe to events with simpleStorage. Notice we have a "storageUpdate" event in the contract.

To listen for that event, run `simpleStorage.events.storageUpdate(function(error, event){console.log(event)})`

[Here is a link to the relevant web3.js documentation for subscribing to events.](https://web3js.readthedocs.io/en/v1.2.11/web3-eth-contract.html#events){target=_blank}

To trigger this event, you will have to call the "set()" function on the contract again. Once the update transaction is mined, the event will fire. This is what it looks like in the browser console.

![](https://files.cdn.thinkific.com/file_uploads/205430/images/964/e04/26d/1595392170831.jpg)

This should give you a good overview of how to connect to a contract and interact with it using web3.js
