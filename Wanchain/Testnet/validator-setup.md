# Polkadot Testnet Validator Setup
Describes simplest (dirty and **NOT** secure) setup to get running on the polkadot testnet.

## Prerequisites 
* Clean Ubuntu 18.04 LTS
<!-- * Installation of the [Essential Toolkit](/Staking-Services/Polkadot/Essential-Toolkit.md)-->


## Table of Content
- [Polkadot Testnet Validator Setup](#polkadot-testnet-validator-setup)
  - [Prerequisites](#prerequisites)
  - [Table of Content](#table-of-content)
  - [Setup](#setup)
  - [Acquire Testcoins](#acquire-testcoins)

## Setup

Create wanchain container

```
sudo -s
wget -qO- https://get.docker.com/ | sh
docker pull wanchain/wanpos

docker run -d --name wantest  -v /home/ubuntu/.wanchain:/root/.wanchain wanchain/wanpos /bin/gwan --pluto

# get get container name
docker ps -aqf "name=wantest"

docker exec -it $(docker ps -aqf "name=wantest") /bin/bash

# within container
gwan attach .wanchain/pluto/gwan.ipc

# create new account, example: personal.newAccount('12345678')
personal.newAccount('YourPassword')

#output should result in the account address displayed, for example: 0x3dd3b33b6a68cdbe399ee6f87526965973d9e20e

#query account, example: personal.showPublicKey("0x3dd3b33b6a68cdbe399ee6f87526965973d9e20e","12345678")
personal.showPublicKey("YourAccountAddress", 'YourPassword')

#output should be similar to following: ["0x14a5ab14d484c3372e068674747ea19d00d04e19b7ff7b5b0972fcf418d8ec682acc12ef5fdd6663458ba39d0c57e2abd1aaa41e7118f7645bdad87ecc18820558", "0x39b36b16e21141d937bffaac53ed02de5aba8c0344c3ac66df974f2f50ad27be07f37a76fab8566b873f59bdaf422b783e7f5b6d545dd8d63ab2e97ec672cf97"]

# exit gwan
exit

# save password e.g.: echo "12345678" > /root/.wanchain/pw.txt
echo "YourPassword" > /root/.wanchain/pw.txt

# exit container
exit
```

## Acquire Testcoins

Create email addressed to `techsupport@wanchain.org` with following content

Title
```
Test Coins Request
```
Content
```
Hello,

I need 100100 WAN test coins for WAN PoS testing. (can be other reasonable amount)
My Address Is: YourAccountAddress

Thank You!
```
Where `YourAccountAddress` is your address as per output of `personal.newAccount` command, for example: `0x3dd3b33b6a68cdbe399ee6f87526965973d9e20e`.



