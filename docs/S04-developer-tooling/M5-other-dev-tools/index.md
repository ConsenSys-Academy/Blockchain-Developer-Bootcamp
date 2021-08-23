# Other Development Tools
  
<i>Before we dive into these other development frameworks, we wanted to provide an "offramp" to folks who may not be comfortable with Javascript Frameworks. We'd encourage you to check out the sections on Node and Javascript Frameworks in the Basic Training course. People uncomfortable with terminal-based development might be interested in <a href="https://github.com/kitze/JSUI" target="_blank" rel="noopener noreferrer">JSUI,</a> a GUI-based Javascript framework development environment.</i>

## Hardhat

Another popular development framework is <a href="https://hardhat.org/" target="_blank" rel="noopener noreferrer">Hardhat,</a> which actually started as a fork of Truffle. It has since grown to create its own suite of tools and a devoted community.

Hardhat divides itself into "tasks" and "plugins". Running `npx hardhat compile` is a task, for example. <a href="https://hardhat.org/plugins/" target="_blank" rel="noopener noreferrer">Plugins</a> are extended functionality ported into Hardhat. <a href="https://hardhat.org/plugins/hardhat-gas-reporter.html" target="_blank" rel="noopener noreferrer">Gas Reporter</a> and 
<a href="https://hardhat.org/plugins/hardhat-contract-sizer.html" target="_blank" rel="noopener noreferrer">Contract Sizer</a> are two popular plugins for Hardhat. 

Why choose Hardhat? Some feel as though the command-line experience of Hardhat is faster than Truffle. Others like the extensive plugin features. One feature popular with Hardhat developers is their use of <code>console.log()</code> in smart contracts. When developing locally with Hardhat, you can import the `console.sol` contract, like so:

<pre>
pragma solidity ^0.6.0;

import "hardhat/console.sol";

contract Token {
  //...
}</pre>

You can then add it to your contract when developing it locally:

<pre>
function transfer(address to, uint256 amount) external {
    console.log("Sender balance is %s tokens", balances[msg.sender]);
    console.log("Trying to send %s tokens to %s", amount, to);

    require(balances[msg.sender] >= amount, "Not enough tokens");

    balances[msg.sender] -= amount;
    balances[to] += amount;
}</pre>

Which gives you this output when running locally on the Hardhat Network:

<pre>
$ npx hardhat test

  Token contract
    Deployment
      ✓ Should set the right owner
      ✓ Should assign the total supply of tokens to the owner
    Transactions
Sender balance is 1000 tokens
Trying to send 50 tokens to 0xead9c93b79ae7c1591b1fb5323bd777e86e150d4
Sender balance is 50 tokens
Trying to send 50 tokens to 0xe5904695748fe4a84b40b3fc79de2277660bd1d3
      ✓ Should transfer tokens between accounts (373ms)
      ✓ Should fail if sender doesn’t have enough tokens
Sender balance is 1000 tokens
Trying to send 100 tokens to 0xead9c93b79ae7c1591b1fb5323bd777e86e150d4
Sender balance is 900 tokens
Trying to send 100 tokens to 0xe5904695748fe4a84b40b3fc79de2277660bd1d3
      ✓ Should update balances after transfers (187ms)


  5 passing (2s)</pre>

You can learn more about this feature in their documentation <a href="https://hardhat.org/hardhat-network/#console-log" target="_blank" rel="noopener noreferrer">here.</a>

Here are some easy ways to get started using Hardhat to see how you like it:
- <a href="https://hardhat.org/tutorial/" target="_blank" rel="noopener noreferrer">Hardhat's Beginner Tutorial and Project Setup</a>
- <a href="https://hardhat.org/hardhat-network/" target="_blank" rel="noopener noreferrer">Hardhat Development Network</a>
- <a href="https://hardhat.org/plugins/" target="_blank" rel="noopener noreferrer">Index of Reusable Plugins</a>

The Hardhat teams recommends "paying attention to see whether any plugins already solve problems [you] may have."

## Scaffold-Eth

## Brownie

## Frontend Tools

For your project, we've also discussed frontend interfaces. There are two services you can use for free to create a frontend instance easily:
- <a href="https://devcenter.heroku.com/start" target="_blank" rel="noopener noreferrer">Heroku</a> is a Platform-as-a-Service, providing a quick way to deploy apps in a number of popular languages, such as Node.js (Javascript), Python, Ruby and Go.  You can connect your Github repo to your project for easy deployment. Heroku's basic plan is free and provides basic resources for getting started. <a href="https://www.heroku.com/free" target="_blank" rel="noopener noreferrer">Read more here.</a>
- <a href="https://www.netlify.com/" target="_blank" rel="noopener noreferrer">Netlify</a> also has a Git-based workflow allowing you to deploy your project easily from Github. It is also free and has a getting started manual <a href="https://docs.netlify.com/configure-builds/get-started/" target="_blank" rel="noopener noreferrer">here.</a>

There are other options as well! These are two of the more popular ones we see students using.

## Additional Material
- <a href="https://medium.com/@shihyuhwang/react-project-setup-using-hardhat-truffle-part-1-20a596865e" target="_blank" rel="noopener noreferrer">Tutorial: React Project Setup Using Hardhat & Truffle Part I</a> From Bootcamp alum and fellow Shih-Yu Hwang
- 


    