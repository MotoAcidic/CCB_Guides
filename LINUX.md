# Linux VPS IPSUM Daemon Installation Guide

## Connect to your Linux VPS over SSH

  * Use your favorite terminal application on Linux or Putty/Bitvise clients on Windows
  * Connect to a terminal session with the Linux VPS
  
## Update your system to the latest

  * From the terminal session, run the following commands
  ```
  sudo apt-get update
  sudo apt-get upgrade
  ```
  
## Download the CCB Linux Daemon

  * From the terminal session, run the following command
  ```
  wget https://github.com/CryptoCashBack-Hub/CCB/releases/download/v1.0.0.1/CryptoCashBack-Linux.tar.gz
  ```
  * From the terminal session, run the following command
  ```
  tar -xvf CryptoCashBack-Linux.tar.gz
  ```
    * From the terminal session, run the following command
  ```
  wget https://github.com/CryptoCashBack-Hub/CCB/releases/download/v1.0.0.1/CryptoCashBack-Linux-binaries.tar.gz
  ```
  * From the terminal session, run the following command
  ```
  tar -xvf CryptoCashBack-Linux-binaries.tar.gz
  ```
  
## Install IPSUM Linux Daemon Runtime Dependencies

  * From the terminal session, run the following commands
  ```
  sudo apt autoremove -y && sudo apt-get update
  sudo apt-get install -y libzmq3-dev libminiupnpc-dev libssl-dev libevent-dev
  sudo apt-get install -y build-essential libtool autotools-dev automake pkg-config
  sudo apt-get install -y bsdmainutils software-properties-common
  sudo apt-get install -y libboost-all-dev
  sudo add-apt-repository ppa:bitcoin/bitcoin -y
  sudo apt-get update
  sudo apt-get install -y libdb4.8-dev libdb4.8++-dev
  ```
  
## Create your IPSUM Linux Daemon configuration file

* From the terminal session, run the following commands
```
mkdir -p ~/.cryptocashback
nano ~/.cryptocashback/cryptocashback.conf
```

* Now add the following lines to this file, replacing any < > field with your information
  * Note: If your setting up a Linux Hot/Cold Wallet, comment out the masternode entries
```
rpcuser=<rpcusername>
rpcpassword=<rpcpassword>
rpcport=19552
listen=1
server=1
daemon=1
staking=0
rpcallowip=127.0.0.1
logtimestamps=1
#masternode=1
port=19551
externalip=<externalip>:19551
#masternodeprivkey=<masternode private key>
```

* Get the latest node seeds from [here](https://github.com/CryptoCashBack-Hub/CCB_Guides/blob/master/Seeds)
* Copy and paste the addnode lines into the bottom of this file
* Save and Exit

## Now make the swap file
* From the terminal session, run the following commands
```
dd if=/dev/zero of=/swapfile bs=1024 count=2M
```
```
chmod 600 /swapfile
```
```
 mkswap /swapfile
```
```
 swapon -a /swapfile

```

## Start the CCB Linux Daemon

* From the terminal session, run the following commands
```
start CryptoCashBack.service
```

## Wait for the CCB Linux Daemon to sync

* From the terminal session, run the following commands
```
watch cryptocashback-cli getinfo
```
* Compare the "Block Height" value with the latest from the [IPSUM block explorer](https://explorer.ipsum.network/). When those are the same, your daemon is synchronized 

