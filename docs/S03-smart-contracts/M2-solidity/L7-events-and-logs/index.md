  Declaring Events
----------------


```
pragma solidity >= 0.5.0 <= 0.8.0;    

contract ExampleContract {       

  event LogReturnValue(address indexed _from, int256 _value);      
  
  function foo(int256 _value) public returns (int256) {       
    emit LogReturnValue(msg.sender, _value);       
    return _value;    
  }    
  
}  
```
 This is how you declare an event called `LogReturnValue`. Use the `event` keyword followed by the event name.

 A recent update to the Solidity compiler requires the `emit` keyword before an event is logged. This helps further clarify when events are being logged in the contract code.

 Declaring events require that you specify the parameter type as well as a name for the parameter. This parameter name is the name that will appear in the log, so make it descriptive and clear.

 You can add the **indexed** keyword to event parameters. Up to three parameters can receive the indexed attribute. This increases the searchability of events. It is possible to filter for specific values of indexed arguments in the user interface.

 [Here is a link to the solidity documentation on events.](https://solidity.readthedocs.io/en/latest/contracts.html#events){target=_blank}

 Use Cases
---------

 The common uses for events can be broken down into three main use cases:

 1. Events can provide smart contract return values for the User Interface
2. They can act as asynchronous triggers with data and
3. They can act as a cheaper form of storage.

### Get values when transaction is mined

 When a transaction is sent via web3.js, a transaction hash is returned, even if the contract functions specifies a return value. Transactions don’t return the contract value because transactions are not immediately mined and included in the blockchain - it takes time (they are asynchronous). You can use an event in the contract function in conjunction with an event watcher in the UI to observe a variable value when the transaction is mined.

### Trigger application logic

 You can use an event watcher as a trigger for application logic beyond just reading return values. You could take another action, display a message or update the UI when an event is observed.

    
 

### Events as Data Storage

 Logs, which are essentially the same as events (the context dictates which term is more appropriate) can also be used as a cheaper form of storage. Logs cost 8 gas per byte whereas contract storage costs 20,000 per 32 bytes, or 625 gas per byte. Logs are cheaper, but also cannot be accessed from any contracts so their use case as storage objects is much more limited. Even still, logs can be useful for aggregating historical reference data.

    
 

 Events are inheritable members of contracts. You can call events of parent contracts from within child contracts.

 When called from within a contract, events cause arguments to be stored in the transaction log, a special data structure in the blockchain. The logs are associated with the address of the contract and will be incorporated into the blockchain, persisting as long as a block is accessible.

 Log and event data are not accessible from within contracts, not even from the contract that created the log. Events are useful when interacting with an application. They can provide notifications and confirmations of transactions happening in the smart contract. They are also useful for debugging purposes during development.

 Logs are not part of the blockchain per se since they are not required for consensus (they are just historical data), but they are verified by the blockchain as the transaction receipt hashes are stored inside the blocks.

 Remember that events are not emitted until the transaction has been successfully mined.

 When to log events
------------------

 Logging an event for every state change of the contract is a good heuristic for when you should use events. This allows you to track any and all updates to the state of the contract by setting up event watchers in your javascript files.

 

---

 Additional Resources:

 * [Technical introduction to Events and Logs in Ethereum (Joseph Chow, Consensys)](https://media.consensys.net/technical-introduction-to-events-and-logs-in-ethereum-a074d65dd61e){target=_blank}
* [Events - Solidity Docs](https://solidity.readthedocs.io/en/latest/contracts.html#events){target=_blank}
* [Listening to events with web3.js](https://web3js.readthedocs.io/en/1.0/web3-eth-subscribe.html?highlight=events#subscribe-logs){target=_blank} or [via the contract object](https://web3js.readthedocs.io/en/v1.2.0/web3-eth-contract.html#contract-events){target=_blank}
* [Article: Deep Dive Into Ethereum Logs](https://codeburst.io/deep-dive-into-ethereum-logs-a8d2047c7371){target=_blank}
* [Article: Everything You Ever Wanted to Know About Events and Logs on Ethereum](https://medium.com/linum-labs/everything-you-ever-wanted-to-know-about-events-and-logs-on-ethereum-fec84ea7d0a5){target=_blank}

  
