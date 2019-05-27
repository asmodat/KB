# Polkadot Testnet Validator Setup
Describes simplest (dirty and **NOT** secure) setup to get running on the polkadot testnet.

## Prerequisites 
* Clean Ubuntu 18.04 LTS
* Installation of the [Essential Toolkit](/Polkadot/Essential-Toolkit.md)


## Table of Content
- [Polkadot Testnet Validator Setup](#polkadot-testnet-validator-setup)
  - [Prerequisites](#prerequisites)
  - [Table of Content](#table-of-content)
  - [Syncing node](#syncing-node)
  - [Creating Accounts](#creating-accounts)
    - [Acquiring Testnet Tokens](#acquiring-testnet-tokens)
  - [Bonding](#bonding)
    - [Session Key](#session-key)
  - [Staking](#staking)
  - [Validating](#validating)
    - [Validator Service](#validator-service)
- [Monitoring](#monitoring)
  - [RPC Monitor](#rpc-monitor)

## Syncing node

Start polkadot node to sync the chain
```
mkdir -p $HOME/logs
nohup polkadot --chain alex &> $HOME/logs/polkadot.log &

#to preview logs
tail -n 100 $HOME/logs/polkadot.log
```

Check logs and await synchronization to the latest block as per [Telemetry](https://telemetry.polkadot.io/) explorer.

## Creating Accounts

Head out to the [Polkadot Dashboard](https://polkadot.js.org/apps/#/) then to the [account](https://polkadot.js.org/apps/#/accounts) section then create account tab and create 3 types of accounts/keys:

* Controller - used to start or stop validating or nominating (should hold small amount of DOT's used to pay fees)
  * Name:  CAN be suffixed with `_controller` string, e.g.: `YourKeyName_controller`
  * From the Mnemonic/Raw seed dropdown select `Mnemonic` option (12 seed words).
  * Type: SHOULD be **sr**25519 (in the `Advanced creation options`)
* Stash - cold wallet, used to bonded its funds to a particular controller. (holds large amount of funds)
  * Name:  CAN be suffixed with `_stash` string, e.g.: `YourKeyName_stash`
  * From the Mnemonic/Raw seed dropdown select `Mnemonic` option (12 seed words).
  * Key Type: SHOULD be **sr**25519 (in the `Advanced creation options`)
* Session - online, hot key used by a validator in order to perform network operations such as signing consensus votes for [GRANDPA](http://wiki.polkadot.network/en/latest/polkadot/learn/consensus/#grandpa-finality-gadget), producing blocks with [BABE](http://wiki.polkadot.network/en/latest/polkadot/learn/consensus/#babe-block-production), and identifying itself to other nodes over libp2p.
  * Name:  CAN be suffixed with `_session` string, e.g.: `YourKeyName_session`
  * Key Type: MUST be **ed**25519 (in the `Advanced creation options`)
  * From the Mnemonic/Raw seed dropdown select `Raw seed` option and save it (hex string 0x...) in plain text (will be required later). 


For all above keys above set `password` then click save to later choose `Create and backup account` in order to store your JSON key file on your computer. Finally click `Save` option in the final view then go again to create account section to create another key.

### Acquiring Testnet Tokens

In order for the account to exist minimum of 100 mDOT (0.1 DOT) tokens are required. Having more then 0.1 DOT in the balance allows to send transactions (pay for transaction fees).

Testnet Faucets
* Polkadot Faucet: https://faucet.polkadot.chat/ 
  * Requires twitter account
  * Distributes 150 mDOT's every 24h
* Blockxlabs Faucet: https://faucets.blockxlabs.com/?new-access=true
  * Requires registration using email address (during verification check spam folder)
  * Distributes 130 mDOT's
* Polkadot Watercolor: https://riot.im/app/#/room/#polkadot-watercooler:matrix.org
  * Summit your address and ask for test token to the latest testnet in case previous two methods fail.

## Bonding

Head out to the [Polkadot Dashboard](https://polkadot.js.org/apps/#/) then to the [Staking Page](https://polkadot.js.org/apps/#/staking/) then [Account Actions](https://polkadot.js.org/apps/#/staking/actions) Tab.

First select your `Stash` account by clicking `Bond Funds` button, bond (e.g. 15 milli) DOT's to your `Controller` account and set payment destination (where rewards will be sent) to the `Stash` account. Click bond and sign transaction with your `Stash` account.

### Session Key
In the [Account Actions](https://polkadot.js.org/apps/#/staking/actions) of the [Staking](https://polkadot.js.org/apps/#/staking) view, after you have [bonded](#bonding) your coins are to the `Controller` account, you will notice a `Set session` button next to the `Controller` account. Click `Set session` then define `session key` option to be your previously created `Session` key then finally click `Set session key` button.

## Staking
After you defined [Session Key](#session-key) then in the [Account Actions](https://polkadot.js.org/apps/#/staking/actions) of the [Staking](https://polkadot.js.org/apps/#/staking) you will notice that `Controller` account has now a `Validate` and `Nominate` buttons. Click on the `Validate` button. You will be presented with following options to be defined

* Unstake threshold - how often you want to be slashed before being removed from the validator set.
  * Recommend setting this value to 1
* Payment preferences - rewards you will keep, the rest will be shared among you and your nominators.

## Validating

In order to start validator node execute following command

```
polkadot \
--chain alex \
--validator \
--key <0xsession_seed_key> \
--name YourValidatorName \
--telemetry-url ws://telemetry.polkadot.io:1024
```

note: before you begin type `ps -A` and kill `polkadot` process using `ps kill <ID>` command otherwise above command will fail.

### Validator Service 
To maintain the node running even after restarts a dedicated service can be created to ensure that the process is alive.

Create new service file
```
nano /lib/systemd/system/polkadot.service
```

Append following lines

```
[Unit]
Description=Polkadot Validator Service
After=network.target

[Service]
Type=simple
ExecStart=/home/ubuntu/polkadot/target/release/polkadot --chain alex --validator --key <0xSession_seed_key> --name YourValidtorName --telemetry-url ws://telemetry.polkadot.io:1024
Restart=always
RestartSec=5

[Install]
WantedBy=default.target
```

note: name flag in the ExecStart argument MUST NOT contain '.' and '@' characters


Enable service, start and check logs

```
systemctl enable polkadot
systemctl start polkadot
journalctl --unit=polkadot -n 100 --no-pager
```

# Monitoring

## RPC Monitor

```
cd /home/ubuntu/
git clone https://github.com/polkadot-js/tools.git
cd tools
npm i

npm install -g @polkadot/api-cli
npm install -g @polkadot/monitor-rpc
```

To quickly test monitor works execute

```
polkadot-js-monitor --ws ws://localhost:9944 --port 8181
```

Create new service file
```
nano /lib/systemd/system/polkadot-monitor-rpc.service
```

Append following lines

```
[Unit]
Description=Polkadot RPC Monitor Service
After=network.target

[Service]
Type=simple
ExecStart=/usr/bin/node /usr/local/lib/node_modules/@polkadot/monitor-rpc/index.js --ws ws://localhost:9944 --port 8181
Restart=always
RestartSec=5

[Install]
WantedBy=default.target
```

Enable service, start and check logs

```
systemctl enable polkadot-monitor-rpc
systemctl start polkadot-monitor-rpc
journalctl --unit=polkadot-monitor-rpc -n 100 --no-pager
```

To test monitor works execute
```
curl http://localhost:8181 

# output example
{"blockNumber":1406922,"blockTimestamp":"2019-05-20T07:06:42.377Z","elapsed":2.296,"ok":true}
```




