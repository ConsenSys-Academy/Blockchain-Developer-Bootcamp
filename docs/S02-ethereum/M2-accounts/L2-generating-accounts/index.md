Generating Ethereum accounts in JavaScript
==========================================

Public key cryptography and digital signatures are a foundational technology that enable blockchains to work. In this project you are going to get your hands dirty and understand how they work at the code level. You will be using JavaScript and a simple web interface to see what is going on.

Generate Private Key
--------------------

First, we are going to generate a private key, derive public keys from the private key and determine the associated accounts. To get started [clone the project](https://github.com/ConsenSys-Academy/ethereum-address-generator-js){target=_blank} and run:

```
$ npm install
$ npm run watch # this will watch for updates in main.js and update bundle.js`
$ npm run reload # this will serve the app @ localhost:8081 and refresh the page when there are updates
```

(If you run into any problems while implementing this demo application, try opening the developer tools in the browser (Ctrl + Shift + I or F12) and checking the "Console" tab.)

In the main.js file include the [bip39 package](https://www.npmjs.com/package/bip39){target=_blank}. We will use this to generate random input to generate a private key.

`const BIP39 = require("bip39")` and directly below that include: 
```
// Generate a random mnemonic (uses crypto.randomBytes under the hood), defaults to 128-bits of entropy  
function generateMnemonic(){  
  return BIP39.generateMnemonic()  
}
```
Note: Not all strings of characters are valid mneomics for generating keys. You can check if a mnemonic is valid by running: 

```
var isValid = BIP39.validateMnemonic("Enter your mnemonic here")  
// This will return false because "Enter your mneomnic here" is not a valid phrase
```

With this mnemonic, you can generate a seed from which to generate a private key. Add the following line to `main.js`: 
 
```
    function generateSeed(mnemonic){      
      return BIP39.mnemonicToSeed(mnemonic)    
    }  
```
Generate a Public / Private Keypair
-----------------------------------

Using this mnemonic as a source of randomness, you can now create signing keypair.

To generate a private key from the hex seed, we will to use the [ethereumjs-wallet library](https://github.com/ethereumjs/ethereumjs-wallet){target=_blank}

 
```
const hdkey = require("ethereumjs-wallet/hdkey")  
```

***Explore a much more robust address derivation application at [iancoleman.io](https://iancoleman.io/bip39/){target=_blank}*** 
 
```
function generatePrivKey(mnemonic){  
    const seed = generateSeed(mnemonic)  
    return hdkey.fromMasterSeed(seed).derivePath(`m/44'/60'/0'/0/0`).getWallet().getPrivateKey()  
}
```

With the private key, we can generate the public key. Import the `ethereumjs` wallet and derive the public key
 
```
const Wallet = require('ethereumjs-wallet')    
  ...        
  function derivePubKey(privKey){        
    const wallet = Wallet.fromPrivateKey(privKey)            
    return wallet.getPublicKey()    
  }
```
Generating the private key and public key is the same for both Bitcoin and Ethereum as both use [secp256k1 elliptic curve cryptography](https://en.bitcoin.it/wiki/Secp256k1){target=_blank}. Deriving an account address from the public key differs slightly.

 Derive the Ethereum Address From the Keypair
--------------------------------------------

Deriving an Ethereum address from a public key requires an additional hashing algorithm. Import it like so:

```
const keccak256 = require('js-sha3').keccak256;
```

Taking the `keccak-256` hash of the public key will return 32 bytes which you need to trim down to the last 20 bytes (40 characters in hex) to get the address
 
```
function deriveEthAddress(pubKey){    
  const address = keccak256(pubKey) // keccak256 hash of  publicKey    
  // Get the last 20 bytes of the public key    
  return "0x" + address.substring(address.length - 40, address.length)    
}
```
You can check this mnemonic, private key and address against [myetherwallet](https://www.myetherwallet.com/#view-wallet-info){target=_blank}. Select restore from mnemonic or private key and verify that the derived address matches the one in this app.

Creating a Digital Signature With Your Key
------------------------------------------

Using this private key we can sign transactions from this address and broadcast them to the network.

Nodes that are verifying transactions in the network will use the signature to determine the address of the signatory, cryptographically verifying that every transaction from this account is coming from someone who has access to the corresponding private key.

You can sign transactions in the browser with the [ethereumjs-tx library](https://github.com/ethereumjs/ethereumjs-tx){target=_blank}.

```
const EthereumTx = require('ethereumjs-tx')    
...  
 
function signTx(privKey, txData){  
    const tx = new EthereumTx(txData)  
    tx.sign(privKey)  
    return tx  
}
```
Unsigned Ethereum transactions look something like this:

```
{  
  nonce: '0x00',  
  gasPrice: '0x09184e72a000',  
  gasLimit: '0x2710',  
  to: '0x31c1c0fec59ceb9cbe6ec474c31c1dc5b66555b6',   
  value: '0x10',   
  data: '0x7f7465737432000000000000000000000000000000000000000000000000000000600057',  
  chainId: 3
}
```
And a signed transaction looks something like this:

```
{   
  nonce: '0x00',   
  gasPrice: '0x09184e72a000',   
  gasLimit: '0x2710',   
  to: '0x31c1c0fec59ceb9cbe6ec474c31c1dc5b66555b6',   
  value: '0x00',   
  data: '0x7f7465737432000000000000000000000000000000000000000000000000000000600057',   
  v: '0x29',   
  r: '0xb934fbdb16fda944ddc0cb33e64344b90fbd25564444832f7f8d697512069402',  
  s: '0x29' 
}
```
Notice the main difference is the inclusion of the variables `v`, `r` and `s`. These variables are used to recover the address corresponding to the key that signed the transaction. This signed transaction is broadcast to the network to be included in a block. You can read more about these variables in [this excellent article here.](https://medium.com/mycrypto/the-magic-of-digital-signatures-on-ethereum-98fe184dc9c7){target=_blank}

You can recover the sender address from the signed transaction with the following method:

```
function getSignerAddress(signedTx){  
  return "0x" + signedTx.getSenderAddress().toString('hex')
}
```
That's it! You've successfully generated a private, public keypair and then used that to derive a valid Ethereum address. You've also then created the world's tiniest crypto-wallet using `signTx()` function and seen how you can recover the address from a digital signature or signed transaction.

You'll very rarely have to do this kind of crypto-primitive handling. For one, it's garbage for security. But, also, there is so much tooling available to you to do these kind of operations safely and efficiently at scale. For learning purposes, however, nothing beats coding this stuff on its own!

 Additional links:
-----------------

* [Understanding the concept of private keys, public keys and addresses in Ethereum](https://etherworld.co/2017/11/17/understanding-the-concept-of-private-key-public-key-and-address-in-ethereum-blockchain/){target=_blank}
* [Bitcoin wiki on Secp256k1](https://en.bitcoin.it/wiki/Secp256k1){target=_blank}
* [Ethereum yellow paper](https://ethereum.github.io/yellowpaper/paper.pdf){target=_blank}
* [Article: The Magic of Digital Signatures (MyCrypto)](https://medium.com/mycrypto/the-magic-of-digital-signatures-on-ethereum-98fe184dc9c7){target=_blank}

 
