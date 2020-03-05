---
title: linux权限
copyright: true
date: 2019-09-19 19:34:59
tags: [Linux,权限]
categories:
- 疑难杂症
top:
---

递归
```
chmod -R 777 mmmmm
```

4代表读权限，2代表写权限，1代表执行权限

```
ls -l
```
```
-rw-------  1 root root  400 Sep 19 19:01 authorized_keys
```
第一个数字表示文件类型，文件（-）、目录（d），链接（l）

后面表示权限

r w x -  
读 写 运行 无  
4 2 1

> 三组分别是 所有者权限 同组权限 其他成员权限

数字代表连接的文件数

用户 用户组 大小（字节） 修改时间 文件名

##### 扩展
linux中 /代表根目录 ~代表当前用户的用户目录，一般是root

.ssh目录一般隐藏在~下面。