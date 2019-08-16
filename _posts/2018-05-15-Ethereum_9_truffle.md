---
layout: post
title: Ethereum_9_truffle
categories: Ethereum
description: 区块链
keywords: Ethereum
---

1. normal step

```
npm install -g truffle
truffle unbox webpack
truffle develop
compile
migrate
npm run dev // 在项目目录下执行/home/como/dapp#
```

```
> truffle-init-webpack@0.0.2 dev /home/como/dapp
> webpack-dev-server

Project is running at http://172.17.81.217:8081/
webpack output is served from /
Hash: 62d5486b7ee13c405d08
Version: webpack 2.7.0
Time: 2362ms
     Asset       Size  Chunks                    Chunk Names
    app.js    1.68 MB       0  [emitted]  [big]  main
index.html  925 bytes          [emitted]         
chunk    {0} app.js (main) 1.65 MB [entry] [rendered]
   [71] ./app/javascripts/app.js 3.64 kB {0} [built]
   [72] (webpack)-dev-server/client?http://172.17.81.217:8081 7.93 kB {0} [built]
   [73] ./build/contracts/MetaCoin.json 47.6 kB {0} [built]
  [111] ./~/loglevel/lib/loglevel.js 7.86 kB {0} [built]
  [117] ./~/querystring-es3/index.js 127 bytes {0} [built]
  [119] ./~/strip-ansi/index.js 161 bytes {0} [built]
  [122] ./app/stylesheets/app.css 905 bytes {0} [built]
  [163] ./~/truffle-contract/index.js 2.64 kB {0} [built]
  [197] ./~/url/url.js 23.3 kB {0} [built]
  [199] ./~/web3/index.js 193 bytes {0} [built]
  [233] (webpack)-dev-server/client/overlay.js 3.67 kB {0} [built]
  [234] (webpack)-dev-server/client/socket.js 1.08 kB {0} [built]
  [235] (webpack)/hot nonrecursive ^\.\/log$ 160 bytes {0} [built]
  [236] (webpack)/hot/emitter.js 77 bytes {0} [built]
  [237] multi (webpack)-dev-server/client?http://172.17.81.217:8081 ./app/javascripts/app.js 40 bytes {0} [built]
     + 223 hidden modules
webpack: Compiled successfully.

```

2. webpack truffle 阿里云ip访问

node_modules目录下的webpack-dev-server/.bin/webpack-dev-server.js文件，里面的yargs.options中的字段

```
"host": {
        type: "string",
        //default: "localhost",
        default: "172.17.81.217",  //新增,输入阿里云的内网IP
        describe: "The hostname/ip address the server will bind to",
        group: CONNECTION_GROUP
    }
```
访问时用阿里云的公网IP访问
http://47.93.230.63:8080/