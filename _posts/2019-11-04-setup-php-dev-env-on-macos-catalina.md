---
layout: post
title: "在 macOS Catalina 10.15 搭建 PHP 开发环境"
date: 2019-11-04 23:33:49 +0800
categories: macos php
---

2019 年 10 月 8 日，苹果公司正式发布了新一代 [macOS](https://www.apple.com/cn/macos/catalina/)，版本为 Catalina (11.15)。

macOS Catalina 预装了 Ruby(2.6.3)、PHP(7.3.9)、Perl(5.18.4)、Python(2.7.16) 等常用的脚本语言，以及 Apache(2.4.41) Web 服务器。

需要注意的是，在新版本中，zsh 已取代 bash 成为新版操作系统中的默认 shell。需要个性化配置 zsh 的同学，可以参考少数派的这篇文章：[让你的 Mac 提前用上 macOS Catalina 的 Shell——Oh My Zsh 配置指南](https://sspai.com/post/55176)。本文不再复述。

以下是我的 MNMP（macOS-nginx-MySQL-PHP）的安装过程。

> 本教程用使用了三处代替：
>
> - 使用 iTerm2 代替了系统自带的命令行终端
> - 使用 nginx 代替了系统自带的 Apache
> - 使用 自行安装的 PHP7.4 代替了系统自带的 PHP7.3.9

#### 安装 iTerm2

推荐 [iTerm2](http://www.iterm2.com/)，iTerm2 功能强大，可以替代系统默认的命令行终端。下载解压后，将 iTerm2 直接拖入"应用程序"目录。

#### 安装 PhpStorm

推荐 [JetBrains PhpStorm](https://www.jetbrains.com/phpstorm/) 作为集成开发工具。

#### 安装 Xcode

[Xcode](https://itunes.apple.com/cn/app/xcode/id497799835) 是苹果出品的包含一系列工具及库的开发套件。通过 AppStore 安装最新版本的 Xcode(9.0)。我们一般不会用 Xcode 来开发后端项目。但这一步也是**必须**的，因为 Xcode 会附带安装一些如 Git 等必要的软件。

#### 安装 Command Line Tools for Xcode

这一步会帮你安装许多常见的基于 Unix 的工具。Xcode 命令行工具作为 Xcode 的一部分，包含了 GCC 编译器。在命令行中执行以下命令即可安装：

```shell
xcode-select --install # 安装 Xcode Command Line Tools
```

当 Xcode 和 Xcode Command Line Tools 安装完成后，你需要启动 Xcode，并点击同意接受许可协议，然后关闭 Xcode 就可以了。这一步骤也是**必须**的，否则 Xcode 包含的一系列开发工具都将不可用。

#### 安装 Homebrew

[Homebrew](http://brew.sh/index_zh-cn.html) 作为 macOS 不可或缺的套件管理器，用来安装、升级以及卸载常用的软件。在命令行中执行以下命令即可安装：

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" # 使用系统自带的 ruby 安装 Homebrew
```

安装后可以修改 Homebrew 源，国外源一直不是很给力，这里我们将 Homebrew 的 git 远程仓库改为[中国科学技术大学开源软件镜像](https://lug.ustc.edu.cn/wiki/mirrors/help/brew.git)：

```shell
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git # 替换brew.git:

cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git # 替换homebrew-core.git:

echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.zshrc # 替换Homebrew Bottles源:

source ~/.zshrc
```

#### 安装 PHP 7.4

安装 PHP7.4.\* 来代替系统自带的 PHP7.3：

```shell
brew install php
```

启动 php 服务：

```php
brew services start php
```

替换系统自带的 php-fpm：

```php
echo 'export PATH="/usr/local/opt/php/sbin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

查看版本信息：

```shell
php -v
php-fpm -v
```

#### 安装 MySQL

推荐 MySQL 8.0 作为数据库服务器：

```shell
brew install mysql
```

当然，你也可以选择安装 PostgreSQL 或者 MariaDB。

安装完成后，启动 MySQL：

```shell
brew services start mysql
```

进入 MySQL 服务器：

```shell
mysql -u root -p
```

设置 root 密码、安全等级等参数：

```shell
mysql_secure_installation
```

按照步骤提示一步一步来即可。

#### 安装 Redis

安装 redis 服务器：

```shell
brew install redis
```

安装完成后，启动 Redis：

```shell
brew services start redis
```

使用 redis 客户端：

```shell
redis-cli
```

#### 安装 nginx

这里我们选择 nginx 代替系统自带的 Apache，作为我们的 Web 服务器：

```php
brew install nginx
```

启动 nginx 服务：

```shell
brew services start nginx
```

查看已安装的 brew services:

```shell
brew services list
```

#### 配置 nginx.conf 文件

通过以下命令可以查看 nginx.conf 文件的位置：

```bash
nginx -h
```

输出：

```bash
nginx version: nginx/1.17.3
Usage: nginx [-?hvVtTq] [-s signal] [-c filename] [-p prefix] [-g directives]
Options:
-?,-h : this help
-v : show version and exit
-V : show version and configure options then exit
-t : test configuration and exit
-T : test configuration, dump it and exit
-q : suppress non-error messages during configuration testing
-s signal : send signal to a master process: stop, quit, reopen, reload
-p prefix : set prefix path (default: /usr/local/Cellar/nginx/1.17.3_1/)
-c filename : set configuration file (default: /usr/local/etc/nginx/nginx.conf)
-g directives : set global directives out of configuration file
```

打开配置文件：

```bash
vi /usr/local/etc/nginx/nginx.conf
```

在文件末尾可以看到：

```bash
include servers/*;
```

它将同目录下的servers目录里的文件都包含了进来，由此，我们可以在servers文件里创建开发项目的配置信息：

```bash
cd /usr/local/etc/nginx/servers/
vi test.conf
```

将以下配置信息，写入 test.conf文件中：

```nginx
server {
    listen 8099;
    server_name localhost;
    root /home/www/php-project;
    rewrite . /index.php;
    location / {
    index index.php index.html index.htm;
    autoindex on;
    }
    #proxy the php scripts to php-fpm
    location ~ \.php$ {
        include /usr/local/etc/nginx/fastcgi.conf;
        fastcgi_intercept_errors on;
        fastcgi_pass 127.0.0.1:9000;
    }
}
```

在上述的`/home/www/php-project`的目录下，我们创建一个 index.php 文件：

```bash
vim /home/www/php-project/index.php
```

写入内容：

```php
<?php
    phpinfo();
```

重启 nginx:

```bash
brew services restart nginx
```

打开浏览器，访问`http://localhost:8099`，即可访问到关于 PHP 配置的信息。

#### 安装 Composer

Composer 是 PHP 用来管理依赖（dependency）关系的工具。你可以在自己的项目中声明所依赖的外部工具库（libraries），Composer 会帮你安装这些依赖的库文件。

安装并替换镜像：

```bash
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ # 改为阿里云的国内源
```

#### 安装 PHP 扩展

以 php-redis 扩展为例，有下载源码包来进行安装或者 pecl install 安装：

```shell
wget https://pecl.php.net/get/redis-5.1.0.tgz # 下载源码包
tar -zxvf redis-5.1.0.tgz # 解压
cd redis-5.1.0 # 进入目录
phpize # 生成编译配置
./configure # 编译配置检测
make # 编译
make install # 安装
```

扩展安装完成后，我们还需最后一步，修改`php.ini`文件，并重启 PHP 服务：

```shell
vi /usr/local/etc/php/7.4/php.ini # 追加 extension=redis.so
brew services restart php # 重启 php 服务
php -m |grep redis # 查看是否安装成功
```

或者使用 pecl 安装：

```shell
pecl install redis
```

详细步骤可参考官方文档：[phpredis install](https://github.com/phpredis/phpredis/blob/develop/INSTALL.markdown)

[php](https://learnku.com/blog/know-nothing/tags/php_28)
[mysql](https://learnku.com/blog/know-nothing/tags/mysql_487)
[composer](https://learnku.com/blog/know-nothing/tags/composer_10)
[redis](https://learnku.com/blog/know-nothing/tags/redis_17)
[homebrew](https://learnku.com/blog/know-nothing/tags/homebrew_12192)
[phpstorm](https://learnku.com/blog/know-nothing/tags/phpstorm_4996)
[laravel-admin](https://learnku.com/blog/know-nothing/tags/laravel-admin_10462)

> 本作品采用[《CC 协议》](https://learnku.com/docs/guide/cc4.0/6589)，转载必须注明作者和本文链接
