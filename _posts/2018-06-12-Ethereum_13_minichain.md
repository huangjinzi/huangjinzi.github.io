---
layout: post
title: Ethereum_13_minichain
categories: Ethereum
description: 区块链
keywords: Ethereum
---


参考：https://medium.com/@mycoralhealth/code-your-own-blockchain-in-less-than-200-lines-of-go-e296282bcffc

1. go env

```
root@iZ2zeb5n81znirjwr3s29iZ:/home/como/gosrc/src/github.com# go env
GOARCH="amd64"
GOBIN="/usr/local/go/bin"
GOCACHE="/root/.cache/go-build"
GOEXE=""
GOHOSTARCH="amd64"
GOHOSTOS="linux"
GOOS="linux"
GOPATH="/home/como/gosrc"
GORACE=""
GOROOT="/usr/local/go"
GOTMPDIR=""
GOTOOLDIR="/usr/local/go/pkg/tool/linux_amd64"
GCCGO="gccgo"
CC="gcc"
CXX="g++"
CGO_ENABLED="1"
CGO_CFLAGS="-g -O2"
CGO_CPPFLAGS=""
CGO_CXXFLAGS="-g -O2"
CGO_FFLAGS="-g -O2"
CGO_LDFLAGS="-g -O2"
PKG_CONFIG="pkg-config"
GOGCCFLAGS="-fPIC -m64 -pthread -fmessage-length=0 -fdebug-prefix-map=/tmp/go-build159128498=/tmp/go-build -gno-record-gcc-switches"


```

2. go

```
#在GOPATH目录的src下，自己的域名作为报名，后面是项目名称
root@iZ2zeb5n81znirjwr3s29iZ:/home/como/gosrc/src/github.com/huangjinzi# vi main.go

package main
import(
        "fmt"
)
func main(){
        fmt.Println("Hello World")
}


root@iZ2zeb5n81znirjwr3s29iZ:/home/como/gosrc/src/github.com/huangjinzi# go run main.go
```

3. 200行的区块链

```
#下载go语言使用到的包
go get github.com/davecgh/go-spew/spew
go get github.com/gorilla/mux
go get github.com/joho/godotenv

#创建一个.env文件
Let’s also create a .env file in the root of our directory defining the port that will serve http requests. Just add one line to this file:
ADDR=8080

#根据实际代码修改为PORT=8080


#启动
root@iZ2zeb5n81znirjwr3s29iZ:/home/como/gosrc/src/github.com/huangjinzi# go run main.go
2018/06/13 11:09:28 HTTP Server Listening on port : 
(main.Block) {
 Index: (int) 0,
 Timestamp: (string) (len=53) "2018-06-13 11:09:28.51955663 +0800 CST m=+0.001379177",
 BPM: (int) 0,
 Hash: (string) (len=64) "f1534392279bddbf9d43dde8701cb5be14b82f76ec6607bf8d6ad557f60f304e",
 PrevHash: (string) ""
}
```



```
粘贴缩进，解决办法

时候会用vi去打开文件再粘贴上去（鄙人以前就是这样），其实需要先设置一下
set paste
然后再进入插入模式粘贴，代码就不会被自动缩进。可是敲代码的时候需要自动缩进，又得改回来:
set nopaste
```

4. postman

```
http://47.93.230.63:8080/
post
body-raw-json

#content
{"BPM"：55}

#response
{
    "Index": 1,
    "Timestamp": "2018-06-13 15:57:19.205461735 +0800 CST m=+10.149356980",
    "BPM": 55,
    "Hash": "94bd04ad704c8bca8f618e5551f8e95fc17909b1541bc01fdef2c91d9a39b29a",
    "PrevHash": "f1534392279bddbf9d43dde8701cb5be14b82f76ec6607bf8d6ad557f60f304e"
}

```

