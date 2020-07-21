# Install Besu hyperledger - Clique
Reference: 

https://besu.hyperledger.org/en/stable/Tutorials/Private-Network/Create-Private-Clique-Network/



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

Clique-Network/
├── Node-1
│   ├── data
├── Node-2
│   ├── data
└── Node-3
    ├── data

#### Generate address and keys

besu --data-path=Node-1/data public-key export-address --to=Node-1/data/node1Address
besu --data-path=Node-2/data public-key export-address --to=Node-2/data/node2Address
besu --data-path=Node-3/data public-key export-address --to=Node-3/data/node3Address
besu --data-path=Node-4/data public-key export-address --to=Node-4/data/node4Address


#### Create Genesis file

Copy the following genesis definition to a file called cliqueGenesis.json and save it in the Clique-Network directory:

```bash
touch cliqueGenesis.json
```

```
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

"extraData":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
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
```

In extraData, replace <Node 1 Address> with the address for Node-1 excluding the 0x prefix.

##### Start node1 as Bootnode
From Clique-Network/ folder

tmux new-session -d -s node1 "besu --data-path=Node-1/data --genesis-file=cliqueGenesis.json --network-id 1981  --rpc-http-enabled --rpc-http-api=ETH,NET,CLIQUE --host-whitelist='*' --rpc-http-cors-origins='all' --rpc-http-host=0.0.0.0"  



When the node starts, the enode URL is displayed. Copy the enode URL to specify Node-1 as the bootnode in the following steps.

*enode://e46dce4f00b6ca355b1911d89362c0fec1df42db324c7fdcf967459cf34568e14263bf1ef5e17993940aece5a9ca7099faf08029a70808ae6b5ed5bd613c0ab7@127.0.0.1:30303*


##### Start node2
```bash
tmux new-session -d -s node2 "besu --data-path=Node-2/data --genesis-file=cliqueGenesis.json --bootnodes enode://e46dce4f00b6ca355b1911d89362c0fec1df42db324c7fdcf967459cf34568e14263bf1ef5e17993940aece5a9ca7099faf08029a70808ae6b5ed5bd613c0ab7@127.0.0.1:30303 --network-id 1981 --p2p-port=30304 --rpc-http-enabled --rpc-http-api=ETH,NET,CLIQUE --host-whitelist='*' --rpc-http-cors-origins='all' --rpc-http-port=8546"
```

##### Start node3
```bash
tmux new-session -d -s node3 "besu --data-path=Node-3/data --genesis-file=cliqueGenesis.json --bootnodes enode://e46dce4f00b6ca355b1911d89362c0fec1df42db324c7fdcf967459cf34568e14263bf1ef5e17993940aece5a9ca7099faf08029a70808ae6b5ed5bd613c0ab7@127.0.0.1:30303 --network-id 1981 --p2p-port=30305 --rpc-http-enabled --rpc-http-api=ETH,NET,CLIQUE --host-whitelist='*' --rpc-http-cors-origins='all' --rpc-http-port=8547"
```

##### Start node4
```bash
tmux new-session -d -s node4 "besu --data-path=Node-4/data --genesis-file=cliqueGenesis.json --bootnodes enode://e46dce4f00b6ca355b1911d89362c0fec1df42db324c7fdcf967459cf34568e14263bf1ef5e17993940aece5a9ca7099faf08029a70808ae6b5ed5bd613c0ab7@127.0.0.1:30303 --network-id 1981 --p2p-port=30306 --rpc-http-enabled --rpc-http-api=ETH,NET,CLIQUE --host-whitelist='*' --rpc-http-cors-origins='all' --rpc-http-port=8548"
```



##### Confirm Private Network is Working

curl -X POST --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":1}' 80.2.12.232:8545

The result confirms Node-1 has 3 peers (Node-2, Node-3 and Node-4):

```
{
  "jsonrpc" : "2.0",
  "id" : 1,
  "result" : "0x3"
}
```



### Deploy Smart Contract

    for users behind proxy use:
    git config --global http.proxy http://username:password@www.proxy.com:80
    
    git clone https://github.com/napoliblockchain/ttstoken.git
    cd ttstoken



##### Using NPM Install Behind A Corporate Proxy Server

npm config set proxy http://<username><password>@proxy-server-url>:<port>
npm config set https-proxy http://<username><password>@proxy-server-url>:<port>

use `%5C` for `\`


##### Install truffle

    apt-get install solc
    select - npm install -g truffle
    or - npm i -g --unsafe-perm=true --allow-root truffle
    npm install


##### Modify truffle-config.js
    insert private key without 0x
    
    var privateKey = "c87509a1c067bbde78beb793e6fa76530b6382a4c0241e5e4a9ec0a0f44dc0d3";
    var providerUrl = "http://napay.napoliblockchain.tk:8545";


##### Install truffle private key provider

    npm install truffle-privatekey-provider


##### Install openzeppelin

    npm install @openzeppelin/contracts    

##### Compile contract

    truffle compile


##### Migrate contract on private network

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




## Metamask

    - SET METAMASK NEW RPC: 80.2.12.232:8545
    - IMPORT "privateKey": "xxxxxxx"
