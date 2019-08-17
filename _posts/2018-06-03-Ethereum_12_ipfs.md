---
layout: post
title: Ethereum_12_ipfs
categories: Ethereum
description: 区块链
keywords: Ethereum
---

1. 下载ipfs dist二进制包

地址 https://ipfs.io/ipns/dist.ipfs.io/#go-ipfs

2. 执行./install.sh

```
root@iZ2zeb5n81znirjwr3s29iZ:/home/como/go-ipfs# ./install.sh
Moved ./ipfs to /usr/local/bin

//之前tar xvzf 解压 mv 移动
//无法执行就将添加path路径，export PATH=$PATH:/home/como/go-ipfs

```

3. 初始化 ipfs init
```
root@iZ2zeb5n81znirjwr3s29iZ:/home/como/go-ipfs# ipfs init
initializing IPFS node at /root/.ipfs
generating 2048-bit RSA keypair...done
peer identity: QmYSnkoAntVQdmsByceEKwMS4XTokW66QxuiKrFeZ29CS8
to get started, enter:

ipfs cat /ipfs/QmS4ustL54uo8FzR9455qaxZwuMiUhyvMcX9Ba8nUH4uVv/readme
```

4. 启动
```
root@iZ2zeb5n81znirjwr3s29iZ:/home/como/go-ipfs# ipfs daemon
Initializing daemon...
Swarm listening on /ip4/127.0.0.1/tcp/4001
Swarm listening on /ip4/172.17.81.217/tcp/4001
Swarm listening on /p2p-circuit/ipfs/QmYSnkoAntVQdmsByceEKwMS4XTokW66QxuiKrFeZ29CS8
Swarm announcing /ip4/127.0.0.1/tcp/4001
Swarm announcing /ip4/172.17.81.217/tcp/4001
API server listening on /ip4/127.0.0.1/tcp/5001
Gateway (readonly) server listening on /ip4/127.0.0.1/tcp/8080
Daemon is ready
```

5. 准备一个文件，如html
```
<html>
<body>
<h1> test page 1 </h1>
<h2> test page 2 </h2>
</body>
</html>
```

6. 上传

```
root@iZ2zeb5n81znirjwr3s29iZ:/home/como/go-ipfs/example# ipfs add -w test.html 
added QmRKXucHZxVY98R6VayB8kWv7s1MWbKTi6n6c5hSkqPNAD test.html
added Qmcwn1kcvcJmE3XMYSCaM75q87UEZLKZG2BrSn5hMmzU6s
```

7. 查看

```
https://ipfs.io/ipfs/QmRKXucHZxVY98R6VayB8kWv7s1MWbKTi6n6c5hSkqPNAD
```


8. ipfs.io的访问
```
#已经翻墙，但ipfs.io仍访问不了
#修改本机host文件，位置C:\Windows\System32\drivers\etc ，加入最后一行

# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost
	0.0.0.0 account.jetbrains.com
	217.182.195.23	ipfs.io

```