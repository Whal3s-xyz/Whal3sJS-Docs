---
title: Whal3s Javascript Library - Reference

language_tabs: # must be one of https://git.io/vQNgJ

- javascript

[//]: # (  - ruby)

[//]: # (  - python)

[//]: # (  - javascript)

toc_footers:

- <a href='https://form.typeform.com/to/bZS0tV6C?typeform-source=docs.whal3s.xyz'>Sign Up for Whal3s</a>
- <a href='https://github.com/Whal3s-xyz'>Whal3s repositories</a>

[//]: # (includes:)

[//]: # ()
[//]: # (- events)

search: true

code_clipboard: true

meta:

- name: Whal3s Javascript library documentation
  content: Documentation for the Whal3s Javascript library

---

# Introduction

Welcome to the Whal3s JavaScript library documentation. This documentation shows you how to implement your utility into
your frontend.

# Installation

First you need to get Whal3sJS into your project. This can be done using the following methods:

* npm: `npm intall whal3sjs`
* yarn: `npm add whal3sjs`

After that you need to create a Whal3s instance.

```javascript
import Whal3s from 'whal3sjs'
//...
const whal3s = new Whal3s();
```

# Initialize

To use your utility, you need to initialize it by using the Whal3s instance.

```javascript
    const utility = whal3s.getUtility('your-utility-id')
utility.init()
```

# Connect wallet

Connection to wallet is the first step to set up before triggering any user transaction.
Wallet connection can be initialized with `connectWallet()`. This function returns a promise and throws an error if
there was any.

```javascript
utility.connectWallet()
  .then(() => console.log('Wallet connection'))
  .catch((error) =>console.log('An error occured'))
```
# Use Utility

## Execute Utility

If your utility contains frontend actions like executing a transaction or calling a smart contract method, you have to use `performAction()`.
This function returns a Promise as well.

```javascript
utility.performAction()
  .then(() => console.log('Action successfully executed'))
  .catch((error) =>console.log('There was an error during user journey'))
```


## Validation
If the wallet is connected and you want to validate the current address, you can use `validateWalletAddress(address:optional)` to do that.
If no address is given, the current connected walled will be used. Otherwise you can validate any other wallet address.

```javascript
utility.validateWalletAddress(address).then((response))
```

The response contains the following three parameters:

````json
{
  "valid": "boolean",
  "maxEngagementsReached": "boolean",
  "engagements": "array of engagements"
}
````

## Attributes
You can access several utility attributes to make life easier. E.g. `utility.selectedAccount`

Attribute | Meaning
---------- | -------
isInitialized | Boolean -- Your utility is ready to use.
selectedAccountIsValid | Boolean -- The current connected wallet matches utility condition.
engagementsCount | Integer -- Total number of engagements for utility.
maxEngagements | Integer -- Maximum allowed number of engagements for this utility.
maxEngagementsPerWallet | Integer -- Maximum allowed number of engagements for this utility per wallet.
id | String -- Id of utility.
selectedAccount | String -- Current connected wallet address.


# Engagements

## Get engagements
To get all engagements for an utility, you can simply call `fetchEngagements()`. This promise returns you an array of engagements.

```javascript
utility.fetchEngagements().then((engagements) => {});
```


# Events
The Whal3s Utility dispatches the following events:
You can connect to them by adding an event listener.
## Event listener
Add eventlistener by using `addEventListener(name, callback)`.

````javascript
utility.addEventListener('transactionHash', (transactionHash) => console.log('transactionHash: ' + transactionHash))
````

## All events
Event | Meaning
---------- | -------
initialized | Initialized -- Your utility is ready to use.
initializationFailed | Initialization failed -- There was an error while initializing utility. Activate debug mode to get further details.
networkSwitch | Network switched -- Changed network to desired one
networkSwitchFailed | Network switched -- There was an erro while switching network
sending | Sending -- Sending transaction data to web3 provider.
sent | Sent -- Web 3 provider received transaction.
transactionHash | Transaction hash - Transaction was commited to the network. Transaction hash in callback.
confirmation | Confirmation -- The transaction got confirmed!
error | Error -- There was an error while validation the transaction.
done | Done -- Transaction process done
estimateGasError | Estimate gas error -- Error while fetching gas amount. Might be due to low token ballance.
gasPriceError | Done -- Error while fetching gas price. Network might not be reachable.
