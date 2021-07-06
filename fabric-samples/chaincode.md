- https://github.com/hyperledger/fabric-samples/tree/main/chaincode/fabcar/external
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
