---
layout: post
title: Ethereum_14_JavaIpfsApi
categories: Ethereum
description: 区块链
keywords: Ethereum
---

1. maven pom 配置

```
#注意version，前面有小写字母v

        <dependency>
            <groupId>com.github.ipfs</groupId>
            <artifactId>java-ipfs-api</artifactId>
            <version>v1.2.0</version>
        </dependency>
		
		<repository>
            <id>jitpack.io</id>
            <url>https://jitpack.io</url>
        </repository>
		
```

2. JUnit test
```
#ip为服务器的Public IP

public class TestIpfs {
    private final IPFS ipfs = new IPFS(new MultiAddress("/ip4/47.93.230.63/tcp/5001"));
    private final Random r = new Random(33550336); // perfect

    @Test
    public void dag() throws IOException {
        byte[] object = "{\"data\":1234}".getBytes();
        MerkleNode put = ipfs.dag.put("json", object);

        Cid expected = Cid.decode("zdpuB2CbdLrUK5AgZusm4hraisDDDC135ugdmZWvMHhhsSYTb");

        Multihash result = put.hash;
        Assert.assertTrue("Correct cid returned", result.equals(expected));

        byte[] get = ipfs.dag.get(expected);
        Assert.assertTrue("Raw data equal", Arrays.equals(object, get));
    }

    public static void main(String[] args) throws IOException, TasteException {

    }
}

```
3. Couldn't connect to IPFS daemon at /api/v0/version

```

#1.阿里云服务器，安全规则开放4001，5001端口
#2.ipfs daemon 启动config配置更改
路径要设置为服务器的Private IP

	



$ cd ~/.ipfs		
		
		
root@iZ2zeb5n81znirjwr3s29iZ:~/.ipfs# vi config 

  "Addresses": {
    "Swarm": [
      "/ip4/0.0.0.0/tcp/4001",
      "/ip6/::/tcp/4001"
    ],
    "Announce": [],
    "NoAnnounce": [],
    "API": "/ip4/172.17.81.217/tcp/5001",
    "Gateway": "/ip4/127.0.0.1/tcp/8080"
  },



root@iZ2zeb5n81znirjwr3s29iZ:~/.ipfs# ipfs daemon

Initializing daemon...
Swarm listening on /ip4/127.0.0.1/tcp/4001
Swarm listening on /ip4/172.17.81.217/tcp/4001
Swarm listening on /p2p-circuit/ipfs/QmYSnkoAntVQdmsByceEKwMS4XTokW66QxuiKrFeZ29CS8
Swarm announcing /ip4/127.0.0.1/tcp/4001
Swarm announcing /ip4/172.17.81.217/tcp/4001
API server listening on /ip4/172.17.81.217/tcp/5001
Gateway (readonly) server listening on /ip4/127.0.0.1/tcp/8080


```

4. add文件后，访问
```
#gateway 修改为0.0.0.0
Gateway (readonly) server listening on /ip4/0.0.0.0/tcp/8080

#http而非https
http://47.93.230.63:8080/ipfs/QmQPzjhk9Eqy7vJWhaheyg4NiBxAz51WXUTsx92STBTs1j

```