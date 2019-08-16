---
layout: post
title: Ethereum_10_petshop
categories: Ethereum
description: 区块链
keywords: Ethereum
---

1. http://truffleframework.com/tutorials/pet-shop

2. 补充完整合约文件sol，补充完整app.js文件

3. 启动顺序

```
testrpc
truffle migrate
npm run dev

//testrpc 8545
//Ganache 7545
//truffle develop 9545

```

4. 当访问http://47.93.230.63:3000/，不出现图片，浏览器排查，index.html文件jq文件引入失败，更换一个

```
    <!script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script!>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.min.js"></script>  
```

5. MetaMask 

通过key引入testrpc的账户