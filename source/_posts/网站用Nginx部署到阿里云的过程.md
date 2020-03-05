---
title: 网站用Nginx部署到阿里云的过程
copyright: true
date: 2019-02-28 15:11:55
tags: [Linux,Hexo,ECS,Nginx]
categories: 疑难杂症
top:
---

### 概述

由于Github仓库在国内访问不稳定，导致网站经常卡顿，目前已经完全瘫痪，正好我还有一年的阿里云服务器，趁此学习一下Linux，并搬迁网站。

<!--more-->

---
### 过程

网上太多了，随便找一个就是了

---
### 大致一些坑
##### 如何安装环境
在阿里云服务器里安装`Nginx`，这里我使用的是`Java开发`镜像，自带环境。

##### 无法切换用户
网上通用的办法是新建一个账户来管理，经过我实践证明，这样会遇到无数的坑，对于新手往往无法解决，直接`root`账户走起。

##### ssh认证失败
1. git服务器打开RSA认证
`vim /etc/ssh/sshd_config`
在sshd_config中开启以下几项：

```shell
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile  .ssh/authorized_keys

```
2.  本地ssh
在`c://users/用户名`下面执行命令`ssh-keygen -t rsa -C  "youremail@example.com"`，将生成的`id_rsa.pub`内容复制。

  >此处填写邮箱。
  >用过一次好像就不能用了，每次重新设定都要重新生成。

3.  服务器端设置
创建 .ssh 文件夹和 .ssh/authorized_keys 文件，并赋予相应的权限

```shell
mkdir .ssh
vim .ssh/authorized_keys
#将公钥复制粘贴到authorized_keys
chmod 600 ~/.ssh/authorzied_keys
chmod 700 ~/.ssh
```

4. 然后就可以执行ssh 命令测试是否可以免密登录`ssh -v root@SERVER` ，如果成功就会跳出来一个`yes/no`的命令。
>SWRVER意思是服务器地址


##### 两个仓库傻傻分不清
两个文件夹，一个是仓库，带git后缀，一个是放静态页面的，也就是`Nginx`的首页目录。

##### 创建仓库的指令

`sudo git init --bare hexo.git`

>不要用rm清空仓库！！！！！
##### Nginx配置文件
对于`Nginx`配置文件的位置，有许多不同，参见说明文档，我这里是在

`/etc/nginx/nginx.conf`。

配置如下

``` shell
server {
        listen       80; #80端口
        server_name  ; #域名

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   /var/www/hexo; #静态页面文件，也就是生成的网页文件所在位置
            index  index.html index.htm; #主页文件
   #        proxy_pass http://127.0.0.1:8080/;
        }
        error_page  404              /404.html; #404文件，直接放在根目录

        # redirect server error pages to the static page /50x.html
        #
       # error_page   500 502 503 504  /50x.html;
        location = 404.html {
            root   /var/www/hexo;
        }



```
每次修改后都要重启服务，`sudo service nginx restart`，或者`systemctl restart nginx`。
##### 不能访问/没有权限/不存在

root账号权限最大，值得拥有，文件权限777走起。

##### 本地Hexo文件无法上传

```shell
deploy:
  type: git
  repo:  root@SERVER:/var/repo/hexo.git
  branch: master
```

记得冒号后面有空格，如果还是上传不了，请换root账户。

##### 成功传到库后还是不显示页面
 自动运行的脚本

```shell
vim /var/repo/hexo.git/hooks/post-receive
```

这个脚本是git操作后自动运行的，内容如下

```shell
#!/bin/bash
git --work-tree=/var/www/hexo --git-dir=/var/repo/hexo.git checkout -f
```

之后`chmod +x post-receive`，使之可运行
意思是会将后面的仓库克隆到前面的网站主目录，这样每次更新仓库都可以自动渲染静态页面来更新。

>必须把后缀`sample`去掉
>如果不生效，可以试试直接在shell里运行，看哪里出错，如果出错多半是权限的问题。

##### 网站主目录有文件了，访问IP还是空白/Nginx/tomcat页面
此时访问IP地址应该可以看见网站了，如果看不见，去阿里云查看安全组设置，开放80端口，或者重启`Nginx`服务，代码是`sudo service nginx restart`，或者`systemctl restart nginx`。
此外，阿里云的服务器还需要备案，如果域名解析不能访问，就去备案吧。
##### 访问其它端口
其它端口仍在开放，可以正常使用，`IP+端口`即可。

---
#### 常用的Linux命令总结

```shell
chmod 777  #4代表读取，2代表写入，1代表运行，7就是全权限了
ls -a #显示目录下全部文件和文件夹，包括隐藏的
su #切换用户
cd #切换文件夹
cd .. #返回上一级目录
vim #vim文本编辑器，i编辑，esc退出编辑，：wq退出并保存，：q只退出，如果报错就后面加！
rm -rf #删除 -r代表遍历 -f代表强制 不要加/ ，不建议-f，
Shift+Insert #粘贴，复制是Ctrl+Insert

```

>cd命令注意事项, `cd/var` 表示切换到了根目录的var，`cd var`表示当前路径的var
>直接使用`cd`命令返回的是用户主目录，需要再次`cd ..`才能看到根目录
>![](https://wx1.sinaimg.cn/large/651335cfly1g11h7t3m7fj210g0gvwfb.jpg)
