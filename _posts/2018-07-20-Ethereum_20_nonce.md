---
layout: post
title: Ethereum_20_nonce
categories: Ethereum
description: 区块链
keywords: Ethereum
---

1. 8545开放，有入侵，造成nonce混乱

现象,有陌生地址交易
```
INFO [08-07|15:40:14] 🔨 mined potential block                  number=947 hash=1bf0a2…1be97e
INFO [08-07|15:40:14] Commit new mining work                   number=948 txs=0 uncles=0 elapsed=358.003µs
INFO [08-07|15:40:20] Submitted transaction                    fullhash=0x7301590eb0745c7cdef48553b850adcf294936bdc01301bf2de9dc1ccbfba3c2 recipient=0x6e4Cc3e76765bdc711cc7b5CbfC5bBFe473B192E
INFO [08-07|15:40:20] Submitted transaction                    fullhash=0x94e5294f3260be39b0215d53ed6d9dd92045b761e076465c88476759c048cb8d recipient=0x6e4Cc3e76765bdc711cc7b5CbfC5bBFe473B192E
INFO [08-07|15:40:22] Submitted transaction                    fullhash=0x15c28e55346608d6a15c8d615d5d285d25401769020b5b2b27d86ecc96f0ff78 recipient=0x7097f41F1C1847D52407C629d0E0ae0fDD24fd58
INFO [08-07|15:40:27] Submitted transaction                    fullhash=0xfdcb73b7c5349c2c923f808a8f339be38987ba8961160e45c44fec1bed5a3c1f recipient=0x6e4Cc3e76765bdc711cc7b5CbfC5bBFe473B192E
INFO [08-07|15:40:29] Successfully sealed new block            number=948 hash=c18ad9…483214
INFO [08-07|15:40:29] 🔗 block reached canonical chain          number=943 hash=11169b…ce2458
INFO [08-07|15:40:29] 🔨 mined potential block                  number=948 hash=c18ad9…483214
INFO [08-07|15:40:29] Commit new mining work                   number=949 txs=1 uncles=0 elapsed=585.204µs
INFO [08-07|15:40:31] Submitted transaction                    fullhash=0x8cd44a515650425421e52352811932e64399787798fefe10305194c86235b5cc recipient=0x6e4Cc3e76765bdc711cc7b5CbfC5bBFe473B192E
INFO [08-07|15:40:33] Submitted transaction                    fullhash=0xd8506e008896bbfceb6456ad7a61e2e2ba2131f4e70b2da9bb0f7b183d25b10a recipient=0x7097f41F1C1847D52407C629d0E0ae0fDD24fd58
> eth.getTransactionCount("0xa187e2207f444a6cf17406ca1af960163c188c26","pending")INFO [08-07|15:40:39] Submitted 

```

解决，服务器安全规则配置，关闭8545端口
```
https://github.com/ethereum/go-ethereum/issues/16467

Ok, so this report relates to someone making transactions from your account(s)? Yes, do not open 8545 to the internet. That's highly dangerous. Especially if you use unlock.

```


2. 排查命令

```
地址为钱包地址后半部,前面加Ox

> eth.getTransactionCount("0xfa6f932c207acf8235b668c2b6cdd964ffa6ad88","pending")
（latest、earliest和pending）
> txpool.status
> txpool.content

```