# Python in Ethereum: Background and Context

After going through all this Solidity content, (which _looks_ like JavaScript but as you now know is very different from JavaScript) we may have some Python developers saying, "What about us?"

Python is, after all, one of the most popular and accessible programming languages. When people want to start programming, they typically feel they have to decide between JavaScript or Python. So, what gives? Where's the Python in Ethereum?

While it's not as popular as Solidity and JavaScript, there are some exciting ways to build on Ethereum using Python. In this section, we're going to go over a few of those projects. In the following section, we'll go over [Vyper,](https://vyper.readthedocs.io/en/stable/){target=_blank} the programming language whose syntax is a subset of Python's.

## Vyper

Vyper is an experimental, contract-oriented, pythonic programming language that targets the Ethereum Virtual Machine. Please note: [there have been some issues with the Vyper compiler.](https://diligence.consensys.net/blog/2019/10/vyper-preliminary-security-review/){target=_blank} Like Python, writing clear, understandable code is of primary importance in Vyper.

Vyper is not trying to be a replacement for Solidity. It is meant to be a more security focused smart contract programming language and will likely not be able to do everything that Solidity can. Its development is uncertain and not nearly as strong as Solidity. You can read more about Vyper in this section [here.](https://vyper.readthedocs.io/en/latest/){target=_blank}

Note that you can use Vyper with a number of development frameworks, including [Truffle](https://www.trufflesuite.com/docs/truffle/reference/configuration#vyper){target=_blank} and Brownie.

## Brownie and Web3.py

[Brownie](https://github.com/eth-brownie/brownie){target=_blank} is a Python-based development and testing framework for smart contracts running on the EVM. It uses [Web3.py](https://web3py.readthedocs.io/en/stable/){target=_blank} as well as Solidity. It is most well-known for being the development framework the [Yearn.Finance](https://yearn.finance){target=_blank} team uses to build their powerful DeFi platform and [CRV.](https://help.coinbase.com/en/coinbase/getting-started/crypto-education/curve-dao-token--crv-){target=_blank}

Brownie definitely takes some notes from Truffle [(they are both "sweet")](https://www.youtube.com/watch?v=R8lcy0JnEt8){target=_blank}, including having a `brownie init` command and their equivalent of Truffle boxes, ["Brownie Mixes."](https://github.com/brownie-mix){target=_blank} This makes it an easy tool for a lot of Truffle developers familiar with Truffle.

Here are some tutorials to introduce you to Brownie:

*   [Tutorial: Develop a DeFi Project using Python (Chainlink){target=_blank}](https://blog.chain.link/develop-python-defi-project/){target=_blank}
*   [Tutorial: Vyper and Brownie Contract Development on EVM Chains](https://medium.com/ethereum-classic/vyper-and-brownie-contract-development-on-evm-chains-85ba7fa2feef){target=_blank} An interesting tutorial walking through developing a contract using Vyper and Brownie.

## Yellow Paper rewrite

[Piper Merriam](https://twitter.com/pipermerriam){target=_blank} is a Python-based Ethereum developer who works for the Ethereum Foundation. They have proposed an [interesting project](https://ethereum-magicians.org/t/replace-the-yellow-paper-with-executable-markdown-specification/6430){target=_blank}: Replacing [Ethereum's yellow paper](https://ethereum.github.io/yellowpaper/paper.pdf){target=_blank} (which we studied earlier) with executable markdown. This was inspired by Ethereum 2.0's [Beacon chain specifications.](https://github.com/ethereum/eth2.0-specs){target=_blank} Rather than writing a document of specifications, the Ethereum 2.0 developer teams built a series of tests based on the spec conditions of a theoretical Beacon chain. Then, Ethereum 2.0 software clients only had to make sure they passed those tests.

Merriam is proposing a similar exercise, but for Ethereum Mainnet (the PoW chain), based in Python. The goal would be to replace the yellow paper, which can be very challenging to read. It would rely heavily on [py-EVM](https://py-evm.readthedocs.io/en/latest/){target=_blank} (a Python implementation of the EVM). The whole project is very new and you can check [it's GitHub repository](https://github.com/ethereum/eth1.0-specs){target=_blank} for updates. Maybe you can even get involved!

## Fe

<a href="https://github.com/ethereum/fe" target="_blank" rel="noopener noreferrer">Fe</a> is "an emerging smart contract language for the Ethereum blockchain." It's influenced both by Python _and_ Rust and was released in January 2021. You can read more about it [here.](https://snakecharmers.ethereum.org/fe-a-new-language-for-the-ethereum-ecosystem/){target=_blank} To be honest, it looks more like Rust than Python, but that's just our opinion.

## Conclusion

While more niche, it's possible to be a Python developer and contribute to the Ethereum (and wider blockchain) ecosystem! Solidity is still important to know, but we hope this gets you started finding more Python opportunities.
