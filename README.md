# Doginals Minter (Ubuntu Version)

A minter and protocol for inscriptions on Dogecoin with local full dogecoin node. 

## ⚠️⚠️⚠️ Important ⚠️⚠️⚠️ 

This is a fork of fork by https://github.com/Puckapao/doginals
It removed the use of dogechain.info and switch `doginals.js` to use your own dogecoin node rpc instead.
There might be some bugs, so please using with caution.

### Changes

- New wallet created will be add to dogecoin-cli watchlist using importaddress method.
- Wallt syncing will use dogecoin-cli's listunspent method to collect UTXOs (max at 9999999 utxos, more than that might have to change your own maxUtxo at line 25).
- Please sync the wallet everytime before doing some mint and split. 

```
node . wallet sync
```
- Added files `.env.sample` and `dogi.json`

## Setup Guide

Clone the repository
```
cd $HOME
git clone https://github.com/themoonether/doginals.git
```

Dependency requirements

### NodeJS
Please head over to (https://github.com/nodesource/distributions#using-ubuntu) and follow the installation instructions.

```
curl -fsSL https://deb.nodesource.com/setup_21.x | sudo -E bash - &&\
sudo apt-get install -y nodejs
```

Check if they are installed by running the following commands:

```
node -v
```

### Install Dogecoin Core

Download and Extract

```
wget https://github.com/dogecoin/dogecoin/releases/download/v1.14.6/dogecoin-1.14.6-x86_64-linux-gnu.tar.gz && tar -xvzf dogecoin-1.14.6-x86_64-linux-gnu.tar.gz
```
Start Dogecoin Core
```
cd dogecoin-1.14.6/bin
sudo cp dogecoind /usr/local/bin
sudo cp dogecoin-cli /usr/local/bin
dogecoind -daemon
```
*After it started and created .dogecoin in your working directory (eg. /home/doge/.dogecoin) stop the core with `ctrl+c` and set up your `dogecoin.conf`*

`dogecoin.conf` setting

```
cd $HOME
cd .dogecoin
nano dogecoin.conf
```

Put the content below in `dogecoin.conf` and start the core with `dogecoind -daemon`
Set to your own username/password

```
server=1
txindex=1
rpcport=22555
rpcallowip=0.0.0.0/0
listen=1
rpcuser=nodeuser
rpcpassword=nodepassword
```
Wait until the chain fully synced.
Check the syncing process with
`dogecoin-cli getblockchaininfo`

Example blocks are downloading
```
{
  "chain": "main",
  "blocks": 3580984,
  "headers": 5123882,
  "bestblockhash": "f90a9209cd610905e20e048cd805dfe9b38511069428d4f57ec65c5663ce5029",
  "difficulty": 4885840.330967796,
  "mediantime": 1611636483,
  "verificationprogress": 0.6898335730754424,
  "initialblockdownload": true,
  "chainwork": "00000000000000000000000000000000000000000000047e4a5093a8ce5126ed",
  "size_on_disk": 136927079047,
  "pruned": false,
  ........................................
```

*** Once it synced your result should be `"initialblockdownload": false`

Copy & edit `.env` in your doginals minter folder 
Set to your own username/password

```
cd $HOME
cd doginals
cp .env.sample .env
nano .env
```

Set your `.env` to your setting

```
NODE_RPC_URL=http://127.0.0.1:22555
NODE_RPC_USER=nodeuser
NODE_RPC_PASS=nodepassword
TESTNET=false
FEE_PER_KB=690000
```
You can get the current fee per kb from here. [Here](https://blockchair.com/)

## Initiate doginals minter with `Node.js`

```
cd $HOME/doginals
npm install
```

### Managing your minter wallet

Create minter wallet ***Do not mint your inscriptions to this wallet***

```
node . wallet new
```
It will create a new wallet address stored in `.wallet.json` , which your private resides
Send some DOGE to minting fund to the wallet
After the tx has confirmed do wallet sync

```
node . wallet sync
```

(Optional) Split your utxos if you wish to mint simutaneously.
```

node . wallet split <amount>

```
Example
`node . wallet split 10`

Wallet transfer function can be done with
```
node . wallet send <address> <optional amount>
```
*By providing no amount will send to whole fund to wallet destination*

Example
```
node . wallet send D6fWtjJ7MSwifGBwPVHd7fADW7krSAAbwu
```

### Inscribing any file or DRC-20 json
```
node . mint <address> <file PATH>
```
Example
```
node . mint D6fWtjJ7MSwifGBwPVHd7fADW7krSAAbwu ./dogi.json
```

DRC-20 json can be structured as following
```
{ 
  "p": "drc-20",
  "op": "mint",
  "tick": "dogi",
  "amt": "1000"
}
```
Feel free to create your own json file for minting
See `dogi.json`

### Lazy minter DRC-20
Inscribing directly with drc-20 script

```
node . drc-20 mint <address> <ticker> <minting lim amount>
```
Example
```
node . drc-20 mint D6fWtjJ7MSwifGBwPVHd7fADW7krSAAbwu kbsu 1000
```

Please follow other methods in main guide here: 
https://github.com/zachzwei/doginals
https://github.com/Puckapao/doginals

### Troubleshooting
SOON
