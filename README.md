Vennd
=====

Vennd is a general purpose gateway service between bitcoind (or any other bitcoind API compatible alt-coin) and Counterparty. In its simplest form, Vennd allows you to create a gateway to frictionlessly between your alt-coin and trade it on the Counterparty distributed exchange.

Feel free to contact me jeremy@vend.io on just about anything.

* VenndNativeFollower - Application which connects to single bitcoind instance
* CounterpartyFollower - Application which connects to the Counterparty API. A single CounterpartyFollower instance can be configured to listen to multiple service addresses and assets
* PaymentProcessor - Application to process Bitcoin and Counterparty payments
* PaymentAuthorizer - TBA - Application to manually authorize payments


Pre-requisites
==============
* Bitcoin installed and blockchain synchronised with txindex=1 http://counterpartyd-build.readthedocs.org/en/latest/SettingUpBitcoind.html
* Counterpartyd installed as per http://counterpartyd-build.readthedocs.org/en/latest/BuildingFromSource.html#on-linux


Requirements
============

Vennd was developed and tested on Ubuntu 12.04 LTS. The following is the recommended specifications for a server running Vennd:

* 4 GB of RAM or higher, SSD with at least 128GB free space
* Ubuntu 12.04 LTS
* Groovy 1.89 or higher. Groovy 2.3 is recommended because of JSON parsing performance improvements. It is recommended to run Vennd with the --indy parameter to enable InvokeDynamic support (http://groovy.codehaus.org/InvokeDynamic+support).
* Oracle JDK 1.7 or higher


Configuration
=============

It is recommended that all of the processes for a single instance of a vending machine runs in the same directory. The sqlite database must be shared between each of the processes and the user permissions can be restricted to a single directory.

Sample configuration to set up a gateway service for an alt-coin based upon Bitcoin.

**VenndNativeFollower.ini**
```
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


Running Vennd
==============

