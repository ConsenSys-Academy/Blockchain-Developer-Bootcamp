Vyper Overview
==============

Despite there being [concerns about its compiler](https://consensys.net/diligence/audits/2019/10/vyper/){target=_blank} and the slower rate of development compared to Solidity, there are still many resources and ways to build smart contracts using [Vyper.](https://vyper.readthedocs.io/en/latest/){target=_blank} In this section, we'll discuss more about the Vyper language and provide resources where you can learn more about the language. Please note, Vyper is still considered somewhat experimental.

Vyper Design Principles
-----------------------

Vyper has a few principles and goals that aim to make it a language that is ideal for programming smart contracts. From [its docs](https://vyper.readthedocs.io/en/latest/){target=_blank} (which we quote extensively in this section):

* **Security** is a primary focus for any smart contract language and Vyper maintains that “it should be possible and natural to build secure smart contracts in Vyper.”
* Vyper code should be not just human readable, but make it difficult to write misleading code. This directive is aimed at **making contract audits as successful as possible.**
* Striving for language and compiler **simplicity** support the other goals by keeping confusing complexity under control.

To achieve these goals, Vyper implements the following features: 

* Bounds and overflow checking
* Support for signed integers and decimal fixed point numbers
* Decidability - Reliably compute upper bounds for gas consumption of any function call
* Strong typing
* Small and understandable compiler code
* Limited support for pure functions

There is a notable lack of the following features that are present in Solidity: 

* **Modifiers** Modifiers make it easier to write misleading code. It encourages writing code where execution jumps around the source file, making audits more difficult. Vyper encourages inline checks in each function to improve clarity.
* **Class Inheritance** Inheritance also makes it easier to write misleading code. Contracts’ logic is spread across multiple files, decreasing readability and requires additional understanding about how inheritance works in case of conflicts.
* **Inline Assembly** Inline assembly makes it possible to manipulate variables without referencing it directly by name. This makes development and auditing more difficult and can obfuscate bugs.
* **Function overloading** Contracts with overloaded functions can be confusing. It may not be clear which function is being called in specific situations.
* **Operator overloading**
* **Recursive calling** It is not possible to set an upper bound on gas limits in contracts with recursive calling
* **Infinite-length loops** It is not possible to set an upper bound on gas limits in contracts with infinite length loops
* **Binary fixed point** In binary fixed point, approximations are required (e.g. in Python 0.3 + 0.3 + 0.3 + 0.1 != 1).

As you can see in the list of features that Vyper is lacking, writing clear, understandable code is of primary importance.

Vyper is not trying to be a replacement for Solidity. It is meant to be a more security focused smart contract programming language and will likely not be able to do everything that Solidity can.

 Additional Links
----------------

* [Code: Simple Bank in Vyper (ConsenSys Academy)](https://github.com/ConsenSys-Academy/simple-bank-vyper){target=_blank} This is a Vyper version of our Simple Bank exercise (normally in Solidity) you'll encounter later in this section.
* [Course: Learn Vyper (0.2)](https://www.youtube.com/watch?v=-kZpEmNnzyE&list=PLO5VPQH6OWdWOd-IJTfIzlM2a1yv1rSN-){target=_blank} A comprehensive series of videos that covers Data Types, Functions, Variables, Logic Control, Errors, Interfaces and much more.
* [Tutorial: Develop a DeFi Project using Python (Chainlink)](https://blog.chain.link/develop-python-defi-project/){target=_blank}
* [Tutorial: Vyper and Brownie Contract Development on EVM Chains](https://medium.com/ethereum-classic/vyper-and-brownie-contract-development-on-evm-chains-85ba7fa2feef){target=_blank} An interesting tutorial walking through developing a contract using Vyper and Brownie.
* [Docs: Vyper by Example](https://vyper.readthedocs.io/en/stable/vyper-by-example.html){target=_blank} From the Vyper documentation, a walkthrough of common development patterns in Vyper.
