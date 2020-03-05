---
title: Win10经常弹出账户控制权限解决办法
copyright: true
date: 2019-02-02 16:13:38
tags: Win10
categories: 疑难杂症
top:
---
最近使用Foxmail每次开机都会跳出来“是否允许更改计算机”的弹框，在防火墙里增加的白名单也没用。在网上查找相关资料，发现有两种解决办法。
1. 使用微软官方提供的UAC权限工具增加白名单，较繁琐，不考虑。
2. Win+R，打开注册表“regedit”，找到```HKEY_CURRENT_USERS\Software\Microsoft\WindowsNT\CurrentVersion\AppCom patFlags\Layers```
    新建值，类似这样

![img](https://oss.caiguoyu.cn/pictures/olds/651335cfgy1fztqteinl8j20fm00n3yb.jpg)


