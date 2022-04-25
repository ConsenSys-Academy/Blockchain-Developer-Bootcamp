Optimizing Gas
==============

Reducing the gas consumed by a contract is important in two situations:

* Cost of deploying a contract
* Cost to call the contract functions

[The Solidity optimizer](https://solidity.readthedocs.io/en/v0.7.1/internals/optimiser.html){target=_blank} tries to improve the efficiency of your contract as much as possible during compile time. Feel free to dig into the internals of the optimizer.

One of the best ways to optimize your contracts gas usage is to reduce expensive operations in the contract's functions. Creating and modifying storage variables can be expensive.

20,000 gas when a value is set to non-zero from zero; 5,000 gas when writing to existing storage or setting a value to zero; and a 15,000 gas refund when a non-zero value is set to zero.

[Here is a list of OPCODES and their gas costs.](https://docs.google.com/spreadsheets/d/1n6mRqkBz3iWcOlRem_mO09GtSKEKrAsfO7Frgx18pNU/edit#gid=0){target=_blank}

Short Circuit Rules
-------------------

The operators `||` and `&&` apply the common short-circuiting rules. This means that in the expression `f(x) || g(y)`, if `f(x)` evaluates to true, `g(y)` will not be evaluated even if it may have side-effects.

How can these functions in [Unoptimized.sol](https://gist.github.com/ConsenSys-Academy/a61670fd8796d73d8b4b7d5935f9e714){target=_blank} be modified to reduce gas usage?

```
function shortCircuit() public view returns(bool){      
  if (oftenFalse || oftenTrue) {          
    return true;      
  } 
}    

function shortCircuit2() public view returns(bool){      
  if(oftenTrue && oftenFalse) {          
    return false;      
  } else {          
    return true;      
  }  
}  
```

Expensive operations in a loop
------------------------------

Modifying storage variables in a loop can be very expensive and should be avoided unless absolutely necessary.

How can this function be improved, given that `loops` is a storage variable? [Here is the source file.](https://gist.github.com/ConsenSys-Academy/a61670fd8796d73d8b4b7d5935f9e714#file-unoptimized-sol-L26){target=_blank}

```
function looping (uint x) public returns (bool) {      
  for(uint i; i < x; i++){          
    loops += 1;      
  }     
  return true;  
}  
```

Reduce the number of loops
--------------------------

Zero loops is ideal, but sometimes you just have to loop. Since loops are expensive, can you reduce the number of loops in your functions?

```
function looping2 (uint x) public pure returns(bool){      
  uint m = 0;      
  uint v = 0;      
  for(uint i = 0; i < x; i++){          
    m += i;      
  }      
  for(uint j = 0; j < x; j++){          
    v -= j;      
  }      
  return true;  
}  
```

Fixed size byte arrays
----------------------

[From the Solidity Docs:](https://solidity.readthedocs.io/en/latest/types.html#fixed-size-byte-arrays){target=_blank}

It is possible to use an array of bytes as `byte[]`, but it is wasting a lot of space, 31 bytes every element, to be exact, when passing in calls. It is better to use `bytes`. As a rule of thumb, use `bytes` for arbitrary-length raw byte data and `string` for arbitrary-length string (UTF-8) data. If you can limit the length to a certain number of bytes, always use one of `bytes1` to `bytes32` because they are much cheaper.

How can this function be optimized?

```
function byteArray() public returns(uint){      
  byte[] byteArray;      
  return gasleft();  
}  
```

Additional Resources:

* [Optimizing Solidity contract's gas usage](https://medium.com/coinmonks/optimizing-your-solidity-contracts-gas-usage-9d65334db6c7){target=_blank}
* [Under Optimized Smart Contracts Devour Your Money](https://arxiv.org/pdf/1703.03994.pdf){target=_blank}
* [How to Write Smart Contracts that Optimize Gas](https://medium.com/better-programming/how-to-write-smart-contracts-that-optimize-gas-spent-on-ethereum-30b5e9c5db85){target=_blank}
