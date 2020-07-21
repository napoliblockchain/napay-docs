# Install Besu hyperledger - IBFT
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

```bash
wget https://bintray.com/api/ui/download/hyperledger-org/besu-repo/besu-1.3.7.tar.gz
tar -xvzf besu-1.3.7.tar.gz
```

Besu command configuration:

```bash
mv besu-1.3.7 /usr/
ln -s /usr/besu-1.3.7/bin/besu /bin/besu
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
      "chainId": 2018,
      "constantinoplefixblock": 0,
      "ibft2": {
        "blockperiodseconds": 15,
        "epochlength": 30000,
        "requesttimeoutseconds": 10
      }
    },
    "nonce": "0x0",
    "timestamp": "0x58ee40ba",
    "gasLimit": "0x1fffffffffffff",
    "difficulty": "0x1",
    "mixHash": "0x63746963616c2062797a616e74696e65206661756c7420746f6c6572616e6365",
    "coinbase": "0x0000000000000000000000000000000000000000",
    "alloc": {
       "fe3b557e8fb62b89f4916b721be55ceb828dbd73": {
          "privateKey": "8f2a55949038a9610f50fb23b5883af3b4ecb3c3bb792cbcefbd1542c692be63",
          "comment": "private key and this comment are ignored.  In a real chain, the private key should NOT be stored",
          "balance": "0xad0000034ab7383078ebc5ac6200000"
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
- replace the  value of gasLimit in the `ibftConfigFile.json` with the  value "0x1fffffffffffff"
- all client must  be executed with `--min-gas-price=0` (only if --miner is enabled and coinbase configured)

#### Blockperiodseconds
- set 15 seconds

#### Generate Node Keys and Genesis File

In the IBFT-Network directory, generate the node key and genesis file:

```bash
besu operator generate-blockchain-config --config-file=ibftConfigFile.json --to=networkFiles --private-key-file-name=key
```

This command creates networkFiles folder.

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
Node1: 0xd377dc9b7b450fe0d92265bdf8bf679fd85c73c1
key: 0xfa97881a123bfb139dec106a97991c2bf6a0f399df3dbf2b04a762cb4621ad8
key.pub: 0xcc5bba0356b707fb9a1906bb70748e12269c40537b40464e182e0adb273fc7ad9b73fd361b186fff3842ff94e1ec42d2415449df8a23b4d2baf18433ec2af3eb

Node2: 0xe16894ca8576e2aef3aca55935af52c42273312a
key: 0x721ae1e8760c312ffdff6a3955653cc23a316f4a039e8cf566c21fda0fd514f9
key.pub: 0x2e8b3a2cf67232e031b5e1c0f69a7340434721eb73ed59b30d3560a8c49ab30fd4468d3f46bc76ade15f0ff8c4a7c0f697248c0ef84f9a968beed9483a81e954

Node3: 0xed5abb075e12b5ac7ea00831da13d9bbf16690bd
key: 0x5c958b3ddf1657699c1fd35a398e0270f615b001e5c0bf89745c41992f23161f
key.pub: 0x65c93be04a70941f7fc03230adcfb43d3a46b17bb02f40866c93f82fe8813659c6c2af0307bd1c0b6e73771431f1367d64505f9a67f587e32e6128602f4aa82e

Node4: 0xf0a49d5888866bdb1f9760c615a29671f69473d3
key: 0x42a933cf5b5801d02d7affc6e4f16d8e176d0fcb3e03e33d3b116f1bdbf05109
key.pub: 0x1d5b553eadcebfef2ca5651f5db92001647bd59741768802152590d893c05a7fc2f3256d856bdfb6b294bb25679206a8628e8d13bc7c8f06e96bf5852357bcd2
```

#### Start First Node as Bootnode

From IBFT-Network/ folder

##### start node1
```bash
tmux new-session -d -s node1 "besu --data-path=Node-1/data --genesis-file=genesis.json --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-whitelist='*' --rpc-http-cors-origins='all' --rpc-http-host=0.0.0.0 --network-id 2018 --min-gas-price=0"
```

When the node starts, the enode URL is displayed. Copy the enode URL to specify Node-1 as the bootnode in the following steps.

*enode://31071cf2640ff1789a74c0003d48fa2ee013e82b59f0cd76d15bc0e8919aca105bddd307bc4bf306abefb8674ab1aba7ca516fb677f76b91c665e2853cff0ae6@127.0.0.1:30303*

##### start node2
```bash
tmux new-session -d -s node2 "besu --data-path=Node-2/data --genesis-file=genesis.json --bootnodes=enode://31071cf2640ff1789a74c0003d48fa2ee013e82b59f0cd76d15bc0e8919aca105bddd307bc4bf306abefb8674ab1aba7ca516fb677f76b91c665e2853cff0ae6@127.0.0.1:30303 --p2p-port=30304 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-whitelist="*" --rpc-http-cors-origins="all" --rpc-http-port=8546 --rpc-http-host=0.0.0.0 --network-id 2018 --min-gas-price=0"
```



##### start node3
```bash
tmux new-session -d -s node3 "besu --data-path=Node-3/data --genesis-file=genesis.json --bootnodes=enode://31071cf2640ff1789a74c0003d48fa2ee013e82b59f0cd76d15bc0e8919aca105bddd307bc4bf306abefb8674ab1aba7ca516fb677f76b91c665e2853cff0ae6@127.0.0.1:30303 --p2p-port=30305 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-whitelist="*" --rpc-http-cors-origins="all" --rpc-http-port=8547 --rpc-http-host=0.0.0.0 --network-id 2018 --min-gas-price=0"
```



##### start node4
```bash
tmux new-session -d -s node4 "besu --data-path=Node-4/data --genesis-file=genesis.json --bootnodes=enode://31071cf2640ff1789a74c0003d48fa2ee013e82b59f0cd76d15bc0e8919aca105bddd307bc4bf306abefb8674ab1aba7ca516fb677f76b91c665e2853cff0ae6@127.0.0.1:30303 --p2p-port=30306 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-whitelist="*" --rpc-http-cors-origins="all" --rpc-http-port=8548 --rpc-http-host=0.0.0.0 --network-id 2018 --min-gas-price=0"  
```

#### Confirm Private Network is Working

curl -X POST --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":1}' localhost:8545

The result confirms Node-1 has three peers (Node-2, Node-3, and Node-4)

```
{
  "jsonrpc" : "2.0",
  "id" : 1,
  "result" : "0x3"
}
```





## Metamask

    - SET METAMASK NEW RPC: 80.2.12.232:8545
    - IMPORT "privateKey": "c87509a1c067bbde78beb793e6fa76530b6382a4c0241e5e4a9ec0a0f44dc0d3"


## Deploy Smart Contract
for users behind proxy use: 

    - git config --global http.proxy http://username:password@www.proxy.com:80
    - git clone https://github.com/napoliblockchain/ttstoken.git
    - cd ttstoken


### installare truffle

    - npm install -g truffle
    - npm install




### Sarà poi necessario modificare il file truffle-config.js

    - var privateKey = "c87509a1c067bbde78beb793e6fa76530b6382a4c0241e5e4a9ec0a0f44dc0d3";
    - var providerUrl = "http://napay.napoliblockchain.tk:8545";


### installare truffle private key provider

    - npm install truffle-privatekey-provider


### installare openzeppelin

    - npm install @openzeppelin/contracts    

### Compilare il contratto

    - truffle compile


### Migrare il contratto su network privato

    - truffle migrate --network private

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
