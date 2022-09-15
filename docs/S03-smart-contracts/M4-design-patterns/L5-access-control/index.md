Access Control Design Patterns
==============================

Access Control is a broad term. Most generally, it means who is allowed to do what on your smart contract. Who is allowed to mint new tokens, create a new pointer contract or release funds, for example.

We'll be looking at Access Control from a Solidity and coding standpoint, but Access Control is actually a pivot point where the blockchain enters the real world. In the following examples, we'll write code to allow a certain `address` to do (or not do) a certain action. However, `address` may correspond to a user in the real world, granting them certain privileges over the contract. If that contract holds the funds for a group, that person is now the treasurer of the group!

Keep this in mind as we go through these different examples and a teaser for our later sections on DAOs.

Restricting Access and `Ownable`
--------------------------------

A very simple form of access control is making contract state private. You cannot prevent people or computer programs from reading your contracts’ state. The state is publicly available information for anyone with access to the blockchain. However, you *can* restrict other contracts’ access to the state by making state variables private, like in the basic example below:

```
contract C1 {  
  uint private internalNum;
}
```

This simple typing can provide some aspect of security through access control.

A broader form of access control is the `Ownable` design pattern, the "Hello, World!" of access control, you might say. It designates a certain address, or addresses, as the "owner" or admin of the contract.

As we learned earlier, function modifiers allow us to reuse code and increase contract readability. We can also use them to restrict access based on the Ownable model:

```
address owner;  

constructor() payable public {      
  owner = msg.sender;  
}    

modifier onlyOwner() {      
  require(msg.sender == owner, "Not authorized.");      
  _;  
}    

function withdraw(uint _amount) onlyOwner public {      
  owner.transfer(_amount);  
}      
```

The above code declares the variable `owner` and assigns that role to whoever is creating the contract, using the `msg.sender` global variable. We then declare a modifier `onlyOwner()`, which establishes a security check at the top of each function we assign it. Using the modifier syntax, we require a check of the identity of the transaction sender to see if it matches the declared `owner`.

We then place this modifier in front of whichever functions we want to restrict access to. In this case, we're adding it to the `withdraw()` function (which makes sense, as we don't want anyone to be able to drain our contract of value!). This makes it so that the only user who can access this specific function is `owner`, all other addresses will fail.

A common contract used for this is OpenZeppelin's [Ownable.sol](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable){target=_blank}, which also lets you `transferOwnership` to another user or `renounceOwnership` if your contract only requires central authority for a certain period of time.

Please note that the Ownable pattern is a bit fragile: it can become a single point of failure and is not very sophisticated in terms of Access Control.

Pausable
--------

Another form of access control has to do with turning the smart contract itself into a state machine. As we mentioned earlier in the distributed consensus section, [a state machine](https://en.wikipedia.org/wiki/Finite-state_machine){target=_blank} can be in one of a finite number of states at any time.

To make the smart contract a state machine, we'll use the `enum` variable type to create a series of possible states. To have access control, we'll then assign only certain functions to run when the contract is in a certain state. Here's what this looks like in Solidity, where the possible states are `Deposits` and `Withdraws` and the state changes after a time of 30 days from the contract's `creationTime`: 

```
enum Stages { Deposits, Withdraws }  
Stages stage = Stages.Deposits;  
mapping(address => uint) balances;  
uint creationTime = now;  

function deposit() payable public {      
  require(stage == Stages.Deposits && msg.value > 0);      
  balances[msg.sender] += msg.value;  
}        

function withdraw() public {      
  if(stage != Stages.Withdraws && now >= creationTime + 30 days) {          
    stage = Stages.Withdraws;      
  }      
  require(stage == Stages.Withdraws && balances[msg.sender] > 0);      
  uint amount = balances[msg.sender];      
  balances[msg.sender] = 0;      
  msg.sender.transfer(amount);  
}        
```

The deposit() function can only be called when the `stage` enum is in `Deposits`. After 30 days has passed, the contract transitions into `Withdraws` whenever someone calls `withdraw()`. 

For an example of this example, ["The DAO"](https://github.com/blockchainsllc/DAO){target=_blank} contract required 27 days between a successful request to split the DAO and the ability to do so. This ensured the funds were kept within the contract, increasing the likelihood of recovery.

We have another example of this form of access control with the Circuit Breaker design pattern, also called Emergency Stop or Pausable. Circuit Breakers are design patterns that allow contract functionality to be stopped. This would be desirable in situations where there is a live contract where a bug has been detected. Freezing the contract would be beneficial for reducing harm before a fix can be implemented. Here's what it looks like in Solidity: 
 
```
contract CircuitBreaker {    
  bool public stopped = false;    
  
  modifier stopInEmergency { require(!stopped); _; }    
  modifier onlyInEmergency { require(stopped); _; }    
  function deposit() stopInEmergency public { … }    
  function withdraw() onlyInEmergency public { … }   
}      
```

Circuit breaker contracts can be set up to permit certain functions in certain situations. For example, if you are implementing a withdrawal pattern, you might want to stop people from depositing funds into the contract if a bug has been detected, while still allowing accounts with balances to withdraw their funds. In a situation such as this, you would also want to restrict access to the accounts that can modify the stopped state variable, maybe to the contract owner (such as multisig wallet) or a set of admins.

Here's another example, with three separate states that dictate certain rules to be followed: 

```
bool isStopped = false;
address owner;
constructor() payable public {    
  owner = msg.sender;
}

function stopContract() public {    
  require(msg.sender == owner);    
  isStopped = true;
}

function resumeContract() public {    
  require(msg.sender == owner)    
  isStopped = false;
}

function emergencyWithdraw() public {    
  require(msg.sender == owner && isStopped);    
  owner.transfer(this.balance);
}
```
 
Role-Based Access Control
-------------------------

Role-based access control is a more layered approach to access control to meet the more varied demands of a smart contract or application. It follows a similar trend in software development access: Certain individuals are administrators, others are contributors, others can just view the code.

OpenZeppelin advocates using their role-based access control library, `[Roles.sol,](https://docs.openzeppelin.com/contracts/2.x/api/access#Roles){target=_blank}` instead of `Ownable.sol`. They've also implemented roles-based access control in contracts, such as ERC20Mintable.sol, which has a `MinterRole` allowed to create new tokens. You can read more about their approach to role-based access control [in this post here.](https://docs.openzeppelin.com/contracts/2.x/access-control){target=_blank}

Role-based access control can be critical to developing code-based governance, such as in a DAO. Keep this design pattern in mind when we discuss DAOs later!

Additional Resources
--------------------

* [Wiki: Access Control](https://docs.openzeppelin.com/contracts/2.x/access-control){target=_blank} A comprehensive article from OpenZeppelin about Access Control design patterns and how contracts in their repository enacts different patterns.
* [Code: OpenZeppelin's Ownable.sol](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable){target=_blank}
* [Code: OpenZeppelin's Pausable.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/b0cf6fbb7a70f31527f36579ad644e1cf12fdf4e/contracts/security/Pausable.sol){target=_blank}
