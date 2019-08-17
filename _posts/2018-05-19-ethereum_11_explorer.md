---
layout: post
title: Ethereum_11_explorer
categories: Ethereum
description: 区块链
keywords: Ethereum
---

1. 地址
https://github.com/carsenk/explorer

```
git clone https://github.com/sthnaqvi/explorer

#先配置地址，在执行install

npm install

bower install（或者bower install --allow-root）
没有bower则先安装 npm install bower -g

npm start
```

2. 配置

```
//阿里云ip地址
47.93.230.63(公)
172.17.81.217(私有)

//app.js
var GETH_HOSTNAME = "47.93.230.63";
var GETH_RPCPORT = 8545;

//package.json
"start": "http-webnode ./app -a 172.17.81.217 -p 8000 -c-1",

//geth启动
geth --datadir data0 --networkid 10 --rpc --rpcaddr 172.17.81.217 --rpcport 8545 --rpcapi "web3,eth" --rpccorsdomain "*"



```

3. 踩坑

```


//v8错误，把node从10减低到8版本
n ls
n 8.0.0

sudo n
选择版本


//Allow Access to Geth and Refresh the Page 出现此错误，把rpccorsdomain 后面改为“*”
geth --datadir data0 --networkid 10 --rpc --rpcaddr 47.93.230.63 --rpcport 8545 --rpcapi "web3,eth" --rpccorsdomain "http://47.93.230.63:8000/"

```


4. node安装,n安装

```
sudo apt-get install nodejs
sudo apt install nodejs-legacy
sudo apt install npm


n sudo npm install npm@latest -g

$ npm install n -g

```