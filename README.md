# Anchor-1-Guide
Anchor-1 Guide


# Manual Node Setup
```
sudo apt update
sudo apt upgrade
sudo apt install gcc
```
# Cloning (This is for new validator)
```
git clone https://github.com/notional-labs/anone.git
cd anone
git checkout testnet-1.0.3
make install
```
# Cloning (For existing validator)
```
cd ~/anone
# Pull latest branches to local 
git fetch
# Checkout correct tag and build
git checkout testnet-1.0.3
make install
# Stop anoned via Screen 
CTRL+C
# or via Systemctl assuming your service file is an1.service
sudo systemctl stop an1
# Clear blockchain data
anoned unsafe-reset-all
```
# Download Genesis Json
```
wget -O ~/.anone/config/genesis.json https://raw.githubusercontent.com/notional-labs/anone/master/networks/testnet-1/genesis.json
```
# Start the chain with new seeds
```
anoned start --p2p.seeds 49a49db05e945fc38b7a1bc00352cafdaef2176c@95.217.121.243:2280,80f0ef5d7c432d2bae99dc8437a9c3db464890cd@65.108.128.139:2280,3afac655e3be5c5fc4a64ec5197346ffb5a855c1@49.12.213.105:2280
```
# Generating new wallet
```
anoned keys add <nameyourwalet>
```
# Restoring old wallet
``` 
anoned keys add <nameyourwallet> --recover
```
# Creating validator
```
anoned tx staking create-validator --amount=1500000000uan1 --from="one1xxxxxxxxxxxxxxxxx" --pubkey=$(anoned tendermint show-validator) --moniker="moniker" --identity="Keybase PGP" --website="https://xxxxxxxxxxxx" --chain-id anone-testnet-1 --commission-rate="0.05" --commission-max-rate="0.20" --commission-max-change-rate="0.01" --min-self-delegation=1 --gas 200000 --fees 250000uan1 --keyring-backend os
```
# Backuping your validator key
```
nano ~/.anone/config/priv_validator_key.json
```

# Helpful command
Show valoper address
```
anoned keys show <keyname> --bech val --address
```
Check status query validator
```
anoned q staking validator <valoperaddress>
```
Delegate
```
anoned tx staking delegate <valoperaddress> <qtyofcoin>uan1 --from <keyname> --chain-id anone-testnet-1 --fees 250000uan1
```
