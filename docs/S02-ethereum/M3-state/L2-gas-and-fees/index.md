We want to stress the distinction between Gas Cost, **gas limit vs. gas price vs. gas cost vs. gas fee.**

**Gas** Special unit denoting how much computation work each EVM op-code uses.  "Every operation that can be performed by a transaction or contract on the Ethereum platform costs a certain number of gas" Gas does not have a financial value associated with it because "ether, like bitcoins, have a market price that can change rapidly! But the cost of computation doesn't go up or down just because the price of ether changes. So it's helpful to separate out the price of computation from the price of the ether token, so that the cost of an operation doesn't have to be changed every time the market moves." ([source](https://ethereum.stackexchange.com/questions/3/what-is-meant-by-the-term-gas))

**Gas Cost** amount of gas for each EVM opcode operation implied by your transaction. The gas cost of an operation is predetermined by the Ethereum Yellow Paper, you have developer tools or a wallet to add up the cost of your transactions.

**Gas Price** The amount of ether required by network multiplied by Gas Cost

**Gas Limit** The maximum amount of gas that could be used by the transaction.

**Transaction Fee** The total amount of ether you spend on a transaction. After 1559, this means the base fee + the miner tip.

Please note, unfortunately these terms are not standardized. For example, the Ethereum Yellow Paper groups what we're calling "Gas Cost" under a section titled "Appendix H: Fee Schedule." We're proposing the above terminology to help you separate between the computation cost and limits and the price of including your transaction in a block.

(Thank you to Nichanan Kesonpat for suggesting the above explainer. Any resulting confusion is strictly on our part, however!)

Additional Resources:

1. [What is Meant By the Term Gas? -- Stackexchange](https://ethereum.stackexchange.com/questions/3/what-is-meant-by-the-term-gas)
2. [Ethereum Yellow Paper](https://ethereum.github.io/yellowpaper/paper.pdf) (Gas costs appear in "Appendix G: Fee Schedule")
3. [Gas Costs as Outlined in Yellow Paper (Spreadsheet)](https://docs.google.com/spreadsheets/d/1n6mRqkBz3iWcOlRem_mO09GtSKEKrAsfO7Frgx18pNU/edit#gid=0)
4. [Ethereum, Gas, Fuel and Fees -- Consensys Media](https://media.consensys.net/ethereum-gas-fuel-and-fees-3333e17fe1dc)
5. [EthGasStation](https://ethgasstation.info/)
6. [EVM Opcodes and Instruction -- Trail of Bits](https://github.com/crytic/evm-opcodes)
7. [GasNow.org](https://www.gasnow.org/) Up-to-date gas estimates
