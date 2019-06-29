How to deploy Vexanium BP node<br>
Important Notes:<br>
The minimum server requirements is dual‑core CPU, 4G RAM, 100G hardrive,and the recommended system is 64‑bit ubuntu 18<br>
Vexanium  mainnet cannot be deployed on the same server as the EOS mainnet, meaning that one server can only deploy one mainnet. This is to preventunusual errors during deployment<br>
Before the deployment of Vexanium  node, please get familar with EOS‑related documents, the use of command client and RPC API use for example<br>
For BP registration, you need get a mainnet account at first.<br>
BP Node Deployment<br>
This is the Vexanium  deployment plan based on linux ubuntu. <br>
Download the release file<br>
apt-get update && apt-get install -y wget unzip<br>
<b>For ubuntu18</b><br>
wget http://209.97.162.124:8060/vex1.7.4bin_ubuntu18.zip <br>
<b>For ubuntu16</b><br>
 wget http://209.97.162.124:8060/vex1.7.4bin_ubuntu16.zip <br>
<b>Preparation</b><br>
Generate a public/private key pair for BP node. Execute the command as follows:<br>
./cleos create key --to-console<br><br>
Execution result as follows:<br><br>
Private key: 5J9ZDeDPvsgCqxyHvYagrNKQxWTqQwiiZ5RPbAJ3gyhvvER795a<br>
Public key: VEX6vJnArfJm7Txiw5uYCRpovNZ3QNw4EXw5Wtk529cWAkViDSwDg<br>
Public key will be used during BP registration later, that is regproducer.<br>
Get a mainnet account as producer-name with the  Public key, for example account  producertest.<br>
Excute the following commands to startup bp node
>"sudo nohup ./nodeos --max-irreversible-block-age -1 --contracts-console --genesis-json ./genesis.json  --blocks-dir ./data/blocks   --data-dir ./data --chain-state-db-size-mb 1024 --http-server-address 127.0.0.1:80 --p2p-listen-endpoint 0.0.0.0:8090 --max-clients 5 --p2p-max-nodes-per-host 5 --enable-stale-production --producer-name producertest --signature-provider=VEX6vJnArfJm7Txiw5uYCRpovNZ3QNw4EXw5Wtk529cWAkViDSwDg=KEY:5J9ZDeDPvsgCqxyHvYagrNKQxWTqQwiiZ5RPbAJ3gyhvvER795a --plugin eosio::http_plugin --plugin eosio::chain_api_plugin --plugin eosio::producer_plugin --p2p-peer-address 209.97.162.124:8091  39.105.124.20:8092 > nodeos.log 2>&1 &"
<br><br>
<h3>BP Registration</h3><br>
Create local wallet: <br>
./cleos  wallet create --to-console<br>
<b>Import bp account private key to the wallet:</b><br>
./cleos wallet import --private-key 5J9ZDeDPvsgCqxyHvYagrNKQxWTqQwiiZ5RPbAJ3gyhvvER795a <br>
<b>Execute command to register:</b>
./cleos --url http://209.97.162.124:8080 system regproducer producertest VEX6vJnArfJm7Txiw5uYCRpovNZ3QNw4EXw5Wtk529cWAkViDSwDg https://producertest.com
There are 2 conditions for block production:
Top 21 BPs can produce blocks
Local BP node syncronization is complete
