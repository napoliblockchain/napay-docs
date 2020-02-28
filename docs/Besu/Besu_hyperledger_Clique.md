# install besu hyperledger poa



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

cd besu-1.3.7


mkdir

Clique-Network/
├── Node-1
│   ├── data
├── Node-2
│   ├── data
└── Node-3
    ├── data

/home/blockchain/besu/besu-1.3.7/bin/besu --data-path=Node-1/data public-key export-address --to=Node-1/data/node1Address                                                                    


/home/blockchain/besu/besu-1.3.7/bin/besu --data-path=Node-2/data public-key export-address --to=Node-2/data/node2Address                                                                    


/home/blockchain/besu/besu-1.3.7/bin/besu --data-path=Node-3/data public-key export-address --to=Node-3/data/node3Address             




Copy the following genesis definition to a file called cliqueGenesis.json and save it in the Clique-Network directory:

{
  "config":{
    "chainId":1981,
    "constantinoplefixblock": 0,
    "clique":{
      "blockperiodseconds":15,
      "epochlength":30000
    }
  },
  "coinbase":"0x0000000000000000000000000000000000000000",
  "difficulty":"0x1",

"extraData":"0x00000000000000000000000000000000000000000000000000000000000000009de809f318e8ee6d9295d2c8ea8faef3a1318c950000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  "gasLimit":"0xa00000",
  "mixHash":"0x0000000000000000000000000000000000000000000000000000000000000000",
  "nonce":"0x0",
  "timestamp":"0x5c51a607",
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
   },
  "number":"0x0",
  "gasUsed":"0x0",
  "parentHash":"0x0000000000000000000000000000000000000000000000000000000000000000"
}


In extraData, replace <Node 1 Address> with the address for Node-1 excluding the 0x prefix.

Start First Node as Bootnode

From Clique-Network/ folder

tmux new-session -d -s node1 "/home/blockchain/besu/besu-1.3.7/bin/besu --data-path=Node-1/data --genesis-file=cliqueGenesis.json --network-id 1981  --rpc-http-enabled --rpc-http-api=ETH,NET,CLIQUE --host-whitelist='*' --rpc-http-cors-origins='all' --rpc-http-host=0.0.0.0"  

**
When the node starts, the enode URL is displayed. Copy the enode URL to specify Node-1 as the bootnode in the following steps.

faultP2PNetwork | Enode URL enode://244e17466e2dbcfc5f6242bb22ebd7387d463386c80ab1656392b4b3a2e55b49bab503bce1f3357880beb92e3efe5b944eb7eede7b15a7e1007330e6f1d9bde6@127.0.0.1:30303


5. Start Node-2

tmux new-session -d -s node2 "/home/blockchain/besu/besu-1.3.7/bin/besu --data-path=Node-2/data --genesis-file=cliqueGenesis.json --bootnodes enode://244e17466e2dbcfc5f6242bb22ebd7387d463386c80ab1656392b4b3a2e55b49bab503bce1f3357880beb92e3efe5b944eb7eede7b15a7e1007330e6f1d9bde6@127.0.0.1:30303 --network-id 1981 --p2p-port=30304 --rpc-http-enabled --rpc-http-api=ETH,NET,CLIQUE --host-whitelist='*' --rpc-http-cors-origins='all' --rpc-http-port=8546"     

**
5. Start Node-3

tmux new-session -d -s node3 "/home/blockchain/besu/besu-1.3.7/bin/besu --data-path=Node-3/data --genesis-file=cliqueGenesis.json --bootnodes enode://244e17466e2dbcfc5f6242bb22ebd7387d463386c80ab1656392b4b3a2e55b49bab503bce1f3357880beb92e3efe5b944eb7eede7b15a7e1007330e6f1d9bde6@127.0.0.1:30303 --network-id 1981 --p2p-port=30305 --rpc-http-enabled --rpc-http-api=ETH,NET,CLIQUE --host-whitelist='*' --rpc-http-cors-origins='all' --rpc-http-port=8547"     

**
Confirm Private Network is Working

curl -X POST --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":1}' 80.2.12.232:8545

The result confirms Node-1 has two peers (Node-2 and Node-3):
{
  "jsonrpc" : "2.0",
  "id" : 1,
  "result" : "0x2"
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
