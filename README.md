Vennd
=====

Vennd is a general purpose gateway service between bitcoind (or any other bitcoind API compatible alt-coin) and Counterparty. In its simplest form, Vennd allows you to create a frictionless gateway between your alt-coin blockchain and trade it on the Counterparty distributed exchange.

Feel free to contact me jeremy@vend.io on just about anything.


The components of Vennd:
* VenndNativeFollower - Application which connects to single bitcoind instance
* CounterpartyFollower - Application which connects to the Counterparty API. A single CounterpartyFollower instance can be configured to listen to multiple service addresses and assets
* PaymentProcessor - Application to process Bitcoin and Counterparty payments
* PaymentAuthorizer - TBA - Application to manually authorize payments


Pre-requisites
==============
* Bitcoin installed and blockchain synchronised with txindex=1 as per http://counterpartyd-build.readthedocs.org/en/latest/SettingUpBitcoind.html
* Counterpartyd installed as per http://counterpartyd-build.readthedocs.org/en/latest/BuildingFromSource.html#on-linux


Requirements
============
Vennd was developed on Ubuntu 12.04 LTS and is the preferred platform to run Vennd. However, Windows 7 or higher is also supported. The following are the recommended specifications for a server running Vennd:

* Windows 7 or higher or Ubuntu 12.04 LTS
* 4 GB of RAM or higher, SSD with at least 128GB free space
* Groovy 1.89 or higher. Groovy 2.3 is recommended because of JSON parsing performance improvements. It is recommended to run Vennd with the --indy parameter to enable InvokeDynamic support (http://groovy.codehaus.org/InvokeDynamic+support).
* Oracle JDK 1.7 or higher


Installation
============
The Linux installation guide can be found at https://github.com/whoisjeremylam/vennd/doc/linux_install.md
The Windows installation guide can be found at https://github.com/whoisjeremylam/vennd/doc/windows_install.md


Configuration
=============

It is recommended that all of the processes for a single instance of a vending machine runs in the same directory. The sqlite database must be shared between each of the processes and the user permissions can be restricted to a single directory.

How to configure a gateway service for your Bitcoin compatible alt-coin https://github.com/whoisjeremylam/vennd/blob/master/doc/gateway_configuration_guide.md

How to configure a simple vending machine
https://github.com/whoisjeremylam/vennd/blob/master/doc/vendingmachine_configuration_guide.md


Running Vennd
==============
Start 
