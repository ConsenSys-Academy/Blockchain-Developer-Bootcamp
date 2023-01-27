# Generating Ethereum accounts in JavaScript

Public key cryptography and digital signatures are a foundational technology that enable blockchains to work. In this project you are going to get your hands dirty and understand how they work at the code level. You will be using JavaScript and a simple web interface to see what is going on.

For a refresher on keys, see [Public/Private Key Crypto](../../../S01-fundamentals/M1-cryptography/L1-pub-key-crypto/index.md) and the [additional resources](../../../S01-fundamentals/M1-cryptography/L2-pub-key-crypto-additional/index.md).

## Generate Private Key

First, we are going to generate a private key, derive public keys from the private key and determine the associated accounts. To get started [clone the project](https://github.com/ConsenSys-Academy/ethereum-address-generator-js){target=\_blank} and run:

```bash
npm install
npm audit fix --force # this will patch any vulnerabilities in outdated packages
npm run watch # this will watch for updates in main.js and update bundle.js`

# In a separate terminal/shell window in the root of the project
npm run reload # this will serve the app @ localhost:8081 and refresh the page when there are updates
```

If you run into any problems while implementing this demo application, try opening the developer tools in the browser (Ctrl + Shift + I or F12) and checking the 'Console' tab. If content doesn't refresh, terminate and restart both terminal calls (`npm run watch` and `npm run reload`)

In the main.js file include the [bip39 package](https://www.npmjs.com/package/bip39){target=\_blank}. We will use this to generate random input to generate a private key.

`const BIP39 = require("bip39")` and directly below that include:

```javascript
// Generate a random mnemonic (uses crypto.randomBytes under the hood), defaults to 128-bits of entropy
function generateMnemonic() {
  return BIP39.generateMnemonic();
}
```

Note: Not all strings of characters are valid mnemonics for generating keys. You can check if a mnemonic is valid by running:

```javascript
var isValid = BIP39.validateMnemonic("Enter your mnemonic here");
// This will return false because "Enter your mnemonic here" is not a valid phrase
```

With this mnemonic, you can generate a seed from which to generate a private key. Add the following line to `main.js`:

```javascript
function generateSeed(mnemonic) {
  return BIP39.mnemonicToSeed(mnemonic);
}
```

## Generate a Public / Private Key-pair

Using this mnemonic as a source of randomness, you can now create signing key-pair.

To generate a private key from the hex seed, we will to use the [ethereumjs-wallet library](https://github.com/ethereumjs/ethereumjs-wallet){target=\_blank}

```javascript
const hdkey = require("ethereumjs-wallet/hdkey");
```

**_Explore a much more robust address derivation application at [iancoleman.io](https://iancoleman.io/bip39/){target=\_blank}_**

```javascript
function generatePrivKey(mnemonic) {
  const seed = generateSeed(mnemonic);
  return hdkey
    .fromMasterSeed(seed)
    .derivePath(`m/44'/60'/0'/0/0`)
    .getWallet()
    .getPrivateKey();
}
```

With the private key, we can generate the public key. Import the `ethereumjs` wallet and derive the public key

```javascript
const Wallet = require('ethereumjs-wallet')
  ...
  function derivePubKey(privKey){
    const wallet = Wallet.fromPrivateKey(privKey)
    return wallet.getPublicKey()
  }
```

Generating the private key and public key is the same for both Bitcoin and Ethereum as both use [secp256k1 elliptic curve cryptography](https://en.bitcoin.it/wiki/Secp256k1){target=\_blank}. Deriving an account address from the public key differs slightly.

## Derive the Ethereum Address From the Keypair

Deriving an Ethereum address from a public key requires an additional hashing algorithm. Import it like so:

```javascript
const keccak256 = require("js-sha3").keccak256;
```

Taking the `keccak-256` hash of the public key will return 32 bytes which you need to trim down to the last 20 bytes (40 characters in hex) to get the address

```javascript
function deriveEthAddress(pubKey) {
  const address = keccak256(pubKey); // keccak256 hash of  publicKey
  // Get the last 20 bytes of the public key
  return "0x" + address.substring(address.length - 40, address.length);
}
```

You can check this mnemonic, private key and address against [myetherwallet](https://www.myetherwallet.com/#view-wallet-info){target=\_blank}. Select restore from mnemonic or private key and verify that the derived address matches the one in this app.

## Creating a Digital Signature With Your Key

Using this private key we can sign transactions from this address and broadcast them to the network.

Note: There are now two types of transactions

1. Legacy (Pre-EIP1559) which at some point will be deprecated
2. EIP1559 Transactions utilizing the new gas fee estimation methods

Both types are covered here.

Nodes that are verifying transactions in the network will use the signature to determine the address of the signatory, cryptographically verifying that every transaction from this account is coming from someone who has access to the corresponding private key.

You can sign transactions in the browser with the [@ethereumjs/tx library](https://github.com/ethereumjs/ethereumjs-monorepo/tree/master/packages/tx){target=\_blank}.

```javascript
const EthereumTx = require('ethereumjs-tx')
...

const { FeeMarketEIP1559Transaction, Transaction } = require("@ethereumjs/tx");
const { Chain, Hardfork, Common } = require("@ethereumjs/common");
const { bigIntToHex } = require("@ethereumjs/util");

function signLegacyTx(privKey, txData){
    const txParams = new Common({ chain: Chain.Mainnet, hardfork: Hardfork.Istanbul })
    const tx = Transaction.fromTxData(txData, { txParams })
    return tx.sign(privKey)
}

function signEIP1559Tx(privKey, txData){
    const txOptions = new Common({ chain: Chain.Mainnet, hardfork: Hardfork.London })
    const tx = FeeMarketEIP1559Transaction.fromTxData(txData, { txOptions })
    return tx.sign(privKey)
}
```

Unsigned Ethereum transactions look something like this:

```javascript
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

```javascript
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

Notice the main difference between signed and unsigned transactions is the inclusion of the variables `v`, `r` and `s`. These variables are used to recover the address corresponding to the key that signed the transaction. This signed transaction is broadcast to the network to be included in a block. You can read more about these variables in [this excellent article here](https://medium.com/mycrypto/the-magic-of-digital-signatures-on-ethereum-98fe184dc9c7){target=\_blank}.

You can recover the sender address from the signed transaction with the following method:

```javascript
function getSignerAddress(signedTx) {
  return "0x" + signedTx.getSenderAddress().toString("hex");
}
```

Unsigned EIP1559 Ethereum transactions looks something like this - _note_ the `gasPrice` is missing and replaced with `maxPriorityFeePerGas` and `maxFeePerGas`, and there is a `type: 2` indicating the EIP1559 transaction.

```javascript
{
    nonce: '0x00',
    type: 2,
    gasLimit: '0x09184e72a000',
    maxPriorityFeePerGas: '0x09184e72a000',
    maxFeePerGas: '0x09184e72a000',
    gasLimit: '0x2710',
    to: '0x31c1c0fec59ceb9cbe6ec474c31c1dc5b66555b6',
    value: '0x10',
    data: '0x7f7465737432000000000000000000000000000000000000000000000000000000600057',
    chainId: 3
}
```

And a signed EIP1559 transaction looks something like this

```javascript
{
    nonce: '0x00',
    type: 2,
    gasLimit: '0x09184e72a000',
    maxPriorityFeePerGas: '0x09184e72a000',
    maxFeePerGas: '0x09184e72a000',
    to: '0x31c1c0fec59ceb9cbe6ec474c31c1dc5b66555b6',
    value: '0x00',
    data: '0x7f7465737432000000000000000000000000000000000000000000000000000000600057',
    chainId: 3,
    v: 0x29,
    r: 0x0172f576ab20d1616ec839b0a8a3475e8113f83f7d98cbe3822f4f4dd7bca262,
    s: 0x025d92c8f2d3add278c263030fb2b4195bb15ad55418141c774354a9594be972
}
```

Notice the main difference between signed and unsigned transaction is the inclusion of the variables `v`, `r` and `s`. These variables are used to recover the address corresponding to the key that signed the transaction.

That's it! You've successfully generated a private, public key-pair and then used that to derive a valid Ethereum address. You've also then created the world's tiniest crypto-wallet. Using the `signLegacyTx()` and the `signEIP1559Tx()` functions you have created and signed transactions. You can now also recover the address from a digital signature or signed transaction.

You'll very rarely have to do this kind of crypto-primitive handling. For one, it's garbage for security. But, also, there is so much tooling available to you to do these kind of operations safely and efficiently at scale. For learning purposes, however, nothing beats coding this stuff on its own!

## Additional links

- [Understanding the concept of private keys, public keys and addresses in Ethereum](https://etherworld.co/2017/11/17/understanding-the-concept-of-private-key-public-key-and-address-in-ethereum-blockchain/){target=\_blank}
- [Bitcoin wiki on Secp256k1](https://en.bitcoin.it/wiki/Secp256k1){target=\_blank}
- [Ethereum yellow paper](https://ethereum.github.io/yellowpaper/paper.pdf){target=\_blank}
- [Article: The Magic of Digital Signatures (MyCrypto)](https://medium.com/mycrypto/the-magic-of-digital-signatures-on-ethereum-98fe184dc9c7){target=\_blank}
