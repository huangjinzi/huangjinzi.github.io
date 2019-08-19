---
layout: wiki
title: Git
categories: Git
description: Git 常用操作记录。
keywords: Git, 版本控制
---


1 . 先有github仓库，vscode连接


```
#打开gitbash
#workspace工作目录下执行

$ git init
$ git remote add origin https://github.com/huangjinzi/vue-img-preview-delete
$ git clone https://github.com/huangjinzi/vue-img-preview-delete
```


2. 先有本地项目，再创建git repository，再关联

```
#cmd wordspace目录下执行
vue init webpack vue-todos

#创建repository

$ git push -u origin master

```

3. error表示git内容为空，先上传本地文件
```
error: src refspec master does not match any.
error: failed to push some refs to 'orgin'


$ git status
$ git add .
$ git status
$ git commit -m "first time"
$ git status

```

4. git clone 速度慢，开启ss代理

```
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080

#取消代理

git config --global --unset http.proxy 
git config --global --unset https.proxy

```



