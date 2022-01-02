### ref
- https://github.com/hyperledger/caliper
- https://www.hyperledger.org/learn/publications/blockchain-performance-metrics

### docs
```
https://hyperledger.github.io/caliper/v0.4.2/getting-started/
https://hyperledger.github.io/caliper/v0.4.2/installing-caliper/
https://hyperledger.github.io/caliper/v0.4.2/bench-config/
https://hyperledger.github.io/caliper/v0.4.2/workload-module/
https://hyperledger.github.io/caliper/v0.4.2/architecture/
https://hyperledger.github.io/caliper/v0.4.2/ethereum-config/
https://hyperledger.github.io/caliper/v0.4.2/fabric-config/new/
https://hyperledger.github.io/caliper/v0.4.2/fabric-config/legacy/
https://hyperledger.github.io/caliper/v0.4.2/fisco-config/
https://hyperledger.github.io/caliper/v0.4.2/fabric-tutorial/
https://hyperledger.github.io/caliper/v0.4.2/writing-connectors/
https://hyperledger.github.io/caliper/v0.4.2/runtime-config/
https://hyperledger.github.io/caliper/v0.4.2/rate-controllers/
https://hyperledger.github.io/caliper/v0.4.2/caliper-monitors/
https://hyperledger.github.io/caliper/v0.4.2/caliper-messengers/
https://hyperledger.github.io/caliper/v0.4.2/benchmark-generator/
https://hyperledger.github.io/caliper/v0.4.2/logging/
https://hyperledger.github.io/caliper/v0.4.2/contributing/
https://hyperledger.github.io/caliper/v0.4.2/caliper-faq/
https://hyperledger.github.io/caliper/v0.4.2/license/
```
## [install](https://hyperledger.github.io/caliper/v0.4.2/installing-caliper/)
### prerequisites
```
Pre-requisites
The following tools are required to install the CLI from NPM:
```
- node-gyp, python2, make, g++ and git (for fetching and compiling some packages during install)
- Node.js **v8.X LTS** or **v10.X LTS** (for running Caliper)
```
$ nvm use v10.15.3
```
- Docker and Docker Compose (only needed when running local examples, or using Caliper through its Docker image)
### [npm](https://hyperledger.github.io/caliper/v0.4.2/installing-caliper/#local-npm-install)
- latest fabric version caliper support is **2.1.0**(2.2.0,2.3.0 not supported), default is 1.4.0
```
[github.com/hyperledger/caliper]
user@ubuntu:~/caliper$ npm init -y
user@ubuntu:~/caliper$ npm install --only=prod \
    @hyperledger/caliper-cli@0.4.0
user@ubuntu:~/caliper$ npx caliper bind \
    --caliper-bind-sut fabric:2.1.0
user@ubuntu:~/caliper$ npx caliper launch manager \
    --caliper-workspace . \
    --caliper-benchconfig benchmarks/scenario/simple/config.yaml \
    --caliper-networkconfig networks/fabric/fabric-v2.1.1/2org1peergoleveldb/fabric-go.yaml

[github.com/hyperledger/caliper-benchmarks]
user@ubuntu:~/caliper-benchmarks$ npm init -y
user@ubuntu:~/caliper-benchmarks$ npm install --only=prod \
    @hyperledger/caliper-cli@0.4.0
user@ubuntu:~/caliper-benchmarks$ npx caliper bind \
    --caliper-bind-sut fabric:2.1.0 --caliper-bind-args=-g
user@ubuntu:~/caliper-benchmarks$ npm audit fix
user@ubuntu:~/caliper-benchmarks/networks/fabric/config_solo$ ./generate.sh
user@ubuntu:~/caliper-benchmarks/networks/fabric/config_raft$  ./generate.sh
user@ubuntu:~/caliper-benchmarks/networks/fabric/config_raft$ expressvpn disconnect
(1.4)
user@ubuntu:~/caliper-benchmarks$ npx caliper bind \
    --caliper-bind-sut fabric:1.4
user@ubuntu:~/caliper-benchmarks$ cp /media/gustav/Investigation/github.com/hyperledger/fabric/scripts/fabric-samples/balance-transfer/artifacts/channel/mychannel.tx ./networks/fabric/config_solo
user@ubuntu:~/caliper-benchmarks$ npm audit fix
user@ubuntu:~/caliper-benchmarks$ npx caliper launch manager \
    --caliper-workspace . \
    --caliper-benchconfig benchmarks/scenario/simple/config.yaml \
    --caliper-networkconfig networks/fabric/v1/v1.4.1/2org1peergoleveldb/fabric-go.yaml
(1.4.0-kafka)
user@ubuntu:~/caliper-benchmarks$ npx caliper launch manager \
    --caliper-workspace . \
    --caliper-benchconfig benchmarks/scenario/simple/config.yaml \
    --caliper-networkconfig networks/fabric/v1/v1.4.0/2org1peergoleveldb_kafka/fabric-go.yaml

(2.1)
user@ubuntu:~/caliper-benchmarks$ npx caliper bind \
    --caliper-bind-sut fabric:2.1.0 --caliper-bind-args=-g
user@ubuntu:~/caliper-benchmarks$ npm audit fix
user@ubuntu:~/caliper-benchmarks$ npx caliper launch manager \
    --caliper-workspace . \
    --caliper-benchconfig benchmarks/scenario/simple/config.yaml \
    --caliper-networkconfig networks/fabric/v2/v2.1.0/2org1peergoleveldb_raft/fabric-go-tls.yaml
    
[github.com/hyperledger/fabric/scripts](https://cxybb.com/article/bean_business/108808167)
user@ubuntu:~/fabric$ git checkout v1.4.1
user@ubuntu:~/fabric/scripts$ ./bootstrap.sh

[Error: Couldn't create Channel 'mychannel'](https://github.com/hyperledger/caliper-benchmarks/issues/37)
A kafka-based Fabric network can be resource-demanding for a single machine. Additionally, make sure that your orderers started successfully (by inspecting the logs). Without these details, debugging the problem is not really possible.

user@ubuntu:~/caliper-benchmarks$ export FABRIC_VERSION=1.4.0;docker-compose -f networks/fabric/docker-compose/2org1peergoleveldb_kafka/docker-compose.yaml up -d
$ docker logs -f <orderer container>
user@ubuntu:~/caliper-benchmarks$ vim networks/fabric/v1/v1.4.1/2org1peergoleveldb/fabric-go.yaml
(original)
caliper:
    blockchain: fabric
    command:
        start: echo 'start'
        end: docker-compose -f networks/fabric/docker-compose/2org1peergoleveldb/docker-compose.yaml down;(test -z \"$(docker ps -aq)\") || docker rm $(docker ps -aq);(test -z \"$(docker images dev* -q)\") || docker rmi $(docker images dev* -q);rm -rf /tmp/hfc-*
(modified)
caliper:
    blockchain: fabric
    command:
        start: echo 'start'
        end: docker-compose -f networks/fabric/docker-compose/2org1peergoleveldb_kafka/docker-compose.yaml down;(test -z \"$(docker ps -aq)\") || docker rm $(docker ps -aq);(test -z \"$(docker images dev* -q)\") || docker rmi $(docker images dev* -q);rm -rf /tmp/hfc-*
        
[Failed to enroll admin ](https://github.com/hyperledger/caliper-benchmarks/issues/118)
sudo chmod 666 /var/run/docker.sock
```
##### [global npm](https://hyperledger.github.io/caliper/v0.4.2/installing-caliper/#global-npm-install)
```
user@ubuntu:~$ npm install -g --only=prod @hyperledger/caliper-cli@0.4.0
(1.4)
user@ubuntu:~$ caliper bind \
    --caliper-bind-sut fabric:1.4 \
    --caliper-bind-args=-g
user@ubuntu:~$ caliper launch manager \
    --caliper-workspace ../caliper-benchmarks \
    --caliper-benchconfig benchmarks/scenario/simple/config.yaml \
    --caliper-fabric-gateway-usegateway \
    --caliper-networkconfig networks/fabric/v1/v1.4.1/2org1peergoleveldb/fabric-go.yaml
(2.1)
user@ubuntu:~$ caliper launch manager \
    --caliper-workspace ../caliper-benchmarks \
    --caliper-benchconfig benchmarks/scenario/simple/config.yaml \
    --caliper-fabric-gateway-usegateway \
    --caliper-networkconfig networks/fabric/v2/v2.1.0/2org1peergoleveldb_raft/fabric-go-tls-solo.yaml
```
## Q & A
- Unexpected error during benchmark execution: Error: Caliper currently only supports gateway based operation using the 2.1.0 Fabric-SDK. Please retry with the gateway flag
```
https://hyperledger.github.io/caliper/v0.4.2/fabric-config/new/
```


