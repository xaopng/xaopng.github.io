---
title: Linux安装docker
abbrlink: 63079
date: 2023-06-20 20:00:42
tags:
---

## 懒人脚本（官方）

{% hideToggle 使用官方脚本安装docker %}
{% note   warning simple %}
官方出品的一键安装脚本（脚本会区分不同的操作系统且脚本会安装体验版（edge版）而不是稳定版（stable版）且最好不要用于生产环境）
{% blockquote docker https://github.com/docker/docker-install  %}
docker安装脚本
{% endblockquote %}
{% endnote %}

1. 执行下面命令

```bash
export DOWNLOAD_URL="https://mirrors.tuna.tsinghua.edu.cn/docker-ce"
sudo wget -qO- https://get.docker.com/ | bash
```

2. 验证安装是否成功

```bash
docker --version
```

3. 输出为下面这样就安装成功了

```bash
Docker version 18.06.1-ce, build e68fc7a
```

{% endhideToggle %}

## CentOS/Ubuntu/Debian

三大平台的安装都可以参考清华园镜像提供的方法：

{% blockquote 清华大学开源软件镜像站 https://mirrors.tuna.tsinghua.edu.cn/help/docker-ce/ %}
清华源镜像提供的docker安装教程，docker官方的自动脚本清华源也提供了使用清华源下载软件包的修改
{% endblockquote %}

## docker换源

{% note   info simple %}
目前网上的换源教程大部分都是使用清华源、科大源、网易云源等等，不过目前都失效了，查了一下，阿里云又换源的教程，需要注册阿里云账号  
{% endnote %}

{% blockquote 阿里云 https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors %}
docker镜像加速器，注意：访问这个地址需要登录阿里云 
{% endblockquote %}
