# Install Besu hyperledger - IBFT 2.0



Reference: [https://besu.hyperledger.org/en/stable/Tutorials/Examples/Private-Network-Example/](https://besu.hyperledger.org/en/stable/Tutorials/Examples/Private-Network-Example/)

# Node.js v12.x:

### Using Ubuntu

```bash
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs
```


# Removing nodejs npm
Removing Nodejs and Npm

```sudo apt-get remove nodejs npm node
sudo apt-get purge nodejs
```
Now remove .node and .npm folders from your system

```
sudo rm -rf /usr/local/bin/npm
sudo rm -rf /usr/local/share/man/man1/node*
sudo rm -rf /usr/local/lib/dtrace/node.d
sudo rm -rf ~/.npm
sudo rm -rf ~/.node-gyp
sudo rm -rf /opt/local/bin/node
sudo rm -rf opt/local/include/node
sudo rm -rf /opt/local/lib/node_modules

sudo rm -rf /usr/local/lib/node*
sudo rm -rf /usr/local/include/node*
sudo rm -rf /usr/local/bin/node*
```
Go to home directory and remove any node or node_modules directory, if exists.

You can verify your uninstallation by these commands; they should not output anything.

```
which node
which nodejs
which npm
```
Installing NVM (Node Version Manager) by downloading and running a script

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
```
The command above will clone the NVM repository from Github to the ~/.nvm directory:

Close and reopen your terminal to start using nvm or run the following to use it now:

```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```
As the output above says, you should either close and reopen the terminal or run the commands to add the path to nvm script to the current shell session. You can do whatever is easier for you.

Once the script is in your PATH, verify that nvm was properly installed by typing:

```
nvm --version
```
which should give this output:

```
0.34.0
```
Installing Node.js and npm
```
nvm install node
nvm install --lts
```
Once the installation is completed, verify it by printing the Node.js version:
```
node --version
```
should give this output:
```
v12.8.1
```
otherwise if you set a prefix you should type this:

```
nvm use --delete-prefix v12.18.3
```

Npm should also be installed with node, verify it using

```
npm -v
```
should give:

```
6.13.4
```



# clone TTS Token

git clone https://github.com/napoliblockchain/ttstoken.git

cd ttstoken\contracts

if we run into root user:

```
npm config set user 0
npm config set unsafe-perm true
```
then

```
npm install -g truffle
npm install truffle-privatekey-provider @openzeppelin/contracts@2.4.0
npm install
```

modify supply in contracts/TTSToken.sol
```
1e9 # 10.000.000,00
```

Modify truffle-config.js and insert correct parameters in privateKey and providerUrl.

Then deploy the smart contract:

```
truffle compile
truffle migrate --network private --skipDryRun
```


```bash
Compiling your contracts...
===========================
> Everything is up to date, there is nothing to compile.



Migrations dry-run (simulation)
===============================
> Network name:    'private-fork'
> Network id:      2018
> Block gas limit: 16234336 (0xf7b760)


1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > block number:        35592
   > block timestamp:     1599995131
   > account:             0xFE3B557E8Fb62b89F4916B721be55cEb828dBd73
   > balance:             198.953655632624425408
   > gas used:            210237 (0x3353d)
   > gas price:           2 gwei
   > value sent:          0 ETH
   > total cost:          0.000420474 ETH

   -------------------------------------
   > Total cost:         0.000420474 ETH


2_token_migration.js
====================

   Deploying 'TTSToken'
   --------------------
   > block number:        35594
   > block timestamp:     1599995141
   > account:             0xFE3B557E8Fb62b89F4916B721be55cEb828dBd73
   > balance:             198.950633432624425408
   > gas used:            1483737 (0x16a3d9)
   > gas price:           2 gwei
   > value sent:          0 ETH
   > total cost:          0.002967474 ETH

   -------------------------------------
   > Total cost:         0.002967474 ETH


Summary
=======
> Total deployments:   2
> Final cost:          0.003387948 ETH





Starting migrations...
======================
> Network name:    'private'
> Network id:      2018
> Block gas limit: 16234336 (0xf7b760)


1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > transaction hash:    0x7b9c94bd0a778e2e1f57e530a0196f778dbafdf5f6f67f8d486abf13197d57f1
   > Blocks: 0            Seconds: 0
   > contract address:    0x05d91B9031A655d08E654177336d08543ac4B711
   > block number:        35602
   > block timestamp:     1599995129
   > account:             0xFE3B557E8Fb62b89F4916B721be55cEb828dBd73
   > balance:             198.948801286624425408
   > gas used:            263741 (0x4063d)
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
   > transaction hash:    0x660bc6cc4fc106485bc18670b80e32ba26d25df296783de0613bfe91fc6182b9
   > Blocks: 0            Seconds: 0
   > contract address:    0xe135783649BfA7c9c4c6F8E528C7f56166efC8a6
   > block number:        35604
   > block timestamp:     1599995133
   > account:             0xFE3B557E8Fb62b89F4916B721be55cEb828dBd73
   > balance:             198.908709846624425408
   > gas used:            1962549 (0x1df235)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.03925098 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.03925098 ETH


Summary
=======
> Total deployments:   2
> Final cost:          0.0445258 ETH
```
