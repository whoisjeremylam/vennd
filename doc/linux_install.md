Linux Installation Guide
========================
Vennd was developed and targeted to run on Ubuntu 12.04 LTS server.

Update Server
Update the Ubuntu server and install dependencies
```
sudo apt-get update
sudo apt-get install unzip
sudo apt-get install python-software-properties
sudo apt-get install git-core python3
```

Install Groovy
==============
The version of Groovy that is contained in the default repository is 1.8.6.

```
sudo apt-get install groovy
```

Or install Groovy 2.3.0 (preferred)

```
wget http://dl.bintray.com/groovy/maven/groovy-binary-2.3.0.zip
unzip groovy-binary-2.3.0.zip
```

Download Sqlite
===============
```
cd ~
mkdir -p .groovy/lib
cd ~/.groovy/lib
wget https://bitbucket.org/xerial/sqlite-jdbc/downloads/sqlite-jdbc-3.7.2.jar
```

Install Oracle JDK 7
====================
The easiest way to install Oracle JDK 7 on Ubuntu is via a PPA repository http://www.webupd8.org/2012/01/install-oracle-java-jdk-7-in-ubuntu-via.html

```
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java7-installer
```

Download Vennd
==============

```
git clone https://github.com/whoisjeremylam/vennd
```
