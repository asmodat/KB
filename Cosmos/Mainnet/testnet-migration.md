# Testnet -> Mainnet

Quick Full Node Migration

```
cd $HOME/.gaiad
zip -r ./config-old.zip ./config
mkdir -p /backups/gaiad/
mv ./config-old.zip /backups/gaiad/

systemctl stop cosmos

rm -r -f -v $HOME/logs/gaiad.log
rm -r -f -v $HOME/.gaiad/data/

sudo apt upgrade -y

rm -f -v $HOME/.gaiad/config/addrbook.json 
rm -f -v $HOME/.gaiad/config/genesis.json

gaiad unsafe-reset-all

cd $GOPATH/src/github.com/cosmos/cosmos-sdk

# warning: Tag might be different!
tag="v0.34.7"
git checkout master
git fetch --all
git reset --hard $tag
git checkout -f $tag
git pull origin $tag

make clean 
make tools install

gaiacli version --long

mkdir -p $HOME/.gaiad/config

curl https://raw.githubusercontent.com/cosmos/launch/master/genesis.json > $HOME/.gaiad/config/genesis.json

nano ~/.gaiad/config/config.toml
```

Set `seeds` property according ot latest [Mainnet Seed Node List](https://github.com/cosmos/launch#seed-nodes) for example


```
seeds = "ba3bacc714817218562f743178228f23678b2873@public-seed-node.cosmoshub.certus.one:26656,3028c6ee9be21f0d34be3e97a59b093e15ec0658@91.205.173.168:26656,6be0856f6365559fdc2e9e97a07d609f754632b0@cosmos-cosmoshub-2-seed.nodes.polychainlabs.com:26656"
```

### Start a Full Node

```
systemctl start cosmos
journalctl --unit=cosmos -n 100 --no-pager

# verify that all works fine
gaiacli status | jq -r '.sync_info.latest_block_height'
```
