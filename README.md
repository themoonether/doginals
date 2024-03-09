# Doginals

A minter and protocol for inscriptions on Dogecoin. 

## ⚠️⚠️⚠️ Important ⚠️⚠️⚠️

This is a fork of https://github.com/zachzwei/doginals
To remove the use of dogechain.info and use your own dogecoin node rpc instead.
There might be some bugs, so please using with caution.

### Changes

- New wallet created will be add to dogecoin-cli watchlist using importaddress method
- Please do
```
node . wallet sync
```
everytime before minting or splitting.

### Guide

Please follow main guide here: https://github.com/zachzwei/doginals