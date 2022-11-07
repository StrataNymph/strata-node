
# STRATA NETWORK

 [![Total alerts](https://img.shields.io/lgtm/alerts/g/hyperledger/besu.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/hyperledger/besu/alerts/)
 [![Language grade: Java](https://img.shields.io/lgtm/grade/java/g/hyperledger/besu.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/hyperledger/besu/context:java)
 [![Documentation Status](https://readthedocs.org/projects/hyperledger-besu/badge/?version=latest)](https://besu.hyperledger.org/en/latest/?badge=latest)
 [![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/3174/badge)](https://bestpractices.coreinfrastructure.org/projects/3174)
 [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/hyperledger/besu/blob/main/LICENSE)
 [![Discord](https://img.shields.io/discord/905194001349627914?logo=Hyperledger&style=plastic)](https://discord.gg/hyperledger)

[Download](https://hyperledger.jfrog.io/artifactory/besu-binaries/besu/)

Besu is an Apache 2.0 licensed, MainNet compatible, Ethereum client written in Java.

## Useful Tutorial Links

* [Besu User Documentation](https://besu.hyperledger.org/en/stable/Tutorials/Private-Network/Create-IBFT-Network/)
* [Besu Issues]
* [Besu Wiki](https://wiki.hyperledger.org/display/BESU/Hyperledger+Besu)
* [How to Contribute to Besu](https://wiki.hyperledger.org/display/BESU/How+to+Contribute)
* [Besu Roadmap](https://wiki.hyperledger.org/display/BESU/Roadmap)

# Steps 

## Installation and Basic Setup

* Install java >= 11
* Create a Root Directory and move to that directory
* Download Besu => wget https://hyperledger.jfrog.io/artifactory/besu-binaries/besu/21.1.4/besu-21.1.4.zip
* unzip besu-21.1.4.zip
* mv besu-21.1.4 besu
* cd besu/bin
* ./besu --version
* cd Root Directory 
* mkdir Network 
* cd Network

## Create how many nodes needed for your project, For example create two nodes setup

* mkdir -p Node-1/data
* mkdir -p Node-2/data
-------------------------------------------------------------------------------------
1. create config.json [Besu User Documentation](https://besu.hyperledger.org/en/stable/Tutorials/Private-Network/Create-IBFT-Network/)
2. ../besu/bin/besu operator generate-blockchain-config --config-file=ibftConfigFile.json --to=networkFiles --private-key-file-name=key
3. cd networkFiles && cd Node-1
4. copy the key & key.pub from networkFiles/keys/address and paste it to the Node-1/data
5. Running cmd N1:-
../../besu/bin/besu --data-path=data --genesis-file=../networkFiles/genesis.json --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT,WEB3,ADMIN,MINER --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8545 --rpc-http-host=0.0.0.0 --min-gas-price=1000000000 --rpc-http-max-active-connections=65535
6. copy the key & key.pub from networkFiles/keys/address and paste it to the Node-2/data
7. Take the Node-1 enode from the curl post method - curl -X POST --data '{"jsonrpc":"2.0","method":"admin_nodeInfo","params":[],"id":1}' http://127.0.0.1:8545
8. paste the enode response in N2 before Node start
    ../../besu/bin/besu --data-path=data --genesis-file=../networkFiles/genesis.json --bootnodes=enode://enode@N1-ip:30303 --p2p-port=30306 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT,WEB3,ADMIN,MINER --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8546 --rpc-http-host=0.0.0.0

