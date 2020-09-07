# Install Besu hyperledger - IBFT 2.0
Reference: https://besu.hyperledger.org/en/stable/Tutorials/Private-Network/Create-IBFT-Network/



### SO windows 7, Ubuntu 18.04 VM
Installing the Default OpenJDK (Java 11)

```bash
sudo apt update
sudo apt install default-jdk
java -version
```



Installing Besu

```bash
mkdir besu
cd besu
```

for users behind proxy use:

```bash
export http_proxy="http://username:password@www.proxy.com:8080"
export https_proxy="http://username:password@www.proxy.com:8080"
```

Download latest Besu version:
You can download the last update version at [https://pegasys.tech/solutions/hyperledger-besu/](https://pegasys.tech/solutions/hyperledger-besu/)

```bash

wget https://bintray.com/api/ui/download/hyperledger-org/besu-repo/besu-1.5.0.tar.gz
tar -xvzf besu-1.5.0.tar.gz
```

Move Besu folder in /usr and create a link to it :

```bash
mv besu-1.5.0 /usr/
ln -s /usr/besu-1.5.0/bin/besu /bin/besu
```

Create folder structure:

mkdir

IBFT-Network/
    ├── Node-1
    │   └── data
    ├── Node-2
    │   └── data
    ├── Node-3
    │   └── data
    └── Node-4
        └── data    

#### Create Configuration File

Copy the following configuration file definition to a file called ibftConfigFile.json and save it in the IBFT-Network directory:

```bash
touch ibftConfigFile.json
```

Copy the example in ibftConfigFile.json:

```
{
 "genesis": {
   "config": {
      "chainId": 2020,
      "constantinoplefixblock": 0,
      "ibft2": {
        "blockperiodseconds": 15,
        "epochlength": 30000,
        "requesttimeoutseconds": 10
      }
    },
    "nonce": "0x0",
    "timestamp": "0x58ee40ba",
    "gasLimit": "0x47b760",
    "difficulty": "0x1",
    "mixHash": "0x63746963616c2062797a616e74696e65206661756c7420746f6c6572616e6365",
    "coinbase": "0x0000000000000000000000000000000000000000",
    "alloc": {
       "fe3b557e8fb62b89f4916b721be55ceb828dbd73": {
          "privateKey": "8f2a55949038a9610f50fb23b5883af3b4ecb3c3bb792cbcefbd1542c692be63",
          "comment": "private key and this comment are ignored.  In a real chain, the private key should NOT be stored",
          "balance": "0xad78ebc5ac6200000"
       },
       "627306090abaB3A6e1400e9345bC60c78a8BEf57": {
         "privateKey": "c87509a1c067bbde78beb793e6fa76530b6382a4c0241e5e4a9ec0a0f44dc0d3",
         "comment": "private key and this comment are ignored.  In a real chain, the private key should NOT be stored",
         "balance": "90000000000000000000000"
       },
       "f17f52151EbEF6C7334FAD080c5704D77216b732": {
         "privateKey": "ae6ae8e5ccbfb04590405997ee2d52d2b330726137b875053c36d94e974d162f",
         "comment": "private key and this comment are ignored.  In a real chain, the private key should NOT be stored",
         "balance": "90000000000000000000000"
       }
      }
 },
 "blockchain": {
   "nodes": {
     "generate": true,
       "count": 4
   }
 }
}
```

#### Gas-free  network  configuration:
- we have replaced the  value of gasLimit in the `ibftConfigFile.json` with the  value "0x1fffffffffffff"
- Then, all client must  be executed with `--min-gas-price=0` (only if --miner is enabled and coinbase configured)
- set 15 seconds Blockperiodseconds

#### Generate Node Keys and Genesis File

In the IBFT-Network directory, generate the node key and genesis file:

```bash
besu operator generate-blockchain-config --config-file=ibftConfigFile.json --to=networkFiles --private-key-file-name=key

Response

2020-09-07 12:18:52.517+02:00 | main | INFO  | GenerateBlockchainConfig | Generating 4 nodes keys.
2020-09-07 12:18:52.545+02:00 | main | INFO  | GenerateBlockchainConfig | Generating keypair for node 0.
2020-09-07 12:18:54.313+02:00 | main | INFO  | GenerateBlockchainConfig | Generating keypair for node 1.
2020-09-07 12:18:54.324+02:00 | main | INFO  | GenerateBlockchainConfig | Generating keypair for node 2.
2020-09-07 12:18:54.338+02:00 | main | INFO  | GenerateBlockchainConfig | Generating keypair for node 3.
2020-09-07 12:18:54.352+02:00 | main | INFO  | GenerateBlockchainConfig | Generating IBFT extra data.
2020-09-07 12:18:54.361+02:00 | main | INFO  | GenerateBlockchainConfig | Writing genesis file.

```
This command create networkFiles folder.



#### Copy the Genesis File to the IBFT-Network Directory

Copy the genesis.json file to the IBFT-Network directory.

```bash
cd networkFiles
cp genesis.json ../
```

#### Copy Node Private Keys to Node Directories

For each node, copy the key files to the data directory for that node

IBFT-Network/
├── genesis.json
├── Node-1
│   ├── data
│   │    ├── key
│   │    ├── key.pub
├── Node-2
│   ├── data
│   │    ├── key
│   │    ├── key.pub
├── Node-3
│   ├── data
│   │    ├── key
│   │    ├── key.pub
├── Node-4
│   ├── data
│   │    ├── key
│   │    ├── key.pub




```bash
- cd networkFiles/keys
- cp 0xd377dc9b7b450fe0d92265bdf8bf679fd85c73c1/*.* ../../Node-1/data/
- cp 0xe16894ca8576e2aef3aca55935af52c42273312a/*.* ../../Node-2/data/
- cp 0xed5abb075e12b5ac7ea00831da13d9bbf16690bd/*.* ../../Node-3/data/
- cp 0xf0a49d5888866bdb1f9760c615a29671f69473d3/*.* ../../Node-4/data/
```



```
Node1: 0x2f3eee7c3fd11aaf0ea9f9ba091a5cf45f6bdade
key: 0x3688a35973030f6254f7d91c5a2b428a16fb6343bec5daba03d19b37d18a61da
key.pub: 0x5a42a37c483c766af13f5615e52bb24708714350eedda9db61d1eceef18007ff3c1b31482d8190c40f5033e360995cd65d73976658cef1b25d79975c0b3ab4dc

Node2: 0x8ef9e34a8f6ff414e4bea6ea7c2d339dc989b02f
key: 0x5a62da22530ef88b00582acd1c3c2f0b3236f04c92bd1eddeee2d83d518e5c0f
key.pub: 0x1ed3d7d0f1abbdc3cdfa205c1218836bc9fa7d5c09a77a28642afb8e4987aea2348228e7fd21b2b236810c14d73e6fec79f704f525da5a96274878f5decbdbf0

Node3: 0x6237f3d0cb05a86c333ce8754469f86fb561cba6
key: 0xcc1232aad5b13fdf47f612b1a5dc2a1348f1c81f13298c88e8f842bd6b6a7637
key.pub: 0x10618199da209da5827a40f75157d75d095e14b2e07a1cca8ea28d755f4607e8d7dccf1488fc8ff90e3ff761ca34bc0a2ffba76ee7407a9f711b0c87d19a7459

Node4: 0xef095aa57ce187d2f310ec893401c621c31f1425
key: 0x35d46d4224230c1eec6b8c798b0cd53cf1eff2935f50842f18a2dc4fe04d65d7
key.pub: 0xafce0cf3303603c8874cd493dcab4b6a0da1fa6fb5e9749a8c2e3337117ffcfd6b8ae82db1006f5a9e315140849d69359d5040178e030d68e7970660fed07533
```

#### Start First Node as Bootnode

From IBFT-Network/ folder

##### start node1
```bash
besu --data-path=Node-1/data --genesis-file=genesis.json --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-whitelist='*' --rpc-http-cors-origins='all' --rpc-http-host=0.0.0.0 --network-id 2020 --rpc-http-port=8501 --p2p-port=30301 --min-gas-price=0 --miner-coinbase=0x5a42a37c483c766af13f5615e52bb24708714350eedda9db61d1eceef18007ff3c1b31482d8190c40f5033e360995cd65d73976658cef1b25d79975c0b3ab4dc
```
When the node starts, the enode URL is displayed. Copy the enode URL to specify Node-1 as the bootnode in the following steps.

*enode://9e02489830b791d99ed457e20a2be311718544f26cb795b4c64f1e655e12c1164e040d25f6c8a31135ce6b612a3cc28be57e265fa8ae364b17ad23ad057240bb@127.0.0.1:30301*

c76cad89034d0fac95c9d36cf30c7d82a7ea5536f680f097decad0d0a4b9a158a6e00b06ed61259cbf17c61e63f9cd1b1e29e67cea8f9aa7dc61fc5a363971c0

```bash
tmux new-session -d -s node1 "besu --data-path=Node-1/data --genesis-file=genesis.json --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT,MINER --host-whitelist='*' --rpc-http-cors-origins='all' --rpc-http-host=0.0.0.0 --network-id 2020 --rpc-http-port=8501 --p2p-port=30301 --min-gas-price=0 --miner-coinbase=0x2f3eee7c3fd11aaf0ea9f9ba091a5cf45f6bdade --miner-enabled"
```





##### start node2
```bash
tmux new-session -d -s node2 "besu --data-path=Node-2/data --genesis-file=genesis.json --bootnodes=enode://9e02489830b791d99ed457e20a2be311718544f26cb795b4c64f1e655e12c1164e040d25f6c8a31135ce6b612a3cc28be57e265fa8ae364b17ad23ad057240bb@127.0.0.1:30301 --p2p-port=30304 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT,MINER --host-whitelist="*" --rpc-http-cors-origins="all" --rpc-http-port=8502 --rpc-http-host=0.0.0.0 --network-id 2020 --min-gas-price=0 --miner-coinbase=0x2f3eee7c3fd11aaf0ea9f9ba091a5cf45f6bdade --miner-enabled"
```



##### start node3
```bash
tmux new-session -d -s node3 "besu --data-path=Node-3/data --genesis-file=genesis.json --bootnodes=enode://9e02489830b791d99ed457e20a2be311718544f26cb795b4c64f1e655e12c1164e040d25f6c8a31135ce6b612a3cc28be57e265fa8ae364b17ad23ad057240bb@127.0.0.1:30301 --p2p-port=30305 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT,MINER --host-whitelist="*" --rpc-http-cors-origins="all" --rpc-http-port=8503 --rpc-http-host=0.0.0.0 --network-id 2020 --min-gas-price=0 --miner-coinbase=0x2f3eee7c3fd11aaf0ea9f9ba091a5cf45f6bdade --miner-enabled"
```



##### start node4
```bash
tmux new-session -d -s node4 "besu --data-path=Node-4/data --genesis-file=genesis.json --bootnodes=enode://9e02489830b791d99ed457e20a2be311718544f26cb795b4c64f1e655e12c1164e040d25f6c8a31135ce6b612a3cc28be57e265fa8ae364b17ad23ad057240bb@127.0.0.1:30301 --p2p-port=30306 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT,MINER --host-whitelist="*" --rpc-http-cors-origins="all" --rpc-http-port=8504 --rpc-http-host=0.0.0.0 --network-id 2020 --min-gas-price=0 --miner-coinbase=0x2f3eee7c3fd11aaf0ea9f9ba091a5cf45f6bdade --miner-enabled"  
```

#### Confirm Private Network is Working

curl -X POST --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":1}' localhost:8501

The result confirms Node-1 has three peers (Node-2, Node-3, and Node-4)

```
{
  "jsonrpc" : "2.0",
  "id" : 1,
  "result" : "0x3"
}
```
curl -X POST --data '{"jsonrpc":"2.0","method":"miner_start","params":[],"id":1}' http://127.0.0.1:8501
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}' http://127.0.0.1:8501



## Metamask

    - SET METAMASK NEW RPC: 5.189.144.215:8545
    - IMPORT "privateKey": "c87509a1c067bbde78beb793e6fa76530b6382a4c0241e5e4a9ec0a0f44dc0d3"


## Deploy Smart Contract
for users behind proxy use:

```
git config --global http.proxy http://username:password@www.proxy.com:80
```

```
git clone https://github.com/jambtc/ttstoken.git
cd ttstoken/contracts

mkdir token/ERC20
cp *.* token/ERC20


```


### 1. setting nodejs version >=12

```
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install gcc g++ make
sudo apt-get install -y nodejs
```

nodejs -v

```
v12.18.3
```
### 2. installing truffle
```
apt update
npm install -g truffle
npm install
```




### 3. Change the truffle-config.js file:
```
var privateKey = "8f2a55949038a9610f50fb23b5883af3b4ecb3c3bb792cbcefbd1542c692be63";
var providerUrl = "http://5.189.144.215:8501";
```


### 4. install truffle private key provider

```
npm install truffle-privatekey-provider
npm install @truffle/hdwallet-provider

```


### 5. install dependencies
```
npm install @babel/core
npm install @openzeppelin/contracts    
```

edit TTSToken.sol for respect import path of ERC files
Then:

### Compile contract
```
truffle compile
```

### Migrating contract on private network
```
truffle migrate --network private
```

##### Response

```
# Migrations dry-run (simulation)

> Network name:    'private-fork'
> Network id:      1981
> Block gas limit: 0xa00000

# 1_initial_migration.js

##    Deploying 'Migrations'

> block number:        17018
> block timestamp:     1576701127
> account:             0x627306090abaB3A6e1400e9345bC60c78a8BEf57
> balance:             89999.999502518
> gas used:            248741
> gas price:           2 gwei
> value sent:          0 ETH
> total cost:          0.000497482 ETH

------

> Total cost:         0.000497482 ETH

# 2_token_migration.js

##    Deploying 'TTSToken'

> block number:        17020
> block timestamp:     1576701129
> account:             0x627306090abaB3A6e1400e9345bC60c78a8BEf57
> balance:             89999.995733502
> gas used:            1857485
> gas price:           2 gwei
> value sent:          0 ETH
> total cost:          0.00371497 ETH

------

> Total cost:          0.00371497 ETH

# Summary

> Total deployments:   2
> Final cost:          0.004212452 ETH





# Starting migrations...

> Network name:    'private'
> Network id:      1981
> Block gas limit: 0xa00000

# 1_initial_migration.js

##    Deploying 'Migrations'

> transaction hash:    0x4a3babbe374cf34d4b5af52d678c895f08b92cfd80ac5da5837b1e32b9254418
> Blocks: 0            Seconds: 0
> contract address:    0x8CdaF0CD259887258Bc13a92C0a6dA92698644C0
> block number:        17017
> block timestamp:     1576701131
> account:             0x627306090abaB3A6e1400e9345bC60c78a8BEf57
> balance:             89999.99472518
> gas used:            263741
> gas price:           20 gwei
> value sent:          0 ETH
> total cost:          0.00527482 ETH

> Saving migration to chain.
>
> ## Saving artifacts
>
> Total cost:          0.00527482 ETH

# 2_token_migration.js

##    Deploying 'TTSToken'

> transaction hash:    0x3c9af3b9f121e2208a1b17b751e94411a9b5581a2abccfd603c9cbf685c3cdb3
> Blocks: 0            Seconds: 12
> contract address:    0x345cA3e014Aaf5dcA488057592ee47305D9B3e10
> block number:        17019
> block timestamp:     1576701161
> account:             0x627306090abaB3A6e1400e9345bC60c78a8BEf57
> balance:             89999.95463502
> gas used:            1962485
> gas price:           20 gwei
> value sent:          0 ETH
> total cost:          0.0392497 ETH

> Saving migration to chain.
>
> ## Saving artifacts
>
> Total cost:           0.0392497 ETH

# Summary

> Total deployments:   2
> Final cost:          0.04452452 ETH
```
