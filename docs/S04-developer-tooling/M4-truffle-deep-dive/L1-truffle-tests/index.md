# Testing, 1, 2, 3
A comprehensive suite of tests adds robustness to your code as it evolves, and Truffle provides an automated testing framework that makes adding this to your project a breeze.

In the following examples, we’ll be writing our tests in JavaScript, although Truffle also supports Solidity based tests too. Check out the following for when you might use one over the other.

All your tests live in a dedicated tests directory, which is automatically created if you used truffle init to initialize your project, although you can of course create one after the fact. 

Go back to the SimpleStorage file directory we created in the previous lesson, “Intro to Truffle -- Part II”. To create your first test for SimpleStorage run the following:

    truffle create test SimpleStorage

As with the earlier create command this creates a simple scaffold which includes a reference to the actual underlying contract artifact. 

Following this you can simply run the following to run the test suite.

    truffle test

If there is no `development` network specified in `truffle-config.js`, the testing framework will temporarily spin up it’s own Ganache with which to run the tests against (which it subsequently tears down). This ensures it doesn’t pollute any existing ganache instances you might have running.

Let’s try running it again with a more meaningful test. Feel free to copy and paste the following into your own test and try running truffle test again.

    contract("SimpleStorage", function (/* accounts */) {
        it("should assert true", async function () {
        const simpleStorage = await SimpleStorage.deployed();
        await simpleStorage.set(42);
    
    return assert.equal(
      await simpleStorage.get(),
      42
        );
     });
    });


If all is going well, everything should pass again and you’ll see similar output to the following:

    Contract: SimpleStorage
    ✓ should assert true (132ms)
    1 passing (167ms)


As can be inferred from the above example, tests are typically written using the AAA (Arrange, Act, Assert) pattern. In addition, you can access the accounts array and access to the web3 library.

More detail can be found on tests [here](https://www.trufflesuite.com/docs/truffle/testing/testing-your-contracts).