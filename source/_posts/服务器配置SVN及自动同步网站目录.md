---
title: 服务器配置SVN及自动同步网站目录
date:  2017/11/22
tags: [技术]
---

> 安装环境：CentOS 6 + Nginx

<!-- more -->

## 1. 服务器端安装SVN
```
# yum install subversion
# svnserve --version  //检查一下是否安装成功，成功会显示版本信息
# mkdir -p /opt/svn/repositories   //创建SVN版本库目录，目录可自定义
# svnadmin create /opt/svn/repositories //创建版本库，目录需在版本库目录下
```

## 2. SVN版本库文件配置
1. 进入版本库目录，`/opt/svn/repositories/conf`，有三个文件需要配置：
`authz 是权限控制文件`  
`passwd 是账号密码文件`  
`svnserve.conf 是SVN服务配置文件`  
2. 打开`passwd`文件，在[user]下方添加用户和密码，格式为：账号=密码，如 www = www 或者 w= w  
3. 打开`authz`文件，在末尾添加以下代码：
```
[/]
www = rw
w = r
```
  意思是版本库的根目录，用户www对其有读写权限，用户w对其只有读权限。  
4. 打开`svnserve.conf`，添加以下代码：
```
anon-access = read #匿名用户可读
auth-access = write #授权用户可写
password-db = passwd #使用哪个文件作为账号文件
authz-db = authz #使用哪个文件作为权限文件
realm = /opt/svn/repositories # 认证空间名，版本库所在目录
```

## 3. 启动SVN版本库
```
# svnserve -d -r /opt/svn/repositories
```

## 4. 自动同步网站目录
>这里我的SVN版本库是 `/opt/svn/repositories`  
网站目录是 `/data/wwwroot/105668.win`

### 1. 检出一个项目到网站目录
```
# svn checkout file:///opt/svn/repositories /data/wwwroot/105668.win 
```
这时，网站目录已成为SVN的工作副本，我们要做的就是让这个工作副本自动更新，利用hooks实现自动更新。

### 2. 添加钩子(hooks)文件
在`/opt/svn/repositories/hooks`目录下新建文件`post-commit`,文件内容如下：
```
#!/bin/sh 
export LANG="zh_CN.UTF-8"    #防止乱码 
svn update /data/wwwroot/105668.win --username www --password www --no-auth-cache #设置登陆账号密码并不缓存 
```
`username` 和 `password` 后跟着你刚才设置的版本库目录账号密码，将`post-commit`文件权限设置为755

## 5. 本地SVN配置

### 1. 安装SVN
省略，实在太简单了 --

### 2. checkout
在本地任意位置创建目录，右键 checkout ，

![checkout][1]

点ok，输入设置好的帐号和密码。  
可以在目录下新建个文件commit试一下，对应的网站目录里有没有新建的文件。

[1]:https://i.loli.net/2017/11/22/5a150c7e4a1fd.jpg
