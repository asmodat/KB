

Seed nodes or persistent peers might be required in order to sync the chain and should be defined within `~/.gaiad/config/config.toml` file.

If you operate a public node/sentry you can create a seed node string by combining `ID` of your node with its IP or DNS address and port 26656

```
<ID>@Node_Public_IP_or_DNS:26656
```

**WARNING:** Node_Public_IP_or_DNS should not contain http nor https prefix

ID can be discovered by querying RPC status:

```
curl Node_Public_IP_or_DNS:26657/status
```

example: `echo $(curl -s http://bity-testnet.cosmos-validators.com:26657/status | jq -r '.result.node_info.id')`

result: 9b725f854a97e964f659b5ee2e3087a4eb7c9787

seed/peer string: `9b725f854a97e964f659b5ee2e3087a4eb7c9787@bity-testnet.cosmos-validators.com:26656`

Note: seed/peer string uses 26656 port not 26657 like in case of /status



 

