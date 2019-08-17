---
layout: post
title: Ethereum_22_poa多节点
categories: Ethereum
description: 区块链
keywords: Ethereum
---

1. 启动第一个节点
```
geth --datadir data0 --networkid 10 --rpc --rpcaddr 10.200.0.175 --rpcport 8545 --rpcapi "web3,eth,net,personal" --rpccorsdomain "*" --unlock "0" --password "password.txt" --nodiscover console
```

2. 初始化第二个节点

```
geth --datadir data1 init genesis.json 

```
3. 查看第一个节点信息

```
> admin.nodeInfo
{
  enode: "enode://52d528dbc9bd3cc706c11b66615a2c5bdcc8111dfc7bfdcc551b41d349bcc46d794aacfd11ab4697d845e42f78561dc71aa46b8d918ea30c0d1d0610cfafac2d@[::]:30303?discport=0",
  id: "52d528dbc9bd3cc706c11b66615a2c5bdcc8111dfc7bfdcc551b41d349bcc46d794aacfd11ab4697d845e42f78561dc71aa46b8d918ea30c0d1d0610cfafac2d",
  ip: "::",
  listenAddr: "[::]:30303",
  name: "Geth/v1.7.2-stable-1db4ecdc/linux-amd64/go1.9.1",
  ports: {
    discovery: 0,
    listener: 30303
  },
  protocols: {
    eth: {
      difficulty: 521781,
      genesis: "0x39447d7a2f3a3edc4302e1bfd00f80303e0d008f9a016bc58803668773feaed3",
      head: "0x1c74456a8462ebe217ad22f03bd9288a8aaf4337b7ac5431664d76163557540b",
      network: 10
    }
  }
}

```

4. 启动第二个节点

三处修改(data1,30304,8546)

```
geth --datadir data1 --networkid 10 --port 30304 --rpc --rpcaddr 10.200.0.175 --rpcport 8546 --rpcapi "web3,eth,net,personal" --rpccorsdomain "*" --unlock "0" --password "password.txt" --nodiscover console

```


5. 第二个节点addPeer（第一个节点）

```
 > admin.addPeer("enode://52d528dbc9bd3cc706c11b66615a2c5bdcc8111dfc7bfdcc551b41d349bcc46d794aacfd11ab4697d845e42f78561dc71aa46b8d918ea30c0d1d0610cfafac2d@127.0.0.1:30303?discport=0")
true

加入后开始同步区块

> INFO [10-23|14:54:44] Block synchronisation started 
INFO [10-23|14:54:44] Imported new state entries               count=104 elapsed=278.065µs processed=104 pending=0 retry=0 duplicate=0 unexpected=0
INFO [10-23|14:54:44] Imported new block headers               count=192 elapsed=78.688ms  number=192 hash=ee92f0…22bebe ignored=0
INFO [10-23|14:54:44] Imported new block receipts              count=3   elapsed=182.61µs  bytes=12 number=3   hash=772ff1…752beb ignored=0
INFO [10-23|14:54:44] Imported new block receipts              count=6   elapsed=801.295µs bytes=1921 number=9   hash=6a0711…bbd3a2 ignored=0
INFO [10-23|14:54:44] Imported new block receipts              count=1   elapsed=94.655µs  bytes=4    number=10  hash=bff042…db754f ignored=0
INFO [10-23|14:54:45] Imported new block receipts              count=182 elapsed=3.484ms   bytes=6443 number=192 hash=ee92f0…22bebe ignored=0
INFO [10-23|14:54:45] Imported new block headers               count=192 elapsed=87.628ms  number=384 hash=49475d…060cad ignored=0
INFO [10-23|14:54:45] Imported new block receipts              count=76  elapsed=3.189ms   bytes=304  number=268 hash=0584a9…2b78eb ignored=0
INFO [10-23|14:54:45] Imported new block receipts              count=116 elapsed=5.456ms   bytes=3902 number=384 hash=49475d…060cad ignored=0
INFO [10-23|14:54:45] Imported new block headers               count=1536 elapsed=654.015ms number=1920 hash=d93077…073b23 ignored=0
INFO [10-23|14:54:45] Imported new block receipts              count=2    elapsed=1.235ms   bytes=8    number=386  hash=9197d1…b683cd ignored=0
INFO [10-23|14:54:45] Imported new block receipts              count=1534 elapsed=20.500ms  bytes=16518 number=1920 hash=d93077…073b23 ignored=0
INFO [10-23|14:54:46] Imported new block headers               count=1728 elapsed=695.368ms number=3648 hash=7bdf8b…02c555 ignored=0
INFO [10-23|14:54:46] Imported new block receipts              count=1728 elapsed=20.234ms  bytes=6912  number=3648 hash=7bdf8b…02c555 ignored=0
INFO [10-23|14:54:47] Imported ne

```

6. 授权账户

```
> miner.start()
Error: etherbase missing: etherbase address must be explicitly specified

> eth.accounts
[]
> personal.newAccount("eumingSecret")
"0x61d0c04f41996a480189f547389c6c808b192017"


https://github.com/EasonWang01/Blockchain-and-Cryptography/blob/master/3ethereum-yi-tai-5e6329/geth/puppeth-cli.md



> clique.proposals
> clique.propose("0x61d0c04f41996a480189f547389c6c808b192017", true)
> clique.discard("0x61d0c04f41996a480189f547389c6c808b192017")
> clique.getSnapshot()
{
  hash: "0x1c74456a8462ebe217ad22f03bd9288a8aaf4337b7ac5431664d76163557540b",
  number: 260890,
  recents: {
    260890: "0x33795aa557c58d6c8686696ed26cfa512f482940"
  },
  signers: {
    0x33795aa557c58d6c8686696ed26cfa512f482940: {}
  },
  tally: {},
  votes: []
}

```
**解决方案：

>将data0的keystore授权账户，copy到data1下

```
root@blockchain-test:/mnt/blockchain/data0/keystore# cp UTC--2018-08-07T08-38-58.690404376Z--33795aa557c58d6c8686696ed26cfa512f482940 /mnt/blockchain/data1/keystore/

```


7. 节点同步

*生成 static-nodes.json 文件
内容格式为 "enode://pubkey@ip:port"

```
[
"enode://52d528dbc9bd3cc706c11b66615a2c5bdcc8111dfc7bfdcc551b41d349bcc46d794aacfd11ab4697d845e42f78561dc71aa46b8d918ea30c0d1d0610cfafac2d@127.0.0.1:30303",
"enode://73247d7f7a35eaa7e0de2b058312f05d88c5add11deeee12d15a536250259202a1ccff44a81d235e40b1ad93fed08fbb03702d95db78d57646ea12dab1cab97b@127.0.0.1:30304"
]


更进一步，替换成私有IP

[
"enode://52d528dbc9bd3cc706c11b66615a2c5bdcc8111dfc7bfdcc551b41d349bcc46d794aacfd11ab4697d845e42f78561dc71aa46b8d918ea30c0d1d0610cfafac2d@10.200.0.175:30303",
"enode://73247d7f7a35eaa7e0de2b058312f05d88c5add11deeee12d15a536250259202a1ccff44a81d235e40b1ad93fed08fbb03702d95db78d57646ea12dab1cab97b@10.200.0.175:30304"
]

```

*放到data/geth目录下

> 这样才是永久同步。之前的addpeer只是临时同步，重启后消失，变成两个网络。


8. uncle叔块产生，未返回交易hash，bn：261042，这个问题未重现


web3j配置为blockServerUrl = http://47.94.227.171:8545时
单独启动node0，或者node1的miner.start(),都可以存证成功

同时启动的时候，好像有两条链在同时挖block reached canonical chain。但也可存证成功。这个提示是正常的，经过5-10次的区块确认，达到权威的主链。哈。