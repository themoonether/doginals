# Doginals

A minter and protocol for inscriptions on Dogecoin. 

## ⚠️⚠️⚠️ Important ⚠️⚠️⚠️

This is a fork of https://github.com/zachzwei/doginals
To remove the use of dogechain.info and use your own dogecoin node rpc instead.
There might be some bugs, so please using with caution.

### Changes

- New wallet created will be add to dogecoin-cli watchlist using importaddress method.
- Wallt syncing will use dogecoin-cli's listunspent method to collect UTXOs (max at 9999999 utxos, more than that might have to change your own maxUtxo at line 25).
- Please sync the wallet everytime before doing some mint and split.
```
node . wallet sync
```

### Guide

.env file example
```
NODE_RPC_URL=http://127.0.0.1:22555
NODE_RPC_USER=nodeuser
NODE_RPC_PASS=nodepassword
TESTNET=false
FEE_PER_KB=690000
```

Please follow other methods in main guide here: https://github.com/zachzwei/doginals

### Troubleshooting
SOON