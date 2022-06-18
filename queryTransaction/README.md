

### [How to Query Transaction By ID in Hyperledger Fabric 2.0](https://www.systutorials.com/how-to-query-transaction-by-id-in-hyperledger-fabric-2-0/)
```
$ cd $GOPATH/src/github.com/hyperledger/fabric-samples/test-network

[Set up the environment variables correctly so that the peer command can work correctly]
$ export FABRIC_CFG_PATH=../config/
$ source scripts/envVar.sh 
$ setGlobals 1
$ parsePeerConnectionParameters 1 2

# Here, parsePeerConnectionParameters 1 2 sets the variables, especially $PEER_CONN_PARMS, so that endorsement requests for the invocation will be sent to both organization 1 and 2

[Invoke a chaincode]
$ peer chaincode invoke \
-o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls $CORE_PEER_TLS_ENABLED --cafile $ORDERER_CA \
$PEER_CONN_PARMS \
-C mychannel -n fabcar \
-c '{"function":"CreateCar","Args":["abc", "makeM", "modelX", "red", "ownerO"]}' \
--waitForEvent

[Query the transaction out by transaction ID]
$ peer chaincode invoke \
-o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls $CORE_PEER_TLS_ENABLED --cafile $ORDERER_CA \
$PEER_CONN_PARMS \
-C mychannel -n qscc \
-c '{"function":"GetTransactionByID","Args":["mychannel", "fa0f757bc278fdf6a32d00975602eb853e23a86a156781588d99ddef5b80720f"]}'

[Deserialize the transaction]

```