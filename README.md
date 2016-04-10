# easy-bitcoin-js
A simple module with basic Bitcoin operations using [bitcoinjs-lib](https://github.com/bitcoinjs/bitcoinjs-lib) and [Blockchain.info](https://blockchain.info) API.

### How to use

```javascript
var easyBtc = require('easy-bitcoin-js');
```

### Supported operations

#### easyBtc.newWallet()
Creates a random new wallet.

##### Returns
- [Object] `$$ecPair`: bitcoinjs keyPair object
- [String] `wif`: private key in WIF format
- [String] `address`: public key (address)

#### easyBtc.getWallet(address)
Gets information from an address in the blockchain.
  
##### Arguments
- [String] `address`: the address of the wallet.

##### Returns
- [Promise] A Q promise with the HTTP result. JSON result is resolved to `resolved.data`.

> **Tip**: the returned `final_balance` property of the transaction JSON contains the wallet's balance.

#### easyBtc.newTransaction(fromWIF, txHashOrigin, toAddress, value)
Creates a transaction.

##### Arguments
- [String] `fromWIF`: private key in WIF format of the origin wallet.
- [String] `txHashOrigin`: the last transaction hash to the origin wallet.
- [String] `toAddress`: the public key (address) of the destination wallet.
- [Number, int] `value`: the amount to transfer in uBTC (microbitcoins).

##### Returns
- [Object] `$$tx`: bitcoinjs transaction object.
- [String] `hex`: the transaction hex script to push into the blockchain.

#### easyBtc.pushTransaction(hexTx)
Pushes a transaction to the blockchain.

##### Arguments
- [String] `hexTx`: the transaction hex script to push into the blockchain.

##### Returns
- [Promise] A Q promise with the HTTP result.

#### easyBtc.getTransaction(txHash)
Gets a transaction from the blockchain.

##### Arguments
- [String] `hexTx`: the transaction hex script to push into the blockchain.

##### Returns
- [Promise] A Q promise with the HTTP result. JSON result is resolved to `resolved.data`.

> **Tip**: the returned `block_height` property of the transaction JSON is present and greater than zero if the transaction is already confirmed. If this property is not present in the JSON or equal to or less than zero, the transaction was not already confirmed.