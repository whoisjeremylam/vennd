Create a gateway to trade an alt-coin on the Counterparty DEX
=============================================================

Prior to creating the gateway, first create an asset in Counterparty which represents your alt-coin.

Each of the following INI files must be edited. Included below is a sample configuration which sets up a gateway service for Litecoin.


**VenndNativeFollower.ini**

VenndNativeFollower is the process which connects to the Bitcoin API compatible alt-coin. It 'listens' if your alt-coin was sent to a payment address. The coins from the payment address is then swept into the central holding address (listenerAddress).

```ini
testMode = false

inceptionBlock = 300043         // The block to start listening for service requests -1. ie start listening on block 300044
feeAmountPercentage = 0.1       // Fee amount in percentage for the vending machine to take. eg 0.1%
txFee = 0.0003172               // Fee in absolute value to take for the costs of Counterparty transaction transmission
confirmationsRequired = 3

listenerAddress = "LR5grCQB8FaxueX2UtvUbURho1qHuQrtFZ"    // The address which the gateway will receive the native alt-coin
paymentAddress = "1M72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd"     // The address which the gateway will dispense the Counterparty asset

inAssetName = "LTC"                                       // A label representing the asset name for the alt-coin
outAssetName = "LITECOINS"                                // This must match the name of the asset you created in Counterparty

database.name = "ltcGateway.db"                           // The filename of the embedded SQL database

sleepIntervalms = 1000                                    // Interval to sleep between checking for new blocks
```


**BitcoinAPI.ini**

This contains connection information to connect to the API of your alt-coin. Please refer to the alt-coin .conf file.
```ini
rpcURL = "http://127.0.0.1:8332"
rpcUser = "rpc"
rpcPassword = "supernova"
```


**CounterpartyFollower.ini**

CounterpartyFollower is the process which connects to counterpartyd and 'listens' if your Counterparty asset was sent on a payment address.
```ini
testMode = false

inceptionBlock =  300043
confirmationsRequired = 3

asset.LITECOINS.counterpartyAssetName = "LITECOINS"                           // Name of the asset you created in Counterparty
asset.LITECOINS.nativeAssetName = "LTC"                                       // Name of your alt-coin
asset.LITECOINS.counterpartyAddress = "1M72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd"    // The address which the gateway will receive the Counterparty asset
asset.LITECOINS.nativeAddress = "LR5grCQB8FaxueX2UtvUbURho1qHuQrtFZ"          //The address which the gateway will send your alt-coin
asset.LITECOINS.txFee = 0.0001
asset.LITECOINS.feePercentage = 0.1
asset.LITECOINS.mappingRequired = true                                        // Must be true if the Counterparty/Bitcoin address is not the same as the alt-coin addressing scheme.

database.name = "ltcGateway.db"
sleepIntervalms = 1000
```


**CounterpartyAPI.ini**

Connection details to connect to counterpartyd. Please check your counterpartyd.conf file.
```ini
counterparty.rpcURL = "http://127.0.0.1:4000"
counterparty.rpcUser = "xcpRpc"
counterparty.rpcPassword = "NYNEX"
counterparty.counterpartyTransactionEncoding = "multisig"                     // Encoding scheme for Counterparty transactions
counterparty.counterpartyMultisendPerBlock = true                             // Enable more than 1 tx per block
```


**PaymentProcessor.ini**
```ini
testMode = false

bitcoin.walletPassphrase = "Imdyingtocatchmybreath"
walletUnlockSeconds = 30

database.name = "ltcGateway.db"
database.busyTimeout = 2000

sleepIntervalms = 60000
```
