---
title: 腾讯轻量服务器部署hexo博客
sticky: 1
password: test
message: 文章尚未撰写完成，完成后会解密
date: 2022-12-20 22:07:28
tags:
updated:
categories:
keywords:
description:
top_img:
comments:
cover:
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


### 步骤：
```shell
# 安装gcc以及gcc-c++
yum install -y gcc gcc-c++

# 安装PCRE库
cd /usr/local/
wget http://downloads.sourceforge.net/project/pcre/pcre/8.37/pcre-8.37.tar.gz
tar -xvf pcre-8.37.tar.gz
cd pcre-8.37
./configure
make && make install
pcre-config --version

# 安装 openssl 、zlib 、 gcc 依赖
yum -y install make zlib zlib-devel gcc-c++ libtool openssl openssl-devel

# 安装nginx
cd /usr/local/
wget http://nginx.org/download/nginx-1.17.9.tar.gz
tar -xvf nginx-1.17.9.tar.gz
cd nginx-1.17.9
./configure
make && make install

# 修改配置文件server 80 端口下的root项 为/home/www/website;
vim /usr/local/nginx-1.17.9/conf
修改44行的内容为            `root   /home/www/website;`

# 安装nodejs 1.19
cd /usr/local
curl -fsSL https://rpm.nodesource.com/setup_19.x | bash -
sudo yum install -y nodejs
## 验证安装是否成功
node -v
npm -v

# 安装git及新建git用户
yum install git
adduser git
chmod 740 /etc/sudoers
vi /etc/sudoers

在图中![221758-MCIt88](https://cdn.jsdelivr.net/gh/sivanWu0222/UpicImageHosting@dev/uPic/2022-12-20/221758-MCIt88.jpg)如下位置添加
git ALL=(ALL) ALL
vi指令执行之后按i进入输入模式
编辑完成之后按一下esc
然后输入:wq即可退出

chmod 400 /etc/sudoers
sudo passwd git

```

第二部分：这部分所有命令必须以git用户执行
```shell
# 切换git用户并且建立密钥
su git
cd ~
mkdir .ssh
cd .ssh
touch authorized_keys
chmod 600 ~/.ssh/authorized_keys
chmod 700 ~/.ssh

## 此时需要到本地的终端生成SSH密钥, -f 参数指定生成密钥的文件名，避免使用默认的id_rsa会覆盖掉本地之前的密钥文件
ssh-keygen -f id_rsa_gz  -C "gz tencent" -t rsa
## 连续敲两下回车即可生成密钥文件到本地机器的~/.ssh/，此时需要
复制~/.ssh/id_rsa_gz.pub文件的内容, 复制到远程主机的git用户家目录下的.ssh/authorized_keys文件中

# 创建git仓库
cd ~
git init --bare blog.git
vi ~/blog.git/hooks/post-receive

输入如下内容：
git --work-tree=/home/www/website --git-dir=/home/git/blog.git checkout -f
保存退出
chmod +x ~/blog.git/hooks/post-receive
```

第三部分：
```shell
su root
输入密码
cd /home
mkdir www
cd www
mkdir website
## 修改文件夹权限 这步很重要 视频中没有提及
chmod 777 /home/www/website
chmod 777 /home/www
```

第四部分：本地电脑测试连接
```shell
43.139.72.111
ssh -v git@43.139.72.111
ssh -v git@服务器的公网ip
```
如果成功登录到远程服务器则执行成功，如果执行失败，可能原因是因为本地机器之前连接过该服务器，所以在`~/known_hosts`中将服务器IP对应的记录全部删除，重新ssh即可，具体原理可以参考文章[一文读懂authorized_keys和known_hosts](https://blog.csdn.net/qq_26400953/article/details/105145103)

第五部分：修改本地hexo博客根配置文件
```
deploy:
  type: git
  repo: git@:服务器的公网ip/home/git/blog.git
  branch: master
```

第六部分：添加脚本文件，执行命令`touch /etc/init.d/nginx`，内容如下：
```shell
#!/bin/bash
###
#Startup script for the nginx Web Server
#chkconfig: 2345 85 15
nginx=/usr/local/nginx/sbin/nginx
conf=/usr/local/nginx/conf/nginx.conf
case $1 in 
    start) 
        # -n 表示输出的内容不进行换行
        echo -n "Starting Nginx" 
        $nginx -c $conf 
        echo " done."
    ;;
    stop) 
        echo -n "Stopping Nginx" 
        killall -9 nginx 
        echo " done."
    ;;
    test) 
        $nginx -t -c $conf 
        echo "Success."
    ;;
    reload)
        echo -n "Reloading Nginx"
        ps auxww | grep nginx | grep master | awk '{print $2}' | xargs kill -HUP
        echo " done."
    ;;
    restart) 
        $nginx -s reload 
        echo "reload done."
    ;;
    *)
        echo "Usage: $0 {start|restart|reload|stop|test|show}"
    ;;
esac
```
执行命令：`chmod +x nginx`
控制指令如下：
- 启动`service nginx start`
- 停止`service nginx stop`
- 重启`service nginx reload`


此时浏览器中键入公网服务器IP就可以发现是nginx首页了


之后在自己的博客中执行如下命令进行部署：
1. `hexo g`
2. `hexo d` ，如果报错`ERROR Deployer not found: git`，则安装`npm install hexo-deployer-git --save npm install hexo-deployer-git --save`


一些疑问：
1. shell中定义变量的时候等号两边加上空格就会有问题，是为什么：`nginx = /usr/local/nginx`这个有问题，正确的应该是`nginx=/usr/local/nginx`
2. 如果在`/etc/init.d`创建一个文件夹，这个相当于什么，是创建了一个Centos服务么，之后就可以通过`service 服务名 start/stop/reload`来控制么
3. 