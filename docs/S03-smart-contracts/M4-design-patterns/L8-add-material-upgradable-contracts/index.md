Additional Material: Upgradable Contracts
=========================================

We wanted to provide another example of an upgradable contract pattern. This pattern uses a separate contract to act as storage to another contract that contains the logic, also known as a "proxy delegate pattern". When you upgrade a contract, all your state is still in the old contract address. Therefore, we say the contract has "Eternal Storage."

To avoid upgrades to the storage contract it should be as flexible as possible, by using several mappings for each data type where hashes are used as keys (only `uint` is shown in the example below):

```
address owner = msg.sender;
address latestVersion;
mapping(bytes32 => uint) uIntStorage;

function upgradeVersion(address _newVersion) public {    
  require(msg.sender == owner);    
  latestVersion = _newVersion;
}

function getUint(bytes32 _key) external view returns(uint) {    
  return uIntStorage[_key];
}

function setUint(bytes32 _key, uint _value) external {    
  require(msg.sender == latestVersion);    
  uIntStorage[_key] = _value;
}

function deleteUint(bytes32 _key) external {    
  require(msg.sender == latestVersion);    
  delete uIntStorage[_key];
}    
```

Each mapping should be manipulated by three functions: store, retrieve and delete. Use the access control pattern to allow only the most recent version of the logic contract to use the "eternal storage."

Additional Material
-------------------

* [Article Series: Summary of Ethereum Upgradeable Smart Contract R&D, Part I](https://blog.indorse.io/ethereum-upgradeable-smart-contract-strategies-456350d0557c){target=_blank} and  [Part II](https://medium.com/coinmonks/summary-of-ethereum-upgradeable-smart-contract-r-d-part-2-2020-db141af915a0){target=_blank} Great overview of upgradability patterns.
* [Tutorial: Security considerations and how to upgrade with Open Zeppelin](https://trufflesuite.com/guides/upgrading-security/)
* [Tutorial: Upgrading Broken Contracts (ConsenSys)](https://consensys.github.io/smart-contract-best-practices/software_engineering/#upgrading-broken-contracts){target=_blank}
* [Tutorial: Diamond Standard](https://dev.to/mudgen/ethereum-s-maximum-contract-size-limit-is-solved-with-the-diamond-standard-2189){target=_blank} An interesting variation on upgradability patterns. We don't see it out a lot in the wild, but an interesting development!
