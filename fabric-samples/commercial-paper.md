## prerequisites
### [nvm](https://github.com/nvm-sh/nvm#installing-and-updating)
- https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-18-04
- https://github.com/nvm-sh/nvm#usage
#### install
```
[using scripts]
$ wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
$ source ~/.bashrc

[using git]
$ cd ~
$ git clone https://github.com/nvm-sh/nvm.git .nvm
$ cd ~/.nvm
$ git checkout v0.38.0
$ ./nvm.sh

```
#### usage
```
[install specific version]
nvm install 10.15.3

[check running version]
nvm run node --version

[switch to specific version]
nvm exec 4.2 node --version

```
