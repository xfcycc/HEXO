---
title: 关于c盘空间清理的若干办法总结
tags:
  - Win10
  - 系统优化
categories: 疑难杂症
copyright: true
date: 2021-01-24 15:39:54
top:
---

> c盘空间清理办法总结



### 软件清理

使用专业的软件如**火绒**来清理垃圾



### 脚本清理

以下是一个清理垃圾的脚本，运行时候最好关闭其他软件，运行时间几分钟不等。

使用的时候新建一个***txt***文件，将所有内容复制进去，保存，再把后缀改为***bat***，右键用管理员权限运行即可。

> 如果看不到后缀名，在任意一个文件夹上方点击查看，将文件扩展名选项打钩

``````bat
@echo off 
echo 正在清除系统垃圾文件，请稍等...... 
del /f /s /q %systemdrive%\*.tmp 
del /f /s /q %systemdrive%\*._mp 
del /f /s /q %systemdrive%\*.log 
del /f /s /q %systemdrive%\*.gid 
del /f /s /q %systemdrive%\*.chk 
del /f /s /q %systemdrive%\*.old 
del /f /s /q %systemdrive%\recycled\*.* 
del /f /s /q %windir%\*.bak 
del /f /s /q %windir%\prefetch\*.* 
rd /s /q %windir%\temp & md %windir%\temp 
del /f /q %userprofile%\cookies\*.* 
del /f /q %userprofile%\recent\*.* 
del /f /s /q "%userprofile%\Local Settings\Temporary Internet Files\*.*" 
del /f /s /q "%userprofile%\Local Settings\Temp\*.*" 
del /f /s /q "%userprofile%\recent\*.*" 
echo 清除系统LJ完成！ 
echo. & pause
``````



### 软件数据迁移

##### QQ与微信

在这两个软件的设置里，都可以找到本地文件的保存位置，将个人文件夹的位置改为其它硬盘，已有的数据也可以直接迁移。

##### 浏览器，迅雷等下载软件

这里以***Chrome***为例，在**设置--高级--下载内容**里面可以设置默认下载位置。



### 系统文件迁移

##### 下载文件夹

***WIn10***默认有一个下载文件夹，这个路径可以改变并迁移原有数据。

![](https://oss.caiguoyu.cn/pictures/20210124/211241.png)



##### 虚拟内存页面文件

右键点击**我的电脑**，选择**属性--高级系统设置--高级--性能设置--高级--虚拟内存更改**

在比较大的硬盘分区存放**托管的系统**，c盘只留一点就可以了。

在各个硬盘根目录可以看到***pagefile.sys***文件，这个就是页面文件了，重启电脑，就会发现该文件已经迁移到你选择的硬盘分区。

> 在任意一个文件夹上方点击查看，勾选隐藏的文件。

![](https://oss.caiguoyu.cn/pictures/20210124/211242.png)

![](https://oss.caiguoyu.cn/pictures/20210124/211243.png)

##### 休眠文件

> 该选项谨慎使用，尤其不要在公司电脑上尝试。

针对有**休眠**功能的电脑。

> 在Win10里，睡眠是指计算机未完全关闭，所有的运行文件保存在内存里。
>
> 休眠是将内存文件保存到硬盘里面，再完全关闭计算机，按下电源按钮后，文件会恢复到内存

以下就是休眠文件，如果不需要这个功能，可以关闭，或者删除这个文件。

![](https://oss.caiguoyu.cn/pictures/20210124/211244.png)

关闭**休眠**功能，右键**菜单**，用管理员权限打开***PowerShell***，输入```powercfg -h off```

