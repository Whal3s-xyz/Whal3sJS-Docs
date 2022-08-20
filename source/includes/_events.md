# Events
The Whal3s Utility dispatches the following events:
You can connect to them by adding an event listener.
```javascript
utility.addEventListener('transactionHash', (transactionHash) => console.log('transactionHash: ' + transactionHash))
```


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
