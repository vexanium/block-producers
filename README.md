How to deploy Vexanium BP node
Important Notes:
The minimum server requirements is dual‑core CPU, 4G RAM, 100G hardrive,and the recommended system is 64‑bit ubuntu 18
Vexanium  mainnet cannot be deployed on the same server as the EOS mainnet, meaning that one server can only deploy one mainnet. This is to preventunusual errors during deployment
Before the deployment of Vexanium  node, please get familar with EOS‑related documents, the use of command client and RPC API use for example
For BP registration, you need get a mainnet account at first.
BP Node Deployment
This is the Vexanium  deployment plan based on linux ubuntu. 
Download the release file
apt-get update && apt-get install -y wget unzip
For ubuntu18
wget http://209.97.162.124:8060/vex1.7.4bin_ubuntu18.zip 
For ubuntu16
 wget http://209.97.162.124:8060/vex1.7.4bin_ubuntu16.zip 
Preparation
Generate a public/private key pair for BP node. Execute the command as follows:
./cleos create key --to-console
Execution result as follows:
Private key: 5J9ZDeDPvsgCqxyHvYagrNKQxWTqQwiiZ5RPbAJ3gyhvvER795a
Public key: VEX6vJnArfJm7Txiw5uYCRpovNZ3QNw4EXw5Wtk529cWAkViDSwDg
Public key will be used during BP registration later, that is regproducer.
Get a mainnet account as producer-name with the  Public key, for example account  producertest.
Excute the following commands to startup bp node
sudo nohup ./nodeos --max-irreversible-block-age -1 --contracts-console --genesis-json ./genesis.json  --blocks-dir ./data/blocks   --data-dir ./data --chain-state-db-size-mb 1024 --http-server-address 127.0.0.1:80 --p2p-listen-endpoint 0.0.0.0:8090 --max-clients 5 --p2p-max-nodes-per-host 5 --enable-stale-production --producer-name producertest --signature-provider=VEX6vJnArfJm7Txiw5uYCRpovNZ3QNw4EXw5Wtk529cWAkViDSwDg=KEY:5J9ZDeDPvsgCqxyHvYagrNKQxWTqQwiiZ5RPbAJ3gyhvvER795a --plugin eosio::http_plugin --plugin eosio::chain_api_plugin --plugin eosio::producer_plugin --p2p-peer-address 209.97.162.124:8091  39.105.124.20:8092 > nodeos.log 2>&1 &
BP Registration
Create local wallet: 
./cleos  wallet create --to-console
Import bp account private key to the wallet:
./cleos wallet import --private-key 5J9ZDeDPvsgCqxyHvYagrNKQxWTqQwiiZ5RPbAJ3gyhvvER795a 
Execute command to register:
./cleos --url http://209.97.162.124:8080 system regproducer producertest VEX6vJnArfJm7Txiw5uYCRpovNZ3QNw4EXw5Wtk529cWAkViDSwDg https://producertest.com
There are 2 conditions for block production:
Top 21 BPs can produce blocks
Local BP node syncronization is complete
