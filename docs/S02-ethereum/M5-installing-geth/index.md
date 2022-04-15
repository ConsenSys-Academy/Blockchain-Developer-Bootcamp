## Setting up Geth

[Geth (Go-Ethereum)](https://geth.ethereum.org/){target=_blank} is a command line interface for running a full ethereum node implemented in Go. This is your local portal to the Ethereum network. When you are running a local Ethereum node, you do not need to rely on any 3rd party service to connect to the Ethereumblockchain. This is what makes the network “trustless”.

### Capabilities

By installing and running geth, you can take part in the Ethereum live network and

1.  Mine real ether
2.  Transfer funds between addresses
3.  Create contracts and send transactions
4.  Explore block history
5.  And much more!

### Interfaces

Geth has several interfaces through which you can communicate with your Ethereum node.

*   JavaScript Console: you can start geth with an interactive console, that provides a javascript runtime environment exposing a javascript API to interact with your node. The [JavaScript Console API](https://github.com/ethereum/go-ethereum/wiki/JavaScript-Console){target=_blank} includes the web3 javascript Ðapp API as well as an 'admin' API.
*   JSON-RPC server: you can start geth with a json-rpc server that exposes the [JSON-RPC API](https://github.com/ethereum/wiki/wiki/JSON-RPC){target=_blank}
*   [Command line options](https://github.com/ethereum/go-ethereum/wiki/Command-Line-Options){target=_blank} documents command line parameters as well as subcommands.

[See this page](https://geth.ethereum.org/docs/install-and-build/installing-geth){target=_blank} for instructions on how to install geth for your platform.

Install geth and start interacting with our node.

Once you install geth, open a new terminal window and type

```
geth
```

</table>

You will see something like the following.

![](https://learn.consensys.net/images/screenshot1.png)![screenshot1.png](https://files.cdn.thinkific.com/file_uploads/205430/images/776/ae3/180/1595097113885.jpg)

Geth starts to look for and connect to peers on the Ethereum network. Once geth finds a peer, it starts syncing blockchain data, importing block headers, block receipts and state entries. You can stop the process with “Ctrl + C”.

Geth also opens an ipc endpoint through which you can connect to your node. If you type:

```
geth attach [path to the ipc endpoint]
```  

in another terminal window, the [geth javascript console](https://github.com/ethereum/go-ethereum/wiki/JavaScript-Console){target=_blank} will appear. In my case, I typed

```
geth attach ~/.ethereum/geth.ipc
```

![](https://learn.consensys.net/images/screenshot2.png)![screenshot2.png](https://files.cdn.thinkific.com/file_uploads/205430/images/582/86a/0d0/1595097114702.jpg)


if you are on Windows, you have to access the javascript console using the pipe geth created by typing the following:

```
geth attach ipc:\\.\pipe\geth.ipc
```

Or when you start geth, you can type

```
geth console
```

and geth will start with the javascript console already displayed. Geth will continue to print logs, which can be annoying when you are typing in the console. To silence the logs, enter

```
debug.verbosity(0)
```

in the console. Type exit to exit the javascript console.

Geth defaults to sync with the main network, but we can sync with any network that we want. 

### Creating an Ethereum Account

Before we launch our private blockchain, let's setup an Ethereum account on Geth. Run:

<pre>geth account new</pre>

Be sure to remember your password! You should see something like this:

![](https://files.cdn.thinkific.com/file_uploads/205430/images/f5e/417/a61/Screen_Shot_2020-09-08_at_3.50.48_PM.png)

Your account number will look different from the image. Copy the address down somewhere, we'll need it for the next step!

Repeat the step one more time to ensure you have two separate accounts.

### Creating a private blockchain

Every blockchain starts with a genesis block, the first block. To create our own blockchain, we need to specify a genesis file from which geth can create a genesis block.

Create a new file called `genesis.json` and paste in the following:

```json
{  
  "config": {  
        "chainId": 4568,  
        "homesteadBlock": 0,  
        "eip150Block": 0,  
        "eip155Block": 0,  
        "eip158Block": 0  
    },  
  "alloc"      : {},  
  "difficulty" : "0x100",  
  "extraData"  : "",  
  "gasLimit"   : "0x7A1200",  
  "parentHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",  
  "timestamp"  : "0x00"  
}
```  

So what's in this genesis file?

The **`config`** section defines the settings for the private blockchain.

The **`chainId`** identifies the blockchain. The Ethereum main net has a chainId of 1\. The Ropsten testnet has a chainId of 3, Rinkeby is 4 and Kovan is 42\. This genesis file has a chainId of 4568, hopefully nobody else is running a chain with the same chainId. We can use the same client to connect to all of the different Ethereum networks.

The Ethereum protocol has hard forked and introduced several backward-incompatible protocol changes. **`homesteadBlock`** and **`eip155/8Block`** tell `geth` in which blocks the changes start. We set these to zero.

**`alloc`** allows us to create addresses and fill the accounts with ether upon initializing the blockchain. We will leave this empty and mine ether to fill our accounts.

**`Difficulty`** indicates how difficult it will be to discover a valid hash of the block. It defines the mining target, which the clients calculate from the previous block's difficulty level and the timestamp. The higher the difficulty, the more calculations the miner will have to do to find a block (on average). This value fluctuates to maintain a target block generation time (~15 seconds in Ethereum). We keep this value low on our private chain so we can quickly find blocks so we don't have to wait.

**`extraData`** is an optional 32 byte value where we can add anything.

**`gasLimit`** is a value that sets the chain-wide limit of gas expenditure per block. We set the value to 10,000,000 as that is the current limit on the main net.

**`parentHash`** is the keccak256 hash of the parent block's header. This pointer to the parent block builds the chain of blocks.

**`timestamp`** is the output of Unix time() function at the block's creation. This parameter helps determine if the difficulty level should be changed to maintain a consistent average block time. It also allows us to verify the order of the blocks in the chain.

Then we need to initialize the geth node with the custom genesis file. In your private blockchain directory, run:

```
geth --datadir . init genesis.json
```

The last line of output in the console should say `Successfully wrote genesis state`. Now we can start the private network so we can mine blocks on the private chain.

If you're on a Mac, run:

<pre>geth --allow-insecure-unlock --datadir . --keystore ~/Library/ethereum/keystore --networkid 4568 --http --http.addr '0.0.0.0' --http.corsdomain "*" --http.port 8502 --http.api 'personal,eth,net,web3,txpool,miner' --mine --miner.etherbase=YOUR_ETHEREUM_ADDRESS_HERE

</pre>

If you're on Linux, run:

<pre>geth --allow-insecure-unlock --datadir . --keystore ~/.ethereum/keystore --networkid 4568 --http --http.addr '0.0.0.0' --http.corsdomain "*" --http.port 8502 --http.api 'personal,eth,net,web3,txpool,miner' --mine --miner.etherbase=YOUR_ETHEREUM_ADDRESS_HERE</pre>

Put the Ethereum address generated earlier instead of **YOUR_ETHEREUM_ADDRESS_HERE**. You should see something like:

![](https://learn.consensys.net/images/screenshot3.png)![screenshot3.png](https://files.cdn.thinkific.com/file_uploads/205430/images/4ee/0eb/900/Screen_Shot_2020-09-08_at_4.01.08_PM.png)

In a new terminal window, cd to the private directory and run:

<pre>geth attach geth.ipc</pre>

You should see something like this:

![](https://files.cdn.thinkific.com/file_uploads/205430/images/bec/4fb/450/Screen_Shot_2020-09-08_at_3.45.47_PM.png)

In the console, type `web3`. This will print all of the commands available via the console.

If you navigate to the `test-private-blockchain` data directory, you will see two directories, `geth` and `keystore`. `Geth` is where the blockchain data will be stored and `keystore` will hold account information. Notice that the `keystore` directory is empty.

### Check your account

You can access all of your geth accounts with `eth.accounts` and it will print them in an array.

    > eth.accounts
    ["0x1c29b7832ad2e4731d816e60f767777cbf374e15", "0x01058d7d56a216b3f1ff8f41c20ad58888424de7"]

You can check the balance of an account with the `eth.getBalance()` method and entering the account.

    > eth.getBalance(eth.accounts[0])
    0

### Mining the private chain

Since the private blockchain is maintaining consensus using proof of work, we need to mine new blocks to process transactions.

To start mining, just run `miner.start()`. Geth needs to build a DAG before the miner starts, but once it does that it will start mining blocks on the private chain. After a few blocks are mined, stop it with `miner.stop()`. [See this link](https://ethereum.stackexchange.com/questions/1993/what-actually-is-a-dag){target=_blank} for more information about what is going on when geth is creating a DAG.

Check the ether balance of you first account now. It should contain some ether. The first `geth` account will default to the coinbase, or etherbase account, which is the account to which mining rewards are sent. You can check this with `eth.coinbase`.

### Sending a transaction

Now that we have some ether in our account, we can send some to another account. For this we can use the geth console and input the `eth.sendTransaction()` method that takes a transaction object.

An ethereum transaction includes the following data:

<code>from:</code> String - The address for the sending account. Uses the web3.eth.defaultAccount property, if not specified.

<code>to:</code> String - (optional) The destination address of the message, left undefined for a contract-creation transaction.

<code>value:</code> Number|String|BigNumber - (optional) The value transferred for the transaction in Wei, also the endowment if it's a contract-creation transaction.

<code>gas:</code> Number|String|BigNumber - (optional, default: To-Be-Determined) The amount of gas to use for the transaction (unused gas is refunded).

<code>gasPrice:</code> Number|String|BigNumber - (optional, default: To-Be-Determined) The price of gas for this transaction in wei, defaults to the mean network gas price.

<code>data:</code> String - (optional) Either a byte string containing the associated data of the message, or in the case of a contract-creation transaction, the initialisation code.

<code>nonce:</code> Number - (optional) Integer of a nonce. This allows to overwrite your own pending transactions that use the same nonce.

To send some ether to another account, first create another account.

    > personal.newAccount()

Next initiate the transaction by specifying the to, the from and the value.

    > eth.sendTransaction({to: eth.accounts[1], from: eth.accounts[0], value: 100})

But this throws an error! `Error: authentication needed: password or unlock`. Geth requires that you unlock your account to send transactions from the account.

    > personal.unlockAccount(eth.accounts[0])
    Unlock account 0xabc...
    true

Now you can send a transaction from account 0.

    > eth.sendTransaction({to: eth.accounts[1], from: eth.accounts[0], value: 100})
    INFO [09-10|17:54:38.360] Setting new local account                address=0x1c29B7832aD2E4731D816E60f767777CbF374E15
    INFO [09-10|17:54:38.361] Submitted transaction                    fullhash=0xdec2391ee28a7997567e5176de995340cf09fd64dc823414f6bf763b1fd1e6ed recipient=0x01058d7d56a216B3F1FF8f41c20ad58888424dE7
    "0xdec2391ee28a7997567e5176de995340cf09fd64dc823414f6bf763b1fd1e6ed"

Check the balance of account 1.

    > eth.getBalance(eth.accounts[1])
    0

It's still zero, because we are not running the miner. Start mining to process the transaction. You can stop mining after geth creates a block.

Check the balance of account 1 again.

    > eth.getBalance(eth.accounts[1])
    100

It should say 100! You have successfully sent a transaction from one account to another over your single node Ethereum network!

## Additional Materials

- [Running Geth in `dev` Mode](https://geth.ethereum.org/docs/getting-started/dev-mode) - an optimized way to run a single node for developing locally
