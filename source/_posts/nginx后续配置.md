---
title: nginx后续配置
copyright: true
date: 2019-03-13 11:45:49
tags: [Hexo,Linux,Nginx]
categories: 疑难杂症
top:
---
备案通过后，后续的一些工作
<!--more-->

#### https搭载

1. 在阿里云申请ssl证书，下载`nginx`版本的证书，在`nginx`安装目录新建`cert`目录

```shell
mkdir cert
```

2. 用`xshell`将两个密钥传输到目录下。

```shell
put 路径 #本地路径
```

3. 在配置文件里，修改以下信息：

```shell
vim /etc/nginx/nginx.conf
```

```shell
server {
        listen       80;
        server_name  www.caiguoyu.cn;

        rewrite ^(.*) https://$server_name$1 permanent; #在这里增加这一句，用来将80端口转发到https，不要改动
```


```shell
server {
        listen       443 ssl ;  #默认开启
        server_name  www.caiguoyu.cn;  #域名

        ssl_certificate     /usr/local/nginx/cert/1804286_www.caiguoyu.cn.pem; #目录如果不正确，用reload指令查找试试
        ssl_certificate_key /usr/local/nginx/cert/1804286_www.caiguoyu.cn.key;

    #   ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;

        ssl_ciphers  ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers  on;

        location / {
            root   /var/www/hexo;
            index  index.html index.htm;
        }
        error_page  404              /404.html;

    }
```

4. 在阿里云的安全组信息增加443端口，重新加载`nginx -s reload `，直接访问http类地址即可转向https

5. 如果要实现其它域名解析到https，可以在域名解析服务里直接跳转https网址,如`CNAME	 @ www.caiguoyu.cn`

6. 网站底部备案信息，在`themes\next\layout\_partials\footer.swig`里，适当位置加上

```
{% if theme.footer.powered %}
<div class="BbeiAn-info">
{{ __('苏ICP备')}} -
<a target="_blank"  href="http://www.miitbeian.gov.cn/">19010692号</a>
</a>
</div>
{% endif %}

```

#### Attention:相关信息自行更换
#### 一些指令

```shell
nginx -s reload #重新加载
nginx -t #测试，通过报succeed
```

>重新加载，会报错误信息，可以用来调试