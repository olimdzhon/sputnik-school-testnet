# Validators School Sputnik Testnet


## Sputnik app-chain binaries installation (sputnikd)

Sputnik app testnet binary repo
https://github.com/Distributed-Validators-Synctems/sputnik-app-chain-practice

```
commit: 36b13319c31a74a1fe99ddd9e0cb84341cd7b6e6
cosmos_sdk_version: v0.47.13-ics-lsm
go: go version go1.21.9 linux/amd64
name: sputnik
server_name: sputnik
version: main-36b13319c31a74a1fe99ddd9e0cb84341cd7b6e6
```

## GenTx generation

### Init
```bash:
gaiad init "<moniker-name>" --chain-id <current course chain id>
```

### Generate keys

```bash:
# To create new keypair - make sure you save the mnemonics!
gaiad keys add <key-name> 
```

or
```
# Restore existing odin wallet with mnemonic seed phrase. 
# You will be prompted to enter mnemonic seed. 
gaiad keys add <key-name> --recover
```
or
```
# Add keys using ledger
gaiad keys show <key-name> --ledger
```

Check your key:
```
# Query the keystore for your public address 
gaiad keys show <key-name> -a
```

### Create account to genesis

```
gaiad genesis add-genesis-account <key-name> 1000000000000000stake
```

### Create GenTX

```
# Create the gentx.
# Note, your gentx will be rejected if you use any amount greater than 10000000stake.
(Maybe app will ask to increase stake amount to 100000000stake)
# Make sure that all participants built their gentx files without typos.

gaiad genesis gentx <key-name> 10000000stake \
  --pubkey=$(gaiad tendermint show-validator) \
  --chain-id=<current course chain id> \
  --moniker="my-moniker" \
  --commission-rate="0.10" \
  --commission-max-rate="0.20" \
  --commission-max-change-rate="0.01"
```

### Add all accounts to genesis

```
# Add account addresses of all participants before generating genesis.
# (whose Gentx files you're using to generate genesis)
gaiad genesis add-genesis-account <account-address> 10000000stake
```

### Generate genesis

```
gaiad genesis collect-gentxs
```

### Start network

```
gaiad start
```
