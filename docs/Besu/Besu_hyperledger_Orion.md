## Installing Orion on Besu for private transactions

##### Remember
To enable privacy functionality in production systems, Orion must be highly available and run in a separate instance to Hyperledger Besu.



#### Installing Orion
- Clone the Orion repository

  ```bash
  cd /home/blockchain
  git clone https://github.com/PegaSysEng/orion.git
  ```



- Build Orion with the Gradle wrapper gradlew, omitting tests as follows:

  ```bash
  cd orion
  ./gradlew build -x test
  ```



- Go to the distribution directory:

  ```bash
  cd build/distributions/
  tar -xzf orion-1.5.1-SNAPSHOT.tar.gz
  ```



- test successful installation

  ```bash
  cd orion-<version>/
  bin/orion --help
  ```



  Orion is now installed in /home/blockchain/orion/build/distributions/orion-1.5.1-SNAPSHOT/orion/bin



#### Configuring Besu with Orion

- Create Orion Directories in each node folder

Clique-Network/
├── Node-1
│   ├── data
│   ├── Orion
├── Node-2
│   ├── data
│   ├── Orion
├── Node-3
    ├── data
    ├── Orion    



- Create Password Files
  In each Orion directory, create a file called passwordFile containing a password to encrypt each Orion key pair.

  ```bash
  echo pwdorion1 > passwordFile
  ```



- Generate Orion Keys
  In each Orion directory, generate a public/private keypair for the Orion node:

  ```bash
  /home/blockchain/orion/build/distributions/orion-1.5.1-SNAPSHOT/bin/orion -g nodeKey   
  ```



- Create Orion Configuration Files
  In the Node-1/Orion directory, create a file called orion.conf and add the following properties:

##### Node-1
```
nodeurl = "http://127.0.0.1:8081/"
nodeport = 8081
clienturl = "http://127.0.0.1:8888/"
clientport = 8888
publickeys = ["nodeKey.pub"]
privatekeys = ["nodeKey.key"]
passwords = "passwordFile"
tls = "off"  
```

##### Node-2
```
nodeurl = "http://127.0.0.1:8082/"
nodeport = 8082
clienturl = "http://127.0.0.1:8889/"
clientport = 8889
publickeys = ["nodeKey.pub"]
privatekeys = ["nodeKey.key"]
passwords = "passwordFile"
othernodes = ["http://127.0.0.1:8081/"]
tls = "off"
```

##### Node-3
```
nodeurl = "http://127.0.0.1:8083/"
nodeport = 8083
clienturl = "http://127.0.0.1:8890/"
clientport = 8890
publickeys = ["nodeKey.pub"]
privatekeys = ["nodeKey.key"]
passwords = "passwordFile"
othernodes = ["http://127.0.0.1:8081/"]
tls = "off"
```



#### Start Orion Nodes

In each Orion directory, start Orion specifying the configuration file created in the previous step:

```bash
/home/blockchain/orion/build/distributions/orion-1.5.1-SNAPSHOT/bin/orion orion.conf  
```



otherwise you can create an autostart file orion_start_nodes.sh
```bash
# start node-1
cd /home/blockchain/besu/besu-1.3.7/Clique-Network/Node-1/Orion
tmux new-session -d -s orion1 "/home/blockchain/orion/build/distributions/orion-1.5.1-SNAPSHOT/bin/orion orion.conf"

# start node-2
cd /home/blockchain/besu/besu-1.3.7/Clique-Network/Node-2/Orion
tmux new-session -d -s orion2 "/home/blockchain/orion/build/distributions/orion-1.5.1-SNAPSHOT/bin/orion orion.conf"

#start node-3
cd /home/blockchain/besu/besu-1.3.7/Clique-Network/Node-3/Orion
tmux new-session -d -s orion3 "/home/blockchain/orion/build/distributions/orion-1.5.1-SNAPSHOT/bin/orion orion.conf"
```

then check Orion with:

```
tmux a -t orion1
```



### Start Besu

Now you can start Besu with new configuration

I create a file with these commands:


```bash
#### Node-1
tmux new-session -d -s node1 "/home/blockchain/besu/besu-1.3.7/bin/besu --data-path=Node-1/data --genesis-file=cliqueGenesis.json --network-id 1981  --rpc-http-enabled --rpc-http-api=ETH,NET,CLIQUE,EEA,PRIV --host-whitelist='*' --rpc-http-cors-origins='all' --rpc-http-host=0.0.0.0 --privacy-enabled --privacy-url=http://127.0.0.1:8888 --privacy-public-key-file=Node-1/Orion/nodeKey.pub --min-gas-price=0"  

#### Node-2
tmux new-session -d -s node2 "/home/blockchain/besu/besu-1.3.7/bin/besu --data-path=Node-2/data --genesis-file=cliqueGenesis.json --bootnodes enode://244e17466e2dbcfc5f6242bb22ebd7387d463386c80ab1656392b4b3a2e55b49bab503bce1f3357880beb92e3efe5b944eb7eede7b15a7e1007330e6f1d9bde6@127.0.0.1:30303 --network-id 1981 --p2p-port=30304 --rpc-http-enabled --rpc-http-api=ETH,NET,CLIQUE,EEA,PRIV --host-whitelist='*' --rpc-http-cors-origins='all' --rpc-http-port=8546 --privacy-enabled --privacy-url=http://127.0.0.1:8889 --privacy-public-key-file=Node-2/Orion/nodeKey.pub --min-gas-price=0"  

#### Node-3
tmux new-session -d -s node3 "/home/blockchain/besu/besu-1.3.7/bin/besu --data-path=Node-3/data --genesis-file=cliqueGenesis.json --bootnodes enode://244e17466e2dbcfc5f6242bb22ebd7387d463386c80ab1656392b4b3a2e55b49bab503bce1f3357880beb92e3efe5b944eb7eede7b15a7e1007330e6f1d9bde6@127.0.0.1:30303 --network-id 1981 --p2p-port=30305 --rpc-http-enabled --rpc-http-api=ETH,NET,CLIQUE,EEA,PRIV --host-whitelist='*' --rpc-http-cors-origins='all' --rpc-http-port=8547 --privacy-enabled --privacy-url=http://127.0.0.1:8890 --privacy-public-key-file=Node-3/Orion/nodeKey.pub --min-gas-price=0"
```


## Compile new contract

- git clone https://github.com/napoliblockchain/ttstoken.git ttsprivate/
- cd ttsprivate

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
Compiling your contracts...
===========================
> Everything is up to date, there is nothing to compile.

Migrations dry-run (simulation)
===============================
> Network name:    'private-fork'
> Network id:      1981
> Block gas limit: 0xa00000

1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > block number:        372114
   > block timestamp:     1582031507
   > account:             0x627306090abaB3A6e1400e9345bC60c78a8BEf57
   > balance:             89931.949329391103740086
   > gas used:            210237
   > gas price:           2 gwei
   > value sent:          0 ETH
   > total cost:          0.000420474 ETH

   -------------------------------------
   > Total cost:         0.000420474 ETH

2_token_migration.js
====================

   Deploying 'TTSToken'
   --------------------
   > block number:        372116
   > block timestamp:     1582031509
   > account:             0x627306090abaB3A6e1400e9345bC60c78a8BEf57
   > balance:             89931.946307207103740086
   > gas used:            1483729
   > gas price:           2 gwei
   > value sent:          0 ETH
   > total cost:          0.002967458 ETH

   -------------------------------------
   > Total cost:         0.002967458 ETH

Summary
=======
   > balance:             89931.946307207103740086
   > gas used:            1483729
   > gas price:           2 gwei
   > value sent:          0 ETH
   > total cost:          0.002967458 ETH

   -------------------------------------
   > Total cost:         0.002967458 ETH

Summary
=======
> Total deployments:   2
> Final cost:          0.003387932 ETH

Starting migrations...
======================
> Network name:    'private'
> Network id:      1981
> Block gas limit: 0xa00000

1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > transaction hash:    0xe4735323d01013a965d468e79887bf3c51969015359edad34387190555f8328c
   > Blocks: 0            Seconds: 12
   > contract address:    0xF426505ac145abE033fE77C666840063757Be9cd
   > block number:        372114
   > block timestamp:     1582031524
   > account:             0x627306090abaB3A6e1400e9345bC60c78a8BEf57
   > balance:             89931.944475045103740086
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
   > transaction hash:    0xb8e581219c0a10241d41b390dd1207d8c8876220687a4c4a316c98d52b17c548
   > Blocks: 0            Seconds: 12
   > contract address:    0xd8672a4A1bf37D36beF74E36edb4f17845E76F4e
   > block number:        372116
   > block timestamp:     1582031554
   > account:             0x627306090abaB3A6e1400e9345bC60c78a8BEf57
   > balance:             89931.904383765103740086
   > gas used:            1962541
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.03925082 ETH

   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.03925082 ETH

Summary
=======
> Total deployments:   2
> Final cost:          0.04452564 ETH
