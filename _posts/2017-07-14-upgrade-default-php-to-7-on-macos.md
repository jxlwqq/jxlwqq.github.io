---
layout: post
title: "将 MacOS 默认的 PHP 版本升级到 7.*"
date: 2017-07-14 16:19:00 +0800
categories: macos php
---

上接：[在macOS Sierra 10.12搭建PHP开发环境](http://www.cnblogs.com/jxlwqq/p/6001323.html)

#### 设置 brew

```
brew tap homebrew/dupes  
brew tap homebrew/versions  
brew tap homebrew/homebrew-php 
```

#### 安装 PHP 7.1

```
brew install php71
```

#### 优先使用 PHP 7.1

```
export PATH="/usr/local/sbin:$PATH"  
echo 'export PATH="/usr/local/sbin:$PATH"' >> ~/.bash_profile
```

#### 启动 PHP-FPM

```
sudo nginx  
sudo php-fpm --fpm-config /usr/local/etc/php/7.1/php-fpm.conf -D  
mysql.server start
```

这三个命令其实是分别启动nginx、php和mysql，你可以将其封装成一个bash命令，然后就可以一个命令启动所有Web服务。

#### 安装扩展

扩展有两种安装方式：

- brew 安装
- 源码包安装 `推荐`

以 PHP-Redis 扩展 phpredis 为例：  
brew 安装

```
brew install php71-redis
```

源码包安装

```
wget https://pecl.php.net/get/redis-3.1.0.tgz
tar zxvf redis-3.1.0.tgz
cd redis-3.1.0
/usr/local/Cellar/php71/7.1.0_11/bin/phpize # !!!注意!!! 7.1.0_11这个小版本目录可能需要你手动改成你下载的对应的最新版本号。

./configure
make
make install
vi /usr/local/etc/php/7.1/php.ini # 追加 extension=redis.so
# 重启 php-fpm
sudo killall -9 php-fpm
sudo php-fpm --fpm-config /usr/local/etc/php/7.1/php-fpm.conf -D
```

#### 参考

- [Install nginx (with HTTP2), PHP 7.0 and MySQL 5.7 server on Mac OSX El Capitan 10.11](http://wlkns.co/install-nginx-php-mysql-on-mac-osx/)
- [mac上通过brew安装php7](https://www.zybuluo.com/phper/note/313803)
