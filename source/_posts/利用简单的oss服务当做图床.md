---
title: 利用简单的oss服务当做图床
copyright: true
date: 2019-09-27 07:33:26
tags: [Hexo,oss]
categories: 疑难杂症
top:
---

阿里云申请oss存储服务。

创建 Bucket ，域名长一点，不可重复，权限选择私有。

接着绑定域名，最好是二级域名，如果没有域名，用上一步的地址也能用。

![image](https://oss.caiguoyu.cn/pictures/20190927/yuming1.png)

![image](https://oss.caiguoyu.cn/pictures/20190927/yuming2.png)


https证书原来的不合适，需要申请一个新的。

![image](https://oss.caiguoyu.cn/pictures/20190927/zhengshu.png)


接下来上传图片，图片上传到容器后，图片选择公共读权限。

之后就可以直接在md文档中引用图片地址了。

后续：编写一个软件自动化（TODO）

##### bug

访问https的文件错误，换成http就正常访问。

显示

```tex
协议不受支持

客户端和服务器不支持一般 SSL 协议版本或加密套件
```

原因是cdn的https未开启,按需设置或者直接关闭。