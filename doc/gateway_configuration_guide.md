Sample configuration to set up a gateway service for an alt-coin based upon Bitcoin.

**VenndNativeFollower.ini**
```ini
testMode = false

inceptionBlock = 300043         // The block to start listening for service requests -1. ie start listening on block 300044
feeAmountPercentage = 0.1       // Fee amount in percentage for the vending machine to take. eg 0.1%
txFee = 0.0003172               // Fee in absolute value to take for the costs of Counterparty transaction transmission
confirmationsRequired = 3

listenerAddress = "LR5grCQB8FaxueX2UtvUbURho1qHuQrtFZ"

inAssetName = "LTC"
outAssetName = "LITECOINS"

database.name = "ltcGateway.db"

sleepIntervalms = 1000
```


**BitcoinAPI.ini**
```
rpcURL = "http://127.0.0.1:8332"
rpcUser = "rpc"
rpcPassword = "supernova"
```


**CounterpartyFollower.ini**
```
testMode = false

inceptionBlock =  300043
feeAmountPercentage = 0.1
txFee = 0.0001
confirmationsRequired = 3

asset.LITECOINS.counterpartyAssetName = "LITECOINS"
asset.LITECOINS.nativeAssetName = "LTC"
asset.LITECOINS.counterpartyAddress = "1M72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd"
asset.LITECOINS.nativeAddress = "LR5grCQB8FaxueX2UtvUbURho1qHuQrtFZ"
asset.LITECOINS.txFee = 0.0001
asset.LITECOINS.feePercentage = 0.1
asset.LITECOINS.mappingRequired = false

database.name = "ltcGateway.db"
sleepIntervalms = 1000
```


**CounterpartyAPI.ini**
```
counterparty.rpcURL = "http://127.0.0.1:4000"
counterparty.rpcUser = "xcpRpc"
counterparty.rpcPassword = "NYNEX"
counterparty.counterpartyTransactionEncoding = "multisig"
counterparty.counterpartyMultisendPerBlock = true
```


**PaymentProcessor.ini**
```
testMode = false

bitcoin.walletPassphrase = "Imdyingtocatchmybreath"
walletUnlockSeconds = 30

database.name = "ltcGateway.db"
database.busyTimeout = 2000

sleepIntervalms = 60000
```
