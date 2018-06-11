# IPSUM Windows and Linux Wallet - Linux VPS Masternode Instructions

## Requirements:
* A local Masternode Wallet with the required Masternode collateral (5000 IPS).
* A GNU/Linux VPS with a Static IP Address referred as __<your vps IP>__ in this document.

* For this guide we are using Ubuntu 16.04 on the VPS, but any distro should do as the executables are statically linked. 
* A 25GB SSD and 1000GB bandwidth will suffice (suggested vultr or digital ocean; use those referral links to support IPS: [vultr](https://www.vultr.com/?ref=7426211) and [Digital Ocean](https://m.do.co/c/0d726bd8cfdc)).
* Select IPV6 and Private Networking. I will leave DDoS and Automatic backups to you. 
* Leave SSH Keys and Startup Script blank.


## Setup Wallet:

* Download the latest wallet for your OS [Releases](https://github.com/ipsum-network/ips/releases)
* For Windows users:
  * run the installer, and leave everything as default.
* For GNU/Linux users:
  * untar the archive where you please (you may copy ipsd and ips-cli in /usr/local/bin for easy access)
* Run the qt, then close it again.

### Syncing

* Open the ips.conf file. It can be found in C:/Users/<Your User>/AppData/Roaming/IPS.
* Copy the addnodes from [here](https://github.com/ipsum-network/seeds/blob/master/README.md) into this file, then save it.
* Re-open your ips-qt. It will now sync much more quickly.

### Addresses

* Whilst it is syncing, create two addresses in the receiving tab. For one, I always use the name of exchange I have purchased the coin from. In this instance it will be called “Graviex”. The other will be called MN1 (For your masternode).

### Wallet Adjustments

* Through options, enable Coin Control, as well as the Masternodes tab (under “Wallet”). As this will require a wallet restart, you may as well go through and change things as you see fit. i.e. Decimals Digits, Interface Theme, and Map Port using UPnP.
* Once this is complete, encrypt your wallet. Once encryption is complete, your wallet will close. Reopen it.

### Exchange

* Open your exchange, and transfer at least 5001 coins to the “Graviex” address. Be sure to account for exchange fees.
* You should receive your coins almost instantly. Please wait for them to confirm before proceeding.

### Coin Control

* Coin Control is how we will create a transaction of *exactly* 5000 IPS. This is necessary, as any other amount is ineligible for a MN status.
* Copy your MN1 address to the clipboard.
* Open the send tab.
* Choose “Inputs” at the top left of the window.
* It should have “List Mode” checked. If not, check it.
* You will see your transaction under the label Graviex. Check it on the left hand panel and click OK.
* Paste your MN1 address in the “Pay To” section. The label “MN1” should automatically be displayed.
* Input 5000 into the “Amount” section.
* Press send, and pay any transaction fees.
* After 2 minutes, open Coin Control again. You should see a transaction of exactly 5000 IPS under MN1. Wait for it to receive 15 confirmations before the next step.

### Masternode Info

* If you wallet is locked, unlock it.
* From the tools menu, open the __Debug Console__ and __open the masternode configuration file__.
* In your masternode configuration file, input a new line:

```MN1 <your vps IP>:19551 ```

* In the debug console, input the command:

```masternode genkey```

* This gives you your <masternode priv key>. Copy it in your masternode configuration file after 22331 (keep a space between 22331 and the masternode priv key) and keep your masternode priv key secret.
* Be sure the 5000IPS payment to MN1 have reached at least 15 confirmations before inputing the following command:
  
```masternode outputs```

* This gives you a <transaction hash> (long string of nonsense) and an <index> (0 or 1)
  Add this to your masternode configuration file which should now look like this:
```MN1 <your vps IP>:22331 <masternode priv key> <transaction hash> <index>```
  which might be something similar to the following line:
```MN1 111.222.111.222:19551 df1265465465432KSJBFNSKJ aLJKHVBSFDLJHGbcdeSFKJSFf654321abcdef321654abcdef321654 1```
* Save and close your masternode configuration file.
* Close the debug console.

### That is all you need to do with your Wallet for now.
