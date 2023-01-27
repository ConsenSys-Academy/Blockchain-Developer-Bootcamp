# Other Security Options

Outside of the tools we've provided so far, there are other great security analysis tools:

## Tools

- [OpenZeppelin Defender](https://openzeppelin.com/defender/){target=\_blank} Less of a security tool per se and more like an operating system or dashboard for your smart contracts. This allows you to monitor your smart contracts, respond to exploits or bugs by adjusting access control, and private transaction relayers.
- [Slither](https://github.com/crytic/slither){target=\_blank} A static analysis framework for Solidity built by the auditing firm [Trail of Bits](https://www.trailofbits.com/){target=\_blank}. It is written in Python, is open-source and you can read more about it [here](https://blog.trailofbits.com/2018/10/19/slither-a-solidity-static-analysis-framework/){target=\_blank}.
- [Manticore](https://github.com/trailofbits/manticore){target=\_blank} "A [symbolic execution](https://en.wikipedia.org/wiki/Symbolic_execution){target=\_blank} tool for analysis of smart contracts and binaries" as well as WASM modules. Also built by Trail of Bits! [Read more here](https://blog.trailofbits.com/2017/04/27/manticore-symbolic-execution-for-humans/){target=\_blank}.
- [Ethersplay](https://github.com/crytic/ethersplay){target=\_blank} An EVM Disassembler which takes as input raw EVM bytecode (your contract you're deploying) and analyzes it at the Assembly level. It can provide a flow graph of all the functions in the bytecode. _Another_ tool from Trail of Bits, it also can let you know where Manticore has scanned.
- [Echidna](https://github.com/crytic/echidna){target=\_blank} A fuzzer like Scribble. It is "a Haskell program designed for fuzzing/property-based testing of Ethereum smarts contracts. It uses sophisticated grammar-based fuzzing campaigns based on a contract ABI to falsify user-defined predicates or Solidity assertions." ([source](https://github.com/crytic/echidna){target=\_blank}) Also from Trail of Bits.

## Learning

- [Blocksec CTFs](https://github.com/openblocksec/blocksec-ctfs){target=\_blank} An amazing collection of blockchain Capture The Flag (CTF) exercises and write-ups
- [Article: Ethereum Quirks and Vulnerabilities](https://swende.se/blog/Ethereum_quirks_and_vulns.html){target=\_blank} Discussion around attack vectors on Ethereum
- [Ethernaut](https://ethernaut.openzeppelin.com/){target=\_blank} Phenomenal CTF / Wargame series of exercises for blockchain security. Be sure to checkout the [EthernautDAO](https://twitter.com/ethernautdao){target=\_blank}, organized in part by the designing of Ethernaut.
- [DamnVulnerableDeFi](https://www.damnvulnerabledefi.xyz/){target=\_blank} A DeFi-oriented CFT
- [Capture the Ether](https://capturetheether.com/){target=\_blank} Another blockchain CTF, written by [Steve Marx](https://twitter.com/smarx){target=\_blank}
- [CipherShastra](https://ciphershastra.com/){target=\_blank} Another CTF-style learning challenge
- [Diligence Public Audits](https://consensys.net/diligence/audits/){target=\_blank}, [OpenZeppelin Audits](https://blog.openzeppelin.com/security-audits/){target=\_blank} Another great way to learn to audit is to read reports from the best organizations doing them. Trail of Bits is not blockchain-specific, but you can see [their public security "reviews" here](https://github.com/trailofbits/publications#security-reviews){target=\_blank}.

## Audits

- [Thread: Before an Audit](https://mobile.twitter.com/tinchoabbate/status/1400170232904400897?s=20){target=\_blank} @Tincho, a security researcher at OpenZeppelin, walks through the things you absolutely should do before submitting your code for an audit
- [Code4rena](https://code4rena.com/){target=\_blank} "A community-driven approach to competitive smart contract audits." A great way to get into auditing — no experience necessary.
- [Immunefi](https://immunefi.com/){target=\_blank} A collection of bug bounties for blockchain projects anyone can contribute.
- [Article: Introducing Solidify (Coinbase)](https://web.archive.org/web/20210830084611/https://blog.coinbase.com/introducing-solidify-a-tool-to-automatically-detect-and-classify-smart-contract-security-risks-73a1338fdbbe){target=\_blank} We haven't gotten a chance to try this one, but Coinbase offering a new tool for smart contract analysis. This is not an endorsement of this, just letting you know it exists!
