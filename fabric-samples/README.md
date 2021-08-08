version| sample| support
-------|-------|--------
2.2.0|
## [fabric & fabric-samples](https://hyperledger-fabric.readthedocs.io/en/latest/install.html)
### Install
#### BUILD FROM CODE
```
$ cd github.com//hyperledger/fabric
github.com//hyperledger/fabric# git checkout v2.3.0
github.com//hyperledger/fabric# make docker
github.com//hyperledger/fabric# make configtxgen\
                                    configtxlator\
                                    cryptogen\
                                    discover\
                                    idemixgen\
                                    orderer\
                                    osnadmin\
                                    peer\
                                    fabric-ca-client\
                                    fabric-ca-server
                                    
github.com//hyperledger/fabric# make dist
github.com//hyperledger/fabric# mv build/bin/ ../fabric-samples/
github.com//hyperledger/fabric# cp -rf release/linux-amd64/config/ ../fabric-samples/
github/hyperledger/fabric-samples# export PATH=$PATH:`pwd`/bin
github/hyperledger/fabric-samples/test-network# 
```
#### DOWNLOAD
```
curl -sSL https://bit.ly/2ysbOFE | bash -s
curl -sSL https://bit.ly/2ysbOFE | bash -s -- -h

curl -sSL https://bit.ly/2ysbOFE | bash -s -- <fabric_version> <fabric-ca_version>
curl -sSL https://bit.ly/2ysbOFE | bash -s -- 2.3.2 1.5.0
```
