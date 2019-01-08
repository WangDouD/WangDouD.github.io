---
title: 用免费的Let's Encrypt SSL证书给网站加上小绿锁
date:  2017/11/2
tags: [技术]
---

![https://wdd.space/][1]

现在非常流行的免费SSL证书非Let's Encrypt所有了，经过近几年的发展，Let's Encrypt的安装也变得非常简单，这里详细介绍一下Let's Encrypt的安装和配置过程。
环境：`CentOS 6 + Apache 2.2`
CertBot是一个很好的工具,我们使用它来安装Let's Encrypt。

<!--more-->


## 一、准备
### 1. 为CertBot安装EPEL库
```
yum -y install epel-release 
```
### 2. 安装CertBot
```
wget https://dl.eff.org/certbot-auto
chmod 755 certbot-auto
```
## 二、安装SSL证书

### 1. 安装证书
```
./certbot-auto --apache
```
### 2. 按照提示操作
（如果Python版本低于2.7会提示版本过低，可以先忽略）

`Enter email address (used for urgent renewal and security notices) (Enter 'c' to cancel):输入管理员邮箱`

提示输入管理员邮箱，因为Let's Encrypt的免费SSL证书有效期是90天，这个邮箱的作用就是在证书快到期之前会发邮件提醒续期。

`(A)gree/(C)ancel: A`

`(Y)es/(N)o: Y`

`Which names would you like to activate HTTPS for?`

选择要安装SSL证书的域名，多个域名可以中间空格

### 3. 成功后，会在/etc/letsencrypt/live/域名/下生成4个证书文件：

`cert.pem ->`、`chain.pem ->`、`fullchain.pem ->`、`privkey.pem ->`

## 三、编辑ssl.conf
### 1.打开`/etc/httpd/conf.d/ssl.conf`，并添加以下语句
```
<VirtualHost _default_:443>
SSLEngine on
DocumentRoot "网站目录"
ServerName 域名:443
SSLCertificateFile fullchain.pem的路径位置（如/etc/letsencrypt/live/www.baidu.com/fullchain.pem）
SSLCertificateKeyFile privkey.pem的路径位置（如/etc/letsencrypt/live/www.baidu.com/privkey.pem）
SSLCertificateChainFile chain.pem的路径位置（如/etc/letsencrypt/live/www.baidu.com/chain.pem）
</VirtualHost>
```
如有多个域名（包括子域名）如要整段继续添加，`SSLCertificateFile`、`SSLCertificateKeyFile`和`SSLCertificateChainFile`字段不用修改，因为证书唯一。

### 2.在这个文件中查找` Listen 443 `，并把前面的#去掉。

### 3.查找`SSLCipherSuite `把这个一行修改为
`SSLCipherSuite AESGCM:ALL:!DH:!EXPORT:!RC4:+HIGH:!MEDIUM:!LOW:!aNULL:!eNULL;`

### 4.查找`SSLProtocol all `把这一行修改为`SSLProtocol all -SSLv2 -SSLv3`

## 四、重启apache服务：
```
service httpd restart
```
这个时候访问 `https://域名/`，应该已经可以了。

## 五、设置自动续期任务
因为Let's Encrypt的免费SSL证书有效期是90天，所以我们可以设置自动续期。先手动续期一次试一下：
```
./certbot-auto renew --dry-run
```
然后进入cron定时任务编辑：
```
crontab -e
```
输入a进入编辑状态，然后用方向键选到新的一行，
加上规则：
```
0 3 1 * * /root/certbot-auto renew –renew-hook
0 3 1 * * /root/certbot-auto renew --dry-run –renew-hook
```
按“ESC”退出编辑状态，输入:wq保存并退出。
查看一下是否存在刚才添加的定时命令：
```
crontab -l
```

[1]: https://i.loli.net/2017/11/02/59fb10bb4c43b.jpg