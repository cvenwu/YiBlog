---
title: chatgpt与Telegram机器人的邂逅
date: 2022-12-16 18:16:47
tags:
sticky: 1 # 表示文章是否指定，数值越大优先级越高
updated:
categories:
keywords:
description:
top_img:
comments:
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---

## 环境准备
1. 拥有一台可以访问外网的服务器，最好是部署在非中国境内的，因为访问Telegram API需要
2. chatGPT需要有API Token

## 方式一：Docker运行安装

### 安装Docker
执行如下脚本安装docker: 

```shell
# 先卸载原来的，不管有没有
apt-get remove docker docker-engine docker.io containerd runc
apt-get update

# 必备软件包
apt install apt-transport-https ca-certificates curl gnupg2 software-properties-common

# 将官方 Docker hub 的 GPG key 添加到系统中
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

# 将 Docker 版本库添加到APT源
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

# 使用新添加的repo中的Docker包更新包数据库
apt update

# 要从Docker repo而不是默认的Debian repo安装
apt install docker-ce

# 安装Docker
apt install docker-ce

# docker镜像源
sudo mkdir -p /etc/docker                           # /etc/创建 docker 文件夹(目录)
# 创建daemon.json文件，添加docker镜像加速，可以在阿里云，腾讯创建个人镜像服务，免费的。
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://ym588h85.mirror.aliyuncs.com"]
}
EOF
# 重载daemon-reload文件
sudo systemctl daemon-reload
# 重启 docker
sudo systemctl restart docker
# 开启docker自启
sudo systemctl enable docker.service
```

## 方式二：源码安装
> 需要安装Go开发环境, 至少需要Go1.16以上


### 安装Golang环境
```shell
wget https://golang.org/dl/go1.16.3.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.16.3.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin >> ~/.bash_profile
source ~/.bash_profile
```

### 仓库克隆并进行配置

```shell
git clone https://github.com/houko/wechatgpt
cd wechatgpt
go build -o main main.go
cp config/config.yaml.example local/config.yaml
```

### 按照教程填入参数并运行对应的脚本
```shell
vim local/config.yaml
```
[参考](https://github.com/houko/wechatgpt)


