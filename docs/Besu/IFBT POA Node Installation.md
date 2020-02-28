#IFBT POA Node installation

reference: https://besu.hyperledger.org/en/stable/

This is the  directory   where  the  binaries of the consenus alghorithm for Linux can be found:

https://pegasys.tech/solutions/hyperledger-besu/

On each  node  of the  cluster java needs to be installed.

`besu` xommand configuration:
`mv besu-1.3.8 /usr/`
`ln -s /usr/besu-1.3.8/bin/besu /bin/besu`

1) Create  the  private keys
2) Export the  public keys (on   each   node):
`./besu --node-private-key-file="./privatekey-node3" public-key export-address`

node  3: 0x760637cb7d4f9d3bda4acf736f01602811c69224
node  2: 0x506a7a2ea5172ab182be1801527d4e2c50638b54
node  1: 0xc3e9dca93f9c9d4fd4edab16f5ef72c903517fff

3) Encode  the file with the  public keys:
`./besu rlp encode --from=toEncode.json`

4) Create  the  file genesis.json

5) Replace the  fileld extraData qith the  encoding obtained from step  3 in the  file genesis.json:

`0xf869a00000000000000000000000000000000000000000000000000000000000000000f83f94c3e9dca93f9c9d4fd4edab16f5ef72c903517fff94506a7a2ea5172ab1

6)  Gas-free  network  configuration:
a) replace the  value of gasLimit in the   genesis.json with the  value "0x1fffffffffffff" b) all client must  be executed with `--min-gas-price=0`

7) This is the  folders confuguration that  must  be implemented on each  node:
- ~/node1
|- data
- ~/node2
|- data
- ~/node3
|- data

8) Copy the  private key in the  folder with   appropriate name

9) Create  the  key.pub  file with the  public key of the  node
11) Run the  following   command on each  node  (modify it if necessary):
`besu --data-path=data --genesis-file=./genesis.json --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-whitelist="*" --rpc-http-cors-origins="all" -- rpc-http-host="0.0.0.0" --rpc-http-port=8501 --p2p-port=30301 --min-gas-price=0 --miner-enabled`

11) Copy the  enodes of the  nodes:
enode node1:
enode://804962a016dfc63a47053e8c210247cd0e5f95cf3236a66494e0b4472a41372868601b39116648d7965b2f16c0151b0cebb0dd94bdf2481040e2cfd953ebe856@
enode node2: enode://
f54f78b481c74abb3d0ec5905ee023bdd61df079642f817146c8c9ea06012c375226073086ecf6ef61429d0f29bcce8da060bd279b61da4d7f9d3efcad132771@127.0.0.1 enode nodw3:
enode://2413eaa2beaff06955c65d6c039c8506505bfea9a9e55ce637dbb9f2831607e5225857cce64b6d9021f3c267c4c963f554b39001a4a271ad7babb21eff26073d@1

12) Create  the  file static-nodes.json in the  nodeX/data directory with an   array  of the  encodes
``` [ "enode://
f54f78b481c74abb3d0ec5905ee023bdd61df079642f817146c8c9ea06012c375226073086ecf6ef61429d0f29bcce8da060bd279b61da4d7f9d3efcad132771@192.168.8

"enode://2413eaa2beaff06955c65d6c039c8506505bfea9a9e55ce637dbb9f2831607e5225857cce64b6d9021f3c267c4c963f554b39001a4a271ad7babb21eff26073d@
]
```

13) Node can be started with this command:
`besu --data-path=data --genesis-file=./genesis.json --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-whitelist="*" --rpc-http-cors-origins="all" -- rpc-http-host="0.0.0.0" --rpc-http-port=8501 --p2p-port=30301 --miner-enabled --min-gas-price 0 --miner-coinbase <chiave pubblica nodo>`

On this purpose we have  created a systemd entry  in order  to  make  the  execution   of the  binary   service based. In oorder  to do so create a entry  into the  /
etc/systemd/system with   the  name  of the  service to run,  for example: besu.service with a content similar to this:



14) Deploy contratto


1/1
