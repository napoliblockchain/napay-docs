# install besu hyperledger poa on Server Fujitsu Primergy

### SO windows 7, Ubuntu 18.04 VM


Installing the Default OpenJDK (Java 11)
sudo apt update
sudo apt install default-jdk
java -version

mkdir besu

for users behind proxy use:
export http_proxy="http://username:password@www.proxy.com:8080"
export https_proxy="http://username:password@www.proxy.com:8080"

wget https://bintray.com/api/ui/download/hyperledger-org/besu-repo/besu-1.3.7.tar.gz
tar -xvzf besu-1.3.7.tar.gz


`besu` command configuration:
`mv besu-1.3.7 /usr/`
`ln -s /usr/besu-1.3.7/bin/besu /bin/besu`


mkdir

IFBT-Network/
    ├── Node-1
    │   └── data
    ├── Node-2
    │   └── data
    ├── Node-3
    │   └── data
    └── Node-4
        └── data    

####Create Configuration File

Copy the following configuration file definition to a file called ibftConfigFile.json and save it in the IBFT-Network directory:

`touch ibftConfigFile.json`

```
{
 "genesis": {
   "config": {
      "chainId": 2018,
      "constantinoplefixblock": 0,
      "ibft2": {
        "blockperiodseconds": 2,
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

####Generate Node Keys and Genesis File
In the IBFT-Network directory, generate the node key and genesis file:
`besu operator generate-blockchain-config --config-file=ibftConfigFile.json --to=networkFiles --private-key-file-name=key`

This command creates networkFiles folder.

####Copy the Genesis File to the IBFT-Network Directory
Copy the genesis.json file to the IBFT-Network directory.
cd networkFiles
cp genesis.json ../

####Copy Node Private Keys to Node Directories
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

Node1: 0x6cd3788fd003e58e98ec45d6ca72b5ffd6a9c2f3
key: 0x205180b490160a19918c467c58c46b32cc482b87babb18de2582b8043a3eba40
key.pub: 0xd22ebfd5d148ab8582c7d10c24bd0aa5048b62a81328af7c87a4b435a009963f6b1df4f1e51853db83c0f228dabdf99ca2435fba154f22a52bba31688644de58

Node2: 0x6e90e1a779b1f707962f6bf7a79e735ac2e3e7f3
key: 0x59aef34d3f3fd5dce7f7ba837fc353464088a6d7126fa193dbccd7a474cc6c77
key.pub: 0x81c96b61a08d8ad8c788df89bf8059af5f7ad3978bc17f421ecb884c4c308b61ef7fc09314b1a4332a633ab13a1294a9d3153f85860ee9f06900b9b5a6c694a6

Node3: 0x94b4ae19024d65a6db0ebb2a3118efdb68bf0943
key: 0x10a034051c282a8faf2679dda2132a47ef362d03912e56e8988babe8c51e8dc0
key.pub: 0x718320303aa12bac046468cb36e69712471049d09da4dcc588efa3bb319769239577a78c8981ac2f8d4657a04f791b26a64ec8fded75996a09f85657b4f7f3a0

Node4: 0xa59da9a96011334f3c95c16bbbdbb8635d722a9d
key: 0x00b3d6d47b19a03cf98b323910b4e04f5d043f83914237cd88776b10d4958f10
key.pub: 0x47e06ced07789d5a9b43620e5c6552945efaa4fc3a25bbc45b606b50e35bc5776b58c53917859e20cc1695c92317860c9c523f1cdc963cee50e14faba540f657


####Start First Node as Bootnode
From IBFT-Network/ folder

##### start node1
`tmux new-session -d -s node1 "besu --data-path=Node-1/data --genesis-file=genesis.json --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-whitelist='*' --rpc-http-cors-origins='all' --rpc-http-host=0.0.0.0 --network-id 2018"`

When the node starts, the enode URL is displayed. Copy the enode URL to specify Node-1 as the bootnode in the following steps.

enode://31071cf2640ff1789a74c0003d48fa2ee013e82b59f0cd76d15bc0e8919aca105bddd307bc4bf306abefb8674ab1aba7ca516fb677f76b91c665e2853cff0ae6@127.0.0.1:30303

##### start node2
`tmux new-session -d -s node2 "besu --data-path=Node-2/data --genesis-file=genesis.json --bootnodes=enode://31071cf2640ff1789a74c0003d48fa2ee013e82b59f0cd76d15bc0e8919aca105bddd307bc4bf306abefb8674ab1aba7ca516fb677f76b91c665e2853cff0ae6@127.0.0.1:30303 --p2p-port=30304 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-whitelist="*" --rpc-http-cors-origins="all" --rpc-http-port=8546 --rpc-http-host=0.0.0.0 --network-id 2018"`

##### start node3
`tmux new-session -d -s node3 "besu --data-path=Node-3/data --genesis-file=genesis.json --bootnodes=enode://31071cf2640ff1789a74c0003d48fa2ee013e82b59f0cd76d15bc0e8919aca105bddd307bc4bf306abefb8674ab1aba7ca516fb677f76b91c665e2853cff0ae6@127.0.0.1:30303 --p2p-port=30305 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-whitelist="*" --rpc-http-cors-origins="all" --rpc-http-port=8547 --rpc-http-host=0.0.0.0 --network-id 2018"`   

##### start node4
`tmux new-session -d -s node4 "besu --data-path=Node-4/data --genesis-file=genesis.json --bootnodes=enode://31071cf2640ff1789a74c0003d48fa2ee013e82b59f0cd76d15bc0e8919aca105bddd307bc4bf306abefb8674ab1aba7ca516fb677f76b91c665e2853cff0ae6@127.0.0.1:30303 --p2p-port=30306 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-whitelist="*" --rpc-http-cors-origins="all" --rpc-http-port=8548 --rpc-http-host=0.0.0.0 --network-id 2018"`   


####Confirm Private Network is Working

curl -X POST --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":1}' localhost:8545

The result confirms Node-1 has three peers (Node-2, Node-3, and Node-4)
{
  "jsonrpc" : "2.0",
  "id" : 1,
  "result" : "0x3"
}




## Metamask

    - SET METAMASK NEW RPC: 80.2.12.232:8545
    - IMPORT "privateKey": "c87509a1c067bbde78beb793e6fa76530b6382a4c0241e5e4a9ec0a0f44dc0d3"


## dEPLOY SMART CONTRACT

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

# Response

Migrations dry-run (simulation)
===============================
> Network name:    'private-fork'
> Network id:      1981
> Block gas limit: 0xa00000


1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > block number:        17018
   > block timestamp:     1576701127
   > account:             0x627306090abaB3A6e1400e9345bC60c78a8BEf57
   > balance:             89999.999502518
   > gas used:            248741
   > gas price:           2 gwei
   > value sent:          0 ETH
   > total cost:          0.000497482 ETH

   -------------------------------------
   > Total cost:         0.000497482 ETH


2_token_migration.js
====================

   Deploying 'TTSToken'
   --------------------
   > block number:        17020
   > block timestamp:     1576701129
   > account:             0x627306090abaB3A6e1400e9345bC60c78a8BEf57
   > balance:             89999.995733502
   > gas used:            1857485
   > gas price:           2 gwei
   > value sent:          0 ETH
   > total cost:          0.00371497 ETH

   -------------------------------------
   > Total cost:          0.00371497 ETH


Summary
=======
> Total deployments:   2
> Final cost:          0.004212452 ETH





Starting migrations...
======================
> Network name:    'private'
> Network id:      1981
> Block gas limit: 0xa00000


1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
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
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00527482 ETH


2_token_migration.js
====================

   Deploying 'TTSToken'
   --------------------
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
   > Saving artifacts
   -------------------------------------
   > Total cost:           0.0392497 ETH


Summary
=======
> Total deployments:   2
> Final cost:          0.04452452 ETH
