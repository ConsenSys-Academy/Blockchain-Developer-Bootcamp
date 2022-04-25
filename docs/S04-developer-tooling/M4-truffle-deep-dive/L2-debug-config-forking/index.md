## Squashing Bugs with the Debugger
 
Debugging is an important part of any software development lifecycle and Truffle ships with a full CLI-based, interactive debugger to help you squash those pesky bugs.

A debug instance is always instantiated off the back of a transaction (tx) hash (as we saw returned when we invoked storage.set(42) in the earlier example). For example:

    {
    tx: '0x46e4bb35108e5ecf7ff656008295fda572a753476d5e04c286fcdb7868447dd6',
    receipt: {
        transactionHash: '0x46e4bb35108e5ecf7ff656008295fda572a753476d5e04c286fcdb7868447dd6',
        transactionIndex: 0,
        blockHash: '0x85dbdf5d71194cb0d841d58bbac283ccf078ce0ebe1c054c6c2ab76442459894',
        blockNumber: 9,
        from: '0x5ca1605d4671669b38f7e37c881ed996ede5ac68',
        to: '0x524b2860a2489e385c5e12537f58d5a09a9d33ab',
    ...
    }

# Running the Debugger
Assuming we have a valid transaction hash the debugger is simply invoked as follows. Note that you’ll need to paste in a hash of a transaction that exists on the chain you’re debugging against.

    truffle debug 0x4a1dcabb384e6ca1b5091495349603499fc2022e5832efdb53f872b6ff23a1c0


Assuming all is good, you should now see the following output (note that the full list of commands has been truncated for brevity):

    Starting Truffle Debugger...

    Addresses affected:
    0x6cA2F11a43b2B8f4DCE7De62f8Dc03f8E12BC48F - SimpleStorage

    Commands:
    (enter) last command entered (step next)
    (o) step over, (i) step into, (u) step out, (n) step next
    (c) continue until breakpoint, (Y) reset & continue to previous error
    (y) (if at end) reset & continue to final error
    (;) step instruction (include number to step multiple)

    SimpleStorage.sol:

    2: pragma solidity >=0.4.21 <0.7.0;
    3:
    4: contract SimpleStorage {
     ^^^^^^^^^^^^^^^^^^^^^^^^


You can now start stepping through your code in a manner similar to that of any traditional debugger. As stated in the Truffle docs though it’s worth noting that “you're not running the code in real-time; instead, you're stepping over the historical execution of that transaction, and mapping that execution onto its associated code”.

In the above example, stepping over a couple of times brings us into our SimpleStorage.sol contract wherein we can see our storedData state variable being assigned its new value.

    SimpleStorage.sol:

    7:   event setEvent(uint newValue);
    8:
    9:   function set(uint x) public {
        ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    debug(develop:0x8bd62b08...)> o

    SimpleStorage.sol:

    8:
    9:   function set(uint x) public {
    10:     storedData = x;

# In-test Debugging
Lastly, a feature available as of Truffle v5.1 is that of in-test debugging. This essentially enables you to interrupt your tests by simply wrapping a given line with await debug(). 

More detail on in-test debugging with a simple example [here](https://trufflesuite.com/docs/truffle/getting-started/using-the-truffle-debugger/#in-test-debugging). 
