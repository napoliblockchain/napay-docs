### Install an Ethereum Blockchain with POA consensus


Let's install ethereum
```bash
sudo apt-get install software-properties-common
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install ethereum
```

configure a node
```bash
mkdir node1
geth --datadir node1/ account new
```
Insert password for node 1: pwdnode1
Then save in a file the address of new account created and in another file the
respective password.
```bash
echo '0x08a58f091xxxxxxxxxxxxxxxxxxxxxx6cfc260b0' >> account.txt
echo 'node1'>node1/password.txt
```

*Se genero nuovi address devo rigenerare il genesis, ma prima devo cancellare
la cartella geth*
Create genesis
```bash
puppeth
create genesis.json
```

Initialize node with the genesis file
```bash
geth --datadir node1/ init genesis.json
```

Generate a bootnode and save enode in a file for future use
```bash
bootnode -genkey boot.key
bootnode -nodekey boot.key -writeaddress
echo '42308ad6724fa5b5f3....95730ec57c4171ebb0a74baf3ae51759' >enode.txt
```

Launch bootnode in tmux session named 'bootnode'
```bash
tmux new-session -d -s bootnode 'bootnode -nodekey boot.key -verbosity 9 -addr :30310'`
```

Launch node1 in tmux session named 'node1'
```bash
tmux new-session -d -s node1 "geth --datadir node1/ --syncmode full --port 30311 --rpc --rpcaddr 81.30.2.232 --rpcport 8501 --rpcapi db,eth,net,web3,txpool,miner --bootnodes enode://9a5c106aa402036814a6f806ec726b00b9730c166149c46093d93567fb31294057c4cae4cb57936e6795926e014b2c853e0fab172768943244b3a9ccc56628e7@127.0.0.1:30310 --networkid 1970 --gasprice 1 -unlock 0xCFe064b7622b032991880f708975a3b03932fA1C --password node1/password.txt --mine --targetgaslimit 7400000 --allow-insecure-unlock"
```

Launch node2 in tmux session named 'node2'
```bash
tmux new-session -d -s node2 "geth --datadir node2/ --syncmode full --port 30312 --rpc --rpcaddr 81.30.2.232 --rpcport 8502 --rpcapi db,eth,net,web3,txpool,miner --bootnodes enode://9a5c106aa402036814a6f806ec726b00b9730c166149c46093d93567fb31294057c4cae4cb57936e6795926e014b2c853e0fab172768943244b3a9ccc56628e7@127.0.0.1:30310 --networkid 1970 --gasprice 1 -unlock 0x5027708592126D2a6816ab026000c17507bB495f --password node2/password.txt --mine --targetgaslimit 7400000 --allow-insecure-unlock"
```

Launch node 3 in tmux sessione named 'node3'
```bash
tmux new-session -d -s node3 "geth --datadir node3/ --syncmode full --port 30313 --rpc --rpcaddr 81.30.2.232 --rpcport 8503 --rpcapi db,eth,net,web3,txpool,miner --bootnodes enode://9a5c106aa402036814a6f806ec726b00b9730c166149c46093d93567fb31294057c4cae4cb57936e6795926e014b2c853e0fab172768943244b3a9ccc56628e7@127.0.0.1:30310 --networkid 1970 --gasprice 1 -unlock 0x29055891Af5c282C68AB284B1d3A2A38c50ecF47 --password node3/password.txt --mine --targetgaslimit 7400000 --allow-insecure-unlock"
```

### Deploy a Smart contract

Let clone a ERC20 token
The token follows the specification in [EIP-20](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md).
```bash
git clone https://github.com/napoliblockchain/ttstoken.git
```


Deploy a contract using `truffle`:

```
npm install -g truffle
npm install
```

Modify the file `truffle-config.js` and insert correct parameters in `privateKey` and `providerUrl`. Then we can deploy the contract using these commands:

```
truffle compile
truffle migrate --network private
```


in console
```bash
cd tokenTTS/contracts
echo "var storageOutput=`solc --optimize --combined-json abi,bin,interface TTSToken.sol`" > storage.js
cat storage.js

geth attach ../node1/geth.ipc
```

Now in Geth console:
```javascript
loadScript('storage.js')
storageOutput
var storageContractAbi = storageOutput.contracts['TTSToken.sol:TTSToken'].abi
var storageContract = eth.contract(JSON.parse(storageContractAbi))
var storageBinCode = "0x" + storageOutput.contracts['TTSToken.sol:TTSToken'].bin

miner.start(1)
personal.unlockAccount(eth.accounts[0])
var deployTransationObject = { from: eth.accounts[0], data: storageBinCode, gas: 1000000 };
var storageInstance = storageContract.new(deployTransationObject)
storageInstance
eth.getTransactionReceipt(storageInstance.transactionHash);
var storageAddress = eth.getTransactionReceipt(storageInstance.transactionHash).contractAddress
storageAddress  // indirizzo dello smart contract

```


### Import in metamask
If you deployed using node1 use cat to show the private key to import in Metamask

```bash
cat keystore node1
```
