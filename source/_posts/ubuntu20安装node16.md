---
title: ubuntu20安装node16
abbrlink: 59359
date: 2023-06-14 16:16:43
tags:
---

Ubuntu默认的软件源只能安装最高10版本的node

可以通过PPA（personal package archive）进行安装。假如我们想安装大版本号为16的Node.js，那么可以先执行下面的命令安装PPA（如果要安装其他版本的，把16换成其他版本号即可，比如14，不能安装18版本的node，PPA已经不支持Ubuntu20了）

运行命令的时候卡住了，可以给命令行走一个代理

```shell
export ALL_PROXY="http://172.28.224.1:7890"
```

```shell
curl -fsSL https://deb.nodesource.com/setup_16.x | sudo bash -E - && sudo apt-get install -y nodejs
```

运行完检查node和npm是否安装

```shell
node -v
npm -v
```

我安装完并没有安装npm，wsl的问题，import的虚拟机有点问题
