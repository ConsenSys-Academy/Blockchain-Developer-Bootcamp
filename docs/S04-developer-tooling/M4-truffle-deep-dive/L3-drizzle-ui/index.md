# Wire up the React app with Drizzle
*Note that Drizzle is currently not actively maintained by Truffle, although the team is always happy to provide best-endeavors support. In addition, ConsenSys is actively hiring for front-end focused roles and/or folks interested in assisting with maintenance. Feel free to reach out if this might of interest!

Before we go further, let's start our React app by running the follow command inside our client directory:

    npm install @drizzle/store

    npm start


This will serve the front-end under `localhost:3000` so open that up in your browser.

Note: Make sure to use an incognito window if you already have MetaMask installed (or disable MetaMask for now). Otherwise, the app will try to use the network specified in MetaMask rather than the develop network under `localhost:9545`.

If the default Create-React-App page loaded without any issues, you may proceed.

## Setup the store
The first thing we need to do is to setup and instantiate the Drizzle store. We are going add the following code to client/src/index.js:

    import drizzle functions and contract artifact
    import { Drizzle } from "@drizzle/store";
    import MyStringStore from "./contracts/MyStringStore.json";

    let drizzle know what contracts we want and how to access our test blockchain
    const options = {
    contracts: [MyStringStore],
    web3: {
        fallback: {
        type: "ws",
        url: "ws://127.0.0.1:9545",
        },
    },
    };
    setup drizzle
    const drizzle = new Drizzle(options);



First, we imported the tools from Drizzle as well as the contract definition.

We then built our options object for Drizzle, which in this case is just specifying the specific contract we want to be loaded by passing in the JSON build artifact.

And finally, we created the drizzleStore and used that to create our drizzle instance which we will pass in as a prop to our App component.

Once that is complete, your index.js should look something like this:

    import React from 'react';
    import ReactDOM from 'react-dom';
    import './index.css';
    import App from './App';
    import * as serviceWorker from './serviceWorker';

    import drizzle functions and contract artifact
    import { Drizzle, generateStore } from "@drizzle/store";
    import MyStringStore from "./contracts/MyStringStore.json";

    let drizzle know what contracts we want and how to access our test blockchain
    const options = {
    contracts: [MyStringStore],
    web3: {
        fallback: {
        type: "ws",
        url: "ws://127.0.0.1:9545",
        },
    },
    };
    setup the drizzle store and drizzle
    const drizzle = new Drizzle(options);
    ReactDOM.render(<App drizzle={drizzle} />, document.getElementById('root'));




Note again that the drizzle instance is passed into the App component as props.

# Drizzle Components
Drizzle maintains a library of React components for commonly used dapp functions. For example, generating input forms for contracts.
Components

## LoadingContainer

This components wraps your entire app (but within the DrizzleProvider) and will show a loading screen until Drizzle, and therefore web3 and your contracts, are initialized.

    loadingComp (component) 
The component displayed while Drizzle intializes.

    errorComp (component) 
The component displayed if Drizzle initialization fails.

## ContractData
    contract(string, required)
Name of the contract to call.

    method (string, required
Method of the contract to call.

    methodArgs (array) 
Arguments for the contract method call. EX: The address for an ERC20 balanceOf() function. The last argument can optionally be an options object with the typical from, gas and gasPrice keys.

    hideIndicator(boolean) 
If true, hides the loading indicator during contract state updates. Useful for things like ERC20 token symbols which do not change.

    toUtf8 (boolean) 
Converts the return value to a UTF-8 string before display.

    toAscii (boolean) 
Converts the return value to an Ascii string before display.

## ContractForm

    contract (string, required
Name of the contract whose method will be the basis the form.

    method (string, required) 
Method whose inputs will be used to create corresponding form fields.

    sendArgs (object) 
An object specifying options for the transaction to be sent; namely: from, gasPrice, gas and value. Further explanation of these parameters can be found here in the web3 documentation.

    labels (array) 
Custom labels; will follow ABI input ordering. Useful for friendlier names. For example "_to" becoming "Recipient Address".
