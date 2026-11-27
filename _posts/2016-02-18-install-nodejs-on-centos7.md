---
layout: post
title: "centos7系统下安装nodejs开发环境"
date: 2016-02-18 16:19:00 +0800
categories: centos nodejs linux
---

**![](/assets/images/install-nodejs-on-centos7/img-01.png)**

**1)安装基础工具（if not exists）**

yum install -y net telnet tools vim wget ntp

**2)同步系统时间（if necessary）**

ntpdate time-a.nist.gov

**3)安装nodejs编译及依赖相关软件（if not exists）**

yum install -y gcc gcc-c++ openssl-devel python

**4)获取nodejs源码包（v5.6.0版本，其他版本可从 <https://nodejs.org/en/download/> 获取）**

wget https://nodejs.org/dist/v5.6.0/node-v5.6.0.tar.gz

**5)解压**

tar zxvf node-v5.6.0.tar.gz

**6)配置、编译、安装**

cd node-v5.6.0

./configure --prefix=/usr/local/node

make && make install

**7)配置nodejs环境**

vim /etc/profile

文末追加配置参数

export NODE\_HOME=/usr/local/node  
export PATH=$NODE\_HOME/bin:$PATH  
export NODE\_PATH=$NODE\_HOME/lib/node\_modules:$PATH

**8)生效nodejs配置**

source /etc/profile

**9)查看node及npm版本**

node -v

npm -v

**10)安装express web框架**

npm install express --save

**11)进一步配置express**

可参考<http://www.expressjs.com.cn/>

**12)学习资料**

[Alibaba:七天学会NodeJS](http://nqdeng.github.io/7-days-nodejs/)

[Node即学即用](http://pan.baidu.com/s/1jMSR8)

[node+mongodb 建站攻略（一期）](http://www.imooc.com/learn/75)

[node建站攻略(二期)——网站升级](http://www.imooc.com/learn/197)

[带你学习Jade模板引擎](http://www.imooc.com/learn/259)
