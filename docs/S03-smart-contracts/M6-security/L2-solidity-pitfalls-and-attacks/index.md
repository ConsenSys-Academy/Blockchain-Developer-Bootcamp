Solidity Pitfalls and Attacks
=============================

As we've made clear again and again, smart contract development is potentially very dangerous. This is unlike the vast portion of web development, where environments and code can be torn down, changed, and easily deployed again. Because of this, being a smart contract developer means being acutely aware of the ways in which your code can be exploited and creating safety features to ensure against unforeseen attacks.

Over the next few sections, we're going to be discussing smart contract security. We'll start by going over some common pitfalls and attacks with Solidity (as a language) and smart contracts generally. We'll then discuss testing as a means to further protect your code. Last, we'll go over some security services you can use when writing and developing smart contracts

Solidity Tips
-------------

### Use Specific Compiler Pragma

A common method is to use the `^` to indicate the lowest compiler version that your contract will work with. However, if you have a testing suite you've built against your contract, you should not include the `^` and just list the compiler version.  

```
pragma solidity ^0.4.4; // Possibly dangerous          
```
   
```
pragma solidity 0.4.4; // Better          
```

### Built-In Variable Names

Built-in variables can be shadowed, be careful when naming your functions: 

```
function revert() internal pure {} // Possibly dangerous        
```
 
```
function myRevert() internal pure {} // Better            
```

### Proper Use of `require`, `assert` and `revert`

**`require(msg.sender == owner)`** 
* Validation of **inputs, external call returns and variables** before state changes
* **Refunds** remaining gas when fail
* Should be used **more often** and **towards the beginning** of functions

**`assert(age > 100)`** 
* Validation of **invariants**, situations that **should never happen** and variables **after state changes**
* **Consumes all gas** when fail
* Should be used **less often** and **towards the end** of functions

**`revert()`** 
* **Reverts** the current transaction
* **Refunds** remaining gas when fail
* Used **within if-else** statements

### Use Modifiers Only for Validations

Just do validations within modifiers and avoid external calls on them: 

```
modifier partnerShare() { // Possibly dangerous
  partner.transfer(msg.value / 10); 
  _; 
}          
```
 
```
modifier onlyOwner() { // Better!
  require(msg.sender == owner); 
  _; 
}          
```

### Pull Over Push

Prioritize *receiving* contract calls over *making* contract calls: 

```
function doRefund() external onlyOwner { // Possibly dangerous  
  uint refund;  
  for(uint i = 0; i < refunds.length; i++) {      
    refund = refunds[i].value;      
    refunds[i].value = 0;      
    refunds[i].addr.transfer(refund);  
  }
}                    
```
 
```
function withdrawRefund() external { // Better!  
  require(refunds[msg.sender] > 0);  
  uint refund = refunds[msg.sender];  
  refunds[msg.sender] = 0;  
  msg.sender.transfer(refund);
}          
```

### Fallback Functions and Data Length

Keep fallback functions simple and check data length: 

```
fallback() payable external { // Possibly dangerous  
  balances[msg.sender] += msg.value;
}            
```
 
```
receive() external { // Better!  
  balances[msg.sender] += msg.value;
}

fallback() external {  
  require(msg.data.length == 0);  
  emit LogDeposit(msg.sender);
}          
```
 
### Checks-Effects-Interactions

Avoid state changes after external calls, to avoid things like [the DAO hack:](https://solidity.readthedocs.io/en/v0.5.11/security-considerations.html#re-entrancy){target=_blank} 

```
function withdraw(uint amount) public { // Possibly dangerous  
  require(balances[msg.sender] >= amount);  
  msg.sender.call{value:amount}("");  
  balances[msg.sender] -= amount;
}        
```
 
```
function withdraw(uint amount) public { // Better!  
  require(balances[msg.sender] >= amount);  
  balances[msg.sender] -= amount;  
  msg.sender.call{value:amount}("");
}        
```
 
### Proper use of `call`, `delegatecall` instead of `send`, `transfer`

After the Istanbul hardfork, [it's recommended](https://consensys.net/diligence/blog/2019/09/stop-using-soliditys-transfer-now/){target=_blank} not to use `send` and `transfer`, and instead use `call.value` 

```
contract Vulnerable { // Possibly dangerous  
  function withdraw(uint256 amount) external {      
    // This forwards 2300 gas, which may not be enough if the recipient      
    // is a contract and gas costs change.      
    msg.sender.transfer(amount);  
  }
}      
```
 
```
contract Fixed { // Better!  
  function withdraw(uint256 amount) external {      
    // This forwards all available gas. Be sure to check the return value!      
    (bool success, ) = msg.sender.call{value:amount}("");      
    require(success, "Transfer failed.");  
  }
}      
```

And then proper use of `call` and `delegatecall`: 

```
addr.call(abi.encodeWithSignature("f(uint)", a));
```

* Used to call functions and send ether
* Allows specify gas
* Returns boolean
* Does not propagate exceptions

```
addr.delegatecall(abi.encodeWithSignature("f(uint)", a));
```

* Used to run functions within the caller's context (library feature)
* Allows specify gas
* Returns boolean
* Does not propagate exceptions

Additional Material
-------------------

* [Wiki: Smart Contract Best Practices (ConsenSys)](https://consensys.github.io/smart-contract-best-practices/){target=_blank}
* [Article: Stop Using Solidity's `transfer`](https://consensys.net/diligence/blog/2019/09/stop-using-soliditys-transfer-now/){target=_blank} Article from ConsenSys Diligence
 
