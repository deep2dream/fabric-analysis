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
- Docker and Docker Compose (only needed when running local examples, or using Caliper through its Docker image)
### [npm](https://hyperledger.github.io/caliper/v0.4.2/installing-caliper/#local-npm-install)
- latest fabric version caliper support is **2.1.0**(2.2.0,2.3.0 not supported), default is 1.4.0
```
user@ubuntu:~/caliper-benchmarks$ npm init -y
user@ubuntu:~/caliper-benchmarks$ npm install --only=prod \
    @hyperledger/caliper-cli@0.4.0
user@ubuntu:~/caliper-benchmarks$ npx caliper bind \
    --caliper-bind-sut fabric:2.1.0
user@ubuntu:~/caliper-benchmarks$ npx caliper launch manager \
    --caliper-workspace . \
    --caliper-benchconfig benchmarks/scenario/simple/config.yaml \
    --caliper-networkconfig networks/fabric/fabric-v2.1.1/2org1peergoleveldb/fabric-go.yaml
```

