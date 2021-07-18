## REF
- https://blog.csdn.net/chendygame/article/details/108625936
- https://yeasy.gitbook.io/blockchain_guide/09_fabric_deploy/install_docker
```
fabric-nodeenv
node:12.13.0-alpine
支持 Node.Js 语言的链码基础镜像，其中安装了 make、python、g++。在链码实例化过程中作为默认编译环境生成 Node.Js 链码镜像，同时作为 Node.Js 链码运行环境。
```
- https://github.com/yeasy/docker-hyperledger-fabric-base
### nodeenv
- https://github.com/ekalinin/nodeenv
- https://github.com/mhart/alpine-node
- https://hub.docker.com/r/hyperledger/fabric-nodeenv/tags?page=1&ordering=last_updated
- https://hub.docker.com/_/node/
- https://github.com/nodejs/docker-node/blob/ce3bb541693325ee21e38184873ceb4364b3e6f4/16/alpine3.11/Dockerfile
- https://dev.to/wimpress/creating-production-ready-containers-advanced-techniques-4jm3
- https://www.bookstack.cn/read/blockchain_guide-1.4.0/09_fabric_deploy-install_docker.md
```
FROM node:16.2.0-alpine as builder
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm ci
COPY app.js ./

FROM node:16.2.0-alpine
WORKDIR /usr/src/app
COPY --from=builder /usr/src/app .
EXPOSE 3000
USER node
CMD ["node","app.js"]
```
