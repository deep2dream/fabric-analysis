- https://hyperledger.github.io/composer/latest/installing/development-tools.html

## Install
-  Install the CLI tools
```
nvm install 8.9.0
npm config set user 0
npm config set unsafe-perm true
[online]
npm install -g composer-cli@0.20
npm install -g composer-rest-server@0.20
npm install -g generator-hyperledger-composer@0.20
npm install -g yo@3.1.1

[offline]
npm v composer-cli dist.tarball | xargs curl | tar -xz
npm v composer-rest-server dist.tarball | xargs curl | tar -xz
npm v generator-hyperledger-composer dist.tarball | xargs curl | tar -xz
npm v yo dist.tarball | xargs curl | tar -xz
```
- Install Playground
```
[online]
npm install -g composer-playground@0.20

[offline]
npm v composer-playground dist.tarball | xargs curl | tar -xz
```
- Install Hyperledger Fabric
```
mkdir ~/fabric-dev-servers && cd ~/fabric-dev-servers

curl -O https://raw.githubusercontent.com/hyperledger/composer-tools/master/packages/fabric-dev-servers/fabric-dev-servers.tar.gz
tar -xvf fabric-dev-servers.tar.gz

cd ~/fabric-dev-servers
export FABRIC_VERSION=hlfv12
./downloadFabric.sh
```
- Controlling your dev environment
```
cd ~/fabric-dev-servers
export FABRIC_VERSION=hlfv12
./startFabric.sh
./createPeerAdminCard.sh

[stop]
./stopFabric.sh
```
- Start the web app ("Playground")
```
composer-playground
```
- destroy a previous setup
```
docker kill $(docker ps -q)
docker rm $(docker ps -aq)
docker rmi $(docker images dev-* -q)
```
