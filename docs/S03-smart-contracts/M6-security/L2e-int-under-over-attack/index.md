Integer Over / Underflow
========================

**Note: Due to SafeMath being included in Solidity 0.8.x, the likelihood of you writing an integer under or overflow is extremely unlikely. However, a number of contracts still exist with this attack vector and it's good to know about. But, again, the inclusion of SafeMath helps significantly protect against this attack vector.**

This contract shows what an integer overflow vulnerability ([SWC-101](https://swcregistry.io/docs/SWC-101){target=_blank}) looks like.

In this VulnerableContract the lockTime is manipulable by the currentInvestor. The maximum value for the lockTime is 4294967295 because it is declared type uint32 (and 2^32 = 4294967296). If the currentInvestor attempts to set the value above 4294967295, it will overflow and start counting back at 0.

```
pragma solidity ^0.5.0;

// Example Integer Overflow and Underflow  

contract VulnerableContract {    
  uint MINIMUM_INVESTMENT = 50 ether;    
  uint32 INITIAL_LOCK_TIME = 2592000; // 30 days in seconds    
  address payable currentInvestor;    
  uint investmentTimestamp;    
  uint32 public lockTime = INITIAL_LOCK_TIME;      
  
  function  increaseLockTime(uint32 _seconds) public {        
    require(msg.sender == currentInvestor);        
    // uint32 max is 4294967295 seconds. Attack passing 4292375295
    lockTime += _seconds;     
  }          
  
  function invest() public payable {        
    require(currentInvestor == address(0));        
    require(msg.value >= MINIMUM_INVESTMENT);        
    currentInvestor = msg.sender;        
    investmentTimestamp = now;    
  }          
  
  function withdrawWithProfit() public {        
    require(msg.sender == currentInvestor);        
    require(now - investmentTimestamp >= lockTime);        
    uint profit = 1 ether + lockTime * 1 wei;        
    currentInvestor.transfer(MINIMUM_INVESTMENT + profit);        
    currentInvestor = address(0);        
    lockTime = INITIAL_LOCK_TIME;    
  }          
  
  function getBalance() view public returns(uint) {        
    return address(this).balance;    
  }          
  
  function() external payable {}
}
```
    
This type of attack is easily avoidable by using [a SafeMath library such as this](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/math/SafeMath.sol){target=_blank}, that provides safety checks and will revert on error. The SafeMath library [now ships](https://blog.soliditylang.org/2020/12/16/solidity-v0.8.0-release-announcement/){target=_blank} with Solidity as of 0.8.x, so you do not have to include it if you're working with a compiler on 0.8.x except in very specific cases mentioned [here](S03-smart-contracts/M6-security/L2e-int-under-over-attack/index.html){target=_blank}.
