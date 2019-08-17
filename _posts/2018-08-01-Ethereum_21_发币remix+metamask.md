---
layout: post
title: Ethereum_21_发币remix+metamask
categories: Ethereum
description: 区块链
keywords: Ethereum
---

1. metamask链接私链

metamask 密码 huangl2015

个人测试 http://47.93.230.63:8545
测试网络 http://47.94.227.171:8545
	
>MeatMask 链接不上私有网络，在--rpcapi 后参数中加入net



2. remix 部署合约
```
Run->Web3 Provider->http://47.94.227.171:8545

**注意这里预置合约账户以太币 Value 10000 ether，之后getBalance可以查看到
> eth.getBalance("0x98288b629bd4401cfe4f7db553c732918fa5ecc2")
1e+22

选择TVBToken，准备执行Deploy
_ethFundDeposit：	0x33795aa557c58d6c8686696ed26cfa512f482940 先设为这个，*注意地址后面不要有空格*
_currentSupply：一半 50000000 吧


// 加入payable后，重新转账
eth.sendTransaction({from:"0x33795aa557c58d6c8686696ed26cfa512f482940",to:"0x98288b629bd4401cfe4f7db553c732918fa5ecc2",value:web3.toWei(1,"ether")})

//合约账户不支持转账？
eth.sendTransaction({from:"0x98288b629bd4401cfe4f7db553c732918fa5ecc2",to:"0x60686232651CB5178059EdbC6dF7bbF1042eBA49",value:web3.toWei(1,"ether")})

//EOA外部账户正常
eth.sendTransaction({from:"0x33795aa557c58d6c8686696ed26cfa512f482940",to:"0x60686232651CB5178059EdbC6dF7bbF1042eBA49",value:web3.toWei(1,"ether")})

```
>合约参考 https://github.com/ethjava/web3j-sample

3. 发币
msg.sender 账户中是全部发行量，即是metaMask登录账号
```
    function TvbToken(
        address _ethFundDeposit,
        uint256 _currentSupply) payable
    {
        ethFundDeposit = _ethFundDeposit;

        isFunding = false;                           //通过控制预售CrowdSale状态
        fundingStartBlock = 0;
        fundingStopBlock = 0;

        currentSupply = formatDecimals(_currentSupply);
        totalSupply = formatDecimals(100000000);
        balances[msg.sender] = totalSupply;
        if(currentSupply > totalSupply) throw;
    }
```

4. cli 向合约账户转账
```

eth.sendTransaction({from:user1,to:user2,value:web3.toWei(3,"ether")})

eth.sendTransaction({from:"0x33795aa557c58d6c8686696ed26cfa512f482940",to:"0xcb0b79aad59f00d250a5fbf99397519ebc3df56b",value:web3.toWei(1000000,"ether")})
```
>没有接受到，可能是contract的payable问题


5. gas自动补充
```
//如果发送者以太币余额小于0.01 ether，则自动向其发送0.01 ether用于gas（由合约账户支出）
                    if (msg.sender.balance < 0.01 ether) {
                            msg.sender.transfer(0.01 ether);
                    }
                    //如果接收者以太币余额小于0.01 ether，则自动向其发送0.01 ether用于gas
                    if (_to.balance < 0.01 ether) {
                            _to.transfer(0.01 ether);
                    }


                    payable
```
6.创建钱包
```
 personal.newAccount() 
 WalletUtils.generateNewWalletFile()
 
 两种方式基本一样
 区别在于WalletUtils创建的钱包文件，一般在应用服务器上；
 
 personal，需要启动时，在rpc后加入personal参数，另外生成的钱包是返回是地址，不是json钱包文件

```

7. 测试账户

```
        String ercContract = "0xd5903b5f69d1e66b286ace56d1c272b8e0f8644d";

        String account1 = "0xB61d39e1400bA9c4e13e1247e03dc14D9833bb6A";
        
		String account2 = "0x3Dcb9E85aCc0Fef13597B91C2d1Cd7137be9df51";
		
        String account11 ="0x790397FDcd6900404FC06f1D21f14937612D2b8b";

        String account22 = "0x3E3Ef7CaB0de386cA75c9fA73F13Cc4Ab5b8e7B1";
```

8. some problem

问 | 答
---|---
问：metamask transfer 只减少，未增加 | 答：可能account不是一个合约
问：bouncycastle provider can't find classes needed for algorithm | 答：https://stackoverflow.com/questions/6908696/bouncycastle-provider-cant-find-classes-needed-for-algorithm
问：Error processing transaction request: insufficient funds for gas * price + value | 答： Const.BLOCK_GAS_PRICE, Const.BLOCK_GAS_LIMIT
问：程序转账在metamsk、remix中未体现|答：在remix执行一次transfer，程序已经产生影响
问：metamask不易导出json文件|答: 目前就是这样
问：metamask重新import|答：重新import后一下账户消失，创建同名Account2，原账户出现，重新import账户，原来的eth和token也还在
问：metamask存在pending问题|答：存在，重新import。eth余额0.011，metamask pending，但remix提交transfer后，两个交易一块被confirm。。eth余额0.011，metamask pending，但remix提交transfer后，两个交易一块被confirm。metamask应该有pending的问题。
问：ALERT: [ethjs-rpc] rpc error with payload{"id":4502903896455,"jsonrpc":"2.0","params":["0xf86a12843b9aca0082520894790397fdcd6900404fc06f1d21f14937612d2b8b87071afd498d00008038a07cb9b1fe4f2a65b5b0011115459ee8b4f89523a6a7cab25d1e0e4a68ab45d484a06ab9abf6eceeb6ffbec38ef3c7737f2f44ec376c614e27ac3aff27616ba99d35"],"method":"eth_sendRawTransaction"} Error: nonce too low |答：不确定
