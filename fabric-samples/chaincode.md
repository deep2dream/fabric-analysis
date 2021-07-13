- https://github.com/hyperledger/fabric-samples/tree/main/chaincode/fabcar/external
- https://blog.csdn.net/bean_business/article/details/109079641
- https://github.com/hyperledger/fabric-samples/blob/v2.1.1/test-network/scripts/deployCC.sh
```
cd github.com/hyperledger/fabric-samples/chaincode/fabcar/external
cp chaincode.env.example chaincode.env
env $(cat chaincode.env | grep -v "#" | xargs) jq -n '{"address":env.CHAINCODE_SERVER_ADDRESS,"dial_timeout": "10s","tls_required": false}' > connection.json
tar cfz code.tar.gz connection.json
tar cfz fabcar-pkg.tgz metadata.json code.tar.gz
peer lifecycle chaincode install ./fabcar-pkg.tgz
docker build -t hyperledger/fabcar-sample .
docker run -it --rm --name fabcar.org1.example.com --hostname fabcar.org1.example.com --env-file chaincode.env --network=net_test hyperledger/fabcar-sample

```
- initialize network
```
export PATH=$PATH:$GOPATH/src/github.com/hyperledger/fabric-samples/bin
export FABRIC_CFG_PATH=$GOPATH/src/github.com/hyperledger/fabric-samples/config

[change]
cd github.com/hyperledger/fabric-samples
git checkout v2.3.0
repl '--channel-id ' '--channelID=' test-network/scripts

cd test-network
./network.sh up -ca
./network.sh createChannel
./network.sh deployCC
```
