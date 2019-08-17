---
layout: post
title: Ethereum_19_poa
categories: Ethereum
description: 区块链
keywords: Ethereum
---

参考

https://github.com/xiaoping378/blog/blob/master/posts/%E4%BB%A5%E5%A4%AA%E5%9D%8A-%E7%A7%81%E6%9C%89%E9%93%BE%E6%90%AD%E5%BB%BA%E5%88%9D%E6%AD%A5%E5%AE%9E%E8%B7%B5.md

1 创建
```
进入/mnt目录

# mkdir blockchain_poa
# geth --datadir data0 account new
输入用户密码并确认

生成账户地址，记住它，后面会用到
3c5082190d57109ae1cd5e55828ccd49b2f8f0d6

#生成genesis.json 创世区块文件
# puppeth

#networkid设置为10
#时间设置为0，默认15秒


blockchain_poa# touch password.txt
vi输入密码即可euming

```

2. 初始账户，分配足够的eth

```
pupp中设定，可以写到创世区块中

如：测试主账户0x33795Aa557C58d6C8686696Ed26CFA512f482940就是这样设定的，有足够的eth（预留余额账户）支付存证的gas费用

```

3. 初始化网络
```
geth --datadir data0 init genesis.json
```

后面部署合约时，如遇到 exceeds block gas limit的问题，这里先修改gasLimit，调大，可先不操作此步，测试服务器未遇到该问题。

```
"gasLimit": "0x47b760"
修改创世区块的gasLimit
"gasLimit"   : "0xffffffff",
```


4. 启动

```
#生产服务器（poa）
geth --datadir data0 --networkid 10 --rpc --rpcaddr 10.200.0.176 --rpcport 8545 --rpcapi "web3,eth" --rpccorsdomain "*" --unlock "0" --password "password.txt" --nodiscover console

#测试服务器（poa）
geth --datadir data0 --networkid 10 --rpc --rpcaddr 10.200.0.175 --rpcport 8545 --rpcapi "web3,eth" --rpccorsdomain "*" --unlock "0" --password "password.txt" --nodiscover console

#开发服务器（poa）
geth --datadir data0 --networkid 11 --rpc --rpcaddr 172.17.81.217 --rpcport 8545 --rpcapi "web3,eth" --rpccorsdomain "*" --unlock "0" --password "password.txt" --nodiscover console

```