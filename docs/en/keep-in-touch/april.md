# Saving Failed Transactions (April 2020)

Since node version 1.2.4, after activation of feature #15 “Ride V4, VRF, Protobuf, Failed transactions” the transaction validation procedure is changed.

* Invoke script transactions and exchange transactions are saved on the blockchain and a fee is charged for them even if the dApp script or the asset script failed, provided that the sender's signature or account script verification passed.

   However if the callable function failed with an error or [throwing an exception](/en/ride/exceptions) before the [complexity](/en/ride/base-concepts/complexity) of performed calculations exceeded the [threshold for saving failed transactions](/en/ride/limits/), the transaction is rejected and the fee is not charged.

* A fee for the invoke script transaction cannot be funded by transfer from dApp to the transaction sender. If sender's balance is insufficient to pay the fee, dApp script is not executed.

[More details about transaction validation](/en/blockchain/transaction/transaction-validation)

In the JSON representation of the transaction, the `applicationStatus` field is added, which contains the result of validation:
* `succeeded` – the transaction is successful.
* `script_execution_failed` – dApp script or asset script failed. Such a transaction doesn't entail changes in balances (other than charging a fee) and account data storages.

Failed transactions are implemented in the Waves protocol and are supported both by [Node Scala](https://github.com/wavesplatform/Waves/releases) and [Node Go](https://github.com/wavesplatform/gowaves/releases/), as well as by the following Waves tools.

## Node API

Added the `applicationStatus` field to the following endpoints:

   * `/blocks/{id}`
   * `/blocks/address/{address}/{from}/{to}`
   * `/blocks/at/{height}`
   * `/blocks/last`
   * `/blocks/seq/{from}/{to}`
   * `/debug/stateChanges/address/{address}/limit/{limit}`
   * `/debug/stateChanges/info/{id}`
   * `/transactions/address/{address}/limit/{limit}`
   * `/transactions/info/{id}`
   * `/transactions/status`

**How to access**: use the pool of Waves nodes with public API:
* Mainnet: <https://nodes.wavesnodes.com/>
* Testnet: <https://nodes-testnet.wavesnodes.com/>
* Stagenet: <https://nodes-stagenet.wavesnodes.com/>

See also [the list of Node API changes in release 1.2](/en/keep-in-touch/release-notes#rest-api-updates)

## Libraries

### waves-transactions

The `waitForTx` and `waitForTxWithNConfirmations` return Promise of transaction which is resolved when the transaction is added to the blockchain. Now the `applicationStatus` field has been added to the transaction.

**How to access**: install the latest version of the library using the command

```bash
npm i @waves/waves-transactions@latest
```

[waves-transactions documentation](https://wavesplatform.github.io/waves-transactions/)

### node-api JS

The `fetchInfo` and `fetchStatus` functions now support the `applicationStatus` field.

**How to access**: install the latest version of the library using the command

```bash
npm i @waves/node-api-js@latest
```

[node-api JS on Github](https://github.com/wavesplatform/node-api-js/)

## Waves Explorer

* Transactions with failed dApp script or asset script results are displayed. In the list of transactions, they are marked with ![](./_assets/stop.png) icon.

   ![](./_assets/failed-transaction.png)

* For invoke script transactions the dApp script result is displayed as a table.

**How to access**: go to <https://wavesexplorer.com/>.

[All changes in Waves Explorer](/en/keep-in-touch/release-notes#waves-explorer)

## Waves IDE

The `applicationStatus` field for transactions that is added to the blockchain is now supported in JavaScript console and in tests.

Please note: tests now need to check not only that the transaction is added to the blockchain, but also the success of the script.

**How to access**: go to <https://waves-ide.com/>.

## Surfboard

The `applicationStatus` field is now supported for transactions added to the blockchain.

**How to access**: install the latest version using the command

```bash
npm i @waves/surfboard@latest
```

[Surfboard on Github](https://github.com/wavesplatform/surfboard)

## Dapp Ui

For the invoke script transaction, in addition to the transaction status on the blockchain, the status of script execution is displayed.

**How to access:** go to <http://waves-dapp.com/>.

## Ride limitations

The maximum complexity of account script and verifier function of dApp script is changed to 2000 for new scripts, regardless of the Standard library version.

The maximum complexity of asset script and callable function of dApp script remains 4000.
