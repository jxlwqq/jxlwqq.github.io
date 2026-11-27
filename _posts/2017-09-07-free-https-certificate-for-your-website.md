---
layout: post
title: "给你的网站免费配置上 HTTPS 证书"
date: 2017-09-07 22:32:00 +0800
categories: https nginx ssl
---

现在越来越多的网站或服务增加了 HTTPS 证书，苹果 AppStore、微信小程序等也已强制要求开发者需提供 HTTPS 的后端接口。在阿里云 / 腾讯云上有一年期的免费赛门铁克 SSL 证书可供尝鲜，但续用则需要付费。

Let's Encrypt 作为一个公共且免费 SSL 的项目逐渐被广大用户传播和使用，是由 Mozilla、Cisco、Akamai、IdenTrust、EFF 等组织人员发起，主要的目的也是为了推进网站从 HTTP 向 HTTPS 过度的进程，目前已经有越来越多的商家加入和赞助支持。

而 Certbot 是由 Let’s Encrypt 官方推荐的一款快速获得网站加密证书的 Python 脚本，简单易用。

但是在 CentOS 6.\* 环境下，由于 Python 的版本问题（系统自带的 Python 是 2.6 版本，但是由于业务需要，又安装了 2.7 版本的 Python），一直会有各种各样的报错，StackOverflow 和 Github 上也没有找到好的解决方案。

好在 Let’s Encrypt 推荐了多种其他语言版本的工具用来快速获取证书。<https://letsencrypt.org/docs/client-options/>

在此，我选择了 acme.sh 这一 Bash 脚本，安装较 Certbot 更方便。

主要步骤如下：

# 1. 安装 **acme.sh**

安装很简单，一个命令：

```
curl https://get.acme.sh | sh
```

普通用户和 root 用户都可以安装使用.

安装过程进行了以下几步:

1. 把 acme.sh 安装到你的 **home** 目录下:

```
~/.acme.sh/
```

并创建 一个 bash 的 alias, 方便你的使用: `acme.sh=~/.acme.sh/acme.sh`

2). 自动为你创建 cronjob, 每天零点自动检测所有的证书, 如果快过期了, 需要更新, 则会自动更新证书，可以通过 `crontab -l` 查看

```
2 0 * * *"/root/.acme.sh"/acme.sh --cron --home"/root/.acme.sh"> /dev/null
```

\*\* 安装过程不会污染已有的系统任何功能和文件 \*\*, 所有的修改都限制在安装目录中: `~/.acme.sh/`

# 2. 生成证书

**acme.sh** 实现了 **acme** 协议支持的所有验证协议.

一般有两种方式验证: http 和 dns 验证.

### 1. http 方式需要在你的网站根目录下放置一个文件, 来验证你的域名所有权, 完成验证. 然后就可以生成证书了.

```
acme.sh --issue -d mydomain.com -d www.mydomain.com --webroot /home/wwwroot/mydomain.com/
```

只需要指定域名, 并指定域名所在的网站根目录. **acme.sh** 会全自动的生成验证文件, 并放到网站的根目录, 然后自动完成验证. 最后会聪明的删除验证文件. 整个过程没有任何副作用.

如果你用的 **apache** 服务器, **acme.sh** 还可以智能的从 **apache** 的配置中自动完成配置, 你不需要指定网站根目录:

```
acme.sh --issue -d mydomain.com --apache
```

如果你还没有运行任何 web 服务, **80** 端口是空闲的, 那么 **acme.sh** 还能假装自己是一个 webserver, 临时听在 **80** 端口, 完成验证:

```
acme.sh --issue -d mydomain.com --standalone
```

### 2. dns 方式, 在域名上添加一条 txt 解析记录, 验证域名所有权.

这种方式的好处是, 你不需要任何服务器, 不需要任何公网 ip, 只需要 dns 的解析记录即可完成验证.

```
acme.sh --issue --dns -d mydomain.com
```

然后, **acme.sh** 会生成相应的解析记录显示出来, 你只需要在你的域名管理面板中添加这条 txt 记录即可.

等待解析完成之后, 重新生成证书:

```
acme.sh --renew -d mydomain.com
```

注意第二次这里用的是 `--renew`

dns 方式的真正强大之处在于可以使用域名解析商提供的 api 自动添加 txt 记录完成验证.

**acme.sh** 目前支持 cloudflare, dnspod, cloudxns, godaddy 以及 ovh 等数十种解析商的自动集成.

以 dnspod 为例, 你需要先登录到 dnspod 账号, 生成你的 api id 和 api key, 都是免费的.

然后:

```
export DP_Id="1234"

export DP_Key="sADDsdasdgdsf"

acme.sh --issue --dns dns_dp -d aa.com -d www.aa.com
```

证书就会自动生成了. 这里给出的 api id 和 api key 会被自动记录下来, 将来你在使用 dnspod api 的时候, 就不需要再次指定了.

直接生成就好了:

```
acme.sh --issue -d mydomain2.com --dns dns_dp
```

# 3. 修改 Web 服务器配置文件

以 nginx 为例。

```
http {

# 新增

server {

listen 80 default_server;

# 新增

listen 443 ssl;

ssl_certificate /etc/nginx/ssl/mydonain.cer;

ssl_certificate_key /etc/nginx/ssl/mydomain.key;

ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

ssl_prefer_server_ciphers on;

# 兼容其他老浏览器的 ssl_ciphers 设置请访问 https://wiki.mozilla.org/Security/Server_Side_TLS

# 其他省略

}

}
```

# 4. copy/ 安装证书

前面证书生成以后, 接下来需要把证书 copy 到真正需要用它的地方.

注意, 默认生成的证书都放在安装目录下: `~/.acme.sh/`, 请不要直接使用此目录下的文件, 例如: 不要直接让 nginx/apache 的配置文件使用这下面的文件. 这里面的文件都是内部使用, 而且目录结构可能会变化.

正确的使用方法是使用 `--installcert` 命令, 并指定目标位置, 然后证书文件会被 copy 到相应的位置,

例如:

```
acme.sh --installcert -d mydomain.com --key-file /etc/nginx/ssl/mydomain.key --fullchain-file /etc/nginx/ssl/mydonain.cer
```

最后，重启 nginx 服务：

```
service nginx force-reload
```

这里用的是 `service nginx force-reload`, 不是 `service nginx reload`, 据测试, `reload` 并不会重新加载证书, 所以用的 `force-reload`。

# 5. 更新证书

目前证书在 60 天以后会自动更新, 你无需任何操作. 今后有可能会缩短这个时间, 不过都是自动的, 你不用关心.

# 6. 更新 acme.sh

目前由于 acme 协议和 letsencrypt CA 都在频繁的更新, 因此 acme.sh 也经常更新以保持同步.

升级 acme.sh 到最新版 :

```
acme.sh --upgrade
```

如果你不想手动升级, 可以开启自动升级:

```
acme.sh --upgrade --auto-upgrade
```

之后, acme.sh 就会自动保持更新了.

你也可以随时关闭自动更新:

```
acme.sh --upgrade --auto-upgrade 0
```
