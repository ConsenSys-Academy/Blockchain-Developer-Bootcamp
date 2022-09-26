# Ethereum .on Events

[![Open in CodeSandbox](https://img.shields.io/badge/Open%20in-CodeSandbox-blue?style=forthebadge-square&logo=codesandbox)](https://codesandbox.io/s/0x1-ethereum-on-events-start-qbhl91)

So… million dollar question: How does a user disconnect? It has to happen through MetaMask or whichever browser wallet they use. All they need to do is open MetaMask and click `Disconnect`. And just like that, they’ve revoked permissions that they initially granted to that dApp.

![disconnect-flow.png](../../img/../../img/S04/disconnect-flow.png)

<blockquote>
⛓️ We’re not logging in and out of a dApp, we’re simply granting and revoking permissions with MetaMask, and the dApp frontend needs to reflect that after the fact. But notice how there’s a louder call to action to ‘Connect’ than there is to ‘Disconnect’?
</blockquote>

If your user disconnects, the frontend, by default, remains unaffected— but that’s not what should happen. If they’re revoking permissions, the frontend should know to purge what information is held in the dApp state, like their balances or current account activity.

Under the hood, when your user disconnects, their browser wallet emits an event. This happens for a few other actions they could take like switching their account, or what network they’re on. With these events, comes the `.on` function, an event listener, that can handle those events and then execute logic based on what just happened. It takes the argument of an event as a string, so disconnecting would be one for example, and a callback function, which will dictate what logic should be executed next.

For an event like disconnecting, the Ethereum Provider API [documentation](https://docs.metamask.io/guide/ethereum-provider.html#disconnect) explains that:

> Once `disconnect`has been emitted, the provider will not accept any new requests until the connection to the chain has been re-established, which requires reloading the page.


As a precaution, MetaMask's Ethereum Provider API documentation also strongly suggests reloading the browser when the network is changed.

Looking back on the [CodeSandbox](https://codesandbox.io/s/0x0-metamask-connect-finish-0fkbhj) example from the last lesson, on load, the `useEffect` will fire off on every refresh. On disconnect, nothing will change. On a ***refresh*** after a disconnect, only then will the ‘Connect’ button will show up. 

Switching the account or the network would yield similar results. The `<Account />` component would still render— so long as you didn’t disconnect. On refresh, it would grab the account you just connected with. If your user is on a network where a target smart contract is not deployed, they won’t be able to execute any contract functionality, because it doesn’t exist on that network. *[Or what if they’re on a network that is set to be deprecated, like Rinkeby, Kovan, or Ropsten, they won’t be able to execute on-chain functionality reliably.](https://blog.ethereum.org/2022/06/21/testnet-deprecation){target=\_blank}* Each of those actions requires an event listener to update the state because they’re not being triggered from the dApp frontend directly, but rather through MetaMask.

## How To Build

We’re going to start off with a new CodeSandbox project. This one is slightly more advanced than the last one. You’ll recognize a few components like the `Connect` or the `InstallMetaMask` button, or `Account`. There are a few new additions:

- `/helpers`: The format address function has been moved to its own file here.
- `/constants`: You’ll find an object containing different network versions and names. Feel free to substitute your own to play around with.
- `/hooks`: You’ll find `useInjectedProvider` here, where we’ll create our own hook to call the Ethereum Provider API and hold our wallet state. The `useEffect` from the last lesson will live in this file, but it’ll be modified slightly.
- `/components`: There’s a `<Network />` component here that takes a prop of `network`, and that along with `<Account />` will sit inside of `<Card />`.

Open up `App.js`, and you’ll see a very familiar empty `<main></main>` element. `ethereum` is unpacked from the window, and `Card`, `Account`, and `Network` are imported but commented out.

At the moment, the `Connect` button doesn’t have any functionality. This will come from the `useInjectedProvider` hook we’ll be building out.

## Where does `useInjectedProvider` come from?

Custom hooks allow for code reusability, readability, and modularity. 

Our provider logic wouldn’t have to live inside `App.js` anymore. The reason for that is as a dApp codebase evolves, so does its state— to a level of absolute complexity that needs to be maintainable. That doesn’t include the components, the routing, or any unrelated API calls. In order to achieve that, we need to be able to extract that logic and keep it organized. That way anyone looking through your code will be able to know exactly where they can find the logic that handles connectivity and wallet state.

`App.js` can then be looked at as the file where our dApp structure will come together, its single purpose will be to import and house the components that need to render based on whatever condition is true at the moment.

If you open up `useInjectedProvider`, you’ll see `useEffect`, as well as `useState`, has been imported from React. Also being imported is `NETWORK_NAME`, which we’ll be using to hold onto the current network we’re connected to. Then `useInjectedProvider` is defined as a function with a `useEffect` that is empty.

```jsx
import { useEffect, useState } from 'react';

import { NETWORK_NAME } from '../constants/networks';

export const useInjectedProvider = () => {
	useEffect(() => {}, []);
	return {};
};
```

The first thing we’ll want to do is unpack `ethereum` from `window`. Then we’ll need to use the `useState` hook to hold onto the network name and our connected account like this:

```jsx
const { ethereum } = window;

const [networkName, setNetworkName] = useState('');
const [connectedAccount, setConnectedAccount] = useState('');
```

The updated `useInjectedProvider` hook should look like this:

```jsx
export const useInjectedProvider = () => {
  const { ethereum } = window;

  const [networkName, setNetworkName] = useState('');
  const [connectedAccount, setConnectedAccount] = useState('');
	useEffect(() => {}, []);
	return {};
};
```

Following the `useEffect` is a return block, at the moment it’s an empty object, but when we change `networkName` or `connectedAccount`, we’ll want to return that value to be consumed wherever we import this hook.

In the last lesson, we used an asynchronous IIFE to request the accounts that we connected with, and then set the state of the connected account to the account returned.

Then, we’ll want to get the network we’re on. We can achieve this by grabbing the chain ID like so:

```jsx
const chainId = await ethereum.request({ method: 'eth_chainId' });
```

This will give us the hexadecimal string representing the current chain ID. From there, when we want to set `networkName` to the value of `NETWORK_NAME[chainId]`. This is what the async IIFE should look like:

```jsx
(async () => {
  try {
    const chainId = await ethereum.request({ method: 'eth_chainId' });
    const [connectedAccount] = await ethereum.request({
      method: 'eth_accounts',
    });

    setNetworkName(NETWORK_NAME[chainId]);
    setConnectedAccount(connectedAccount);
  } catch (e) {
    console.log(e);
  }
})()
```

And that should work. Almost. *We’re not done here yet.* We still have to expose those values in state to be consumed by the rest of our dApp. But we also need to define our connect functionality too, fear not, it’s exactly as it was in the last lesson. Because we unpacked `ethereum` from the window inside `useInjectedProvider`, we’re able to use that for our connect function, that we can define right below where we hold `networkName` and `connectedAccount` in state.

```jsx
const connectWallet = async () => {
		try {
			const [account] =
				await ethereum.request({ method: 'eth_requestAccounts' })
			setConnectedAccount(account);
		} catch (e) {
			console.log(e);
		}
	};
```

Inside `return {}`, we’ll need to add `ethereum`, `connectWallet`, `networkName`, and `connectedAccount`. *Almost there.*

Switch back to `App.js`. Yes, we have our `InstallMetaMask` and `Connect`, but the connect button won’t work 🤔. If you open up `Connect.js`, you’ll see it’s expecting the prop of a function, `connectWallet`, to be passed in. Same with `Account` and `Network`; both of those components are expecting a prop to be passed in— and we’re already holding onto those in our hook 🤔.

We don’t want this hook to be referenced in every component file. Doing so would result in the async IIFE being called multiple times just to get those values. Instead, what we want is to reference it once in `App.js`, and from there, we can pass in those values as props to the components that are expecting them.

The way that we can grab those values is by importing `useInjectedProvider`, and unpacking them like this:

```jsx
const { ethereum, connectWallet, connectedAccount, networkName } = useInjectedProvider()
```

The ternary conditional inside main should feel very familiar here, show the `InstallMetaMask` button if `ethereum` isn’t detected, show the `Connect` button if it is, and if `connectedAccount` is true… show both `Account` and `Network`? 

<blockquote>
⚛️ `Account` and `Network` are sibling elements that need to be wrapped either by a parent component like `Card` or a fragment.

</blockquote>

The `Card` component will wrap around both `Account` and `Network` like this:

```jsx
<Card>
	<Account account={connectedAccount} />
	<Network network={networkName} />
</Card>
```

Your updated ternary should look like this:

```jsx
{connectedAccount ? (
	<Card>
		<Account account={connectedAccount} />
		<Network network={networkName} />
	</Card>
) : ethereum ? (
	<Connect connectWallet={connectWallet} />
) : (
	<InstallMetaMask />
)}
```

## Firing off Events

Disconnecting, switching networks or accounts, won’t trigger the changes we’re looking for, just yet. But setting up `useInjectedProvider` the way we did will allow us to do that now.

Back in `useInjectedProvider`, right beneath where the `try/catch` block, we should have `ethereum.on()` for as many events as we need to listen for. The updated async IIFE should include this:

```jsx
	
ethereum.on('disconnect', () => {
	window.location.reload();
});

ethereum.on('chainChanged', () => {
	window.location.reload();
});

ethereum.on('accountsChanged', () => {
	window.location.reload();
});
```

Try switching your account. Notice the refresh, and how your account updates… right away? What about network? That too? And disconnect? You should see the connect button, if you don’t have any accounts connected. For a smaller example like this, reloading the window is the bare minimum we should prompt. When reloaded, the hook gets called again as all the components are rendered to the DOM, and we have fresh new state to pass in.