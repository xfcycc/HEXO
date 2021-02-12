---
title: QQ语音消息提取
copyright: true
date: 2019-02-09 23:10:43
tags: [QQ,微信]
categories: 疑难杂症
top:
---

前段时间有小伙伴告诉我一个妹子的语音消息很好听，无奈不好转发，于是我研究了一下，有两个办法。

<!--more-->

#### 1.通过替换本地文件的办法（仅限安卓手机）

1. 让你的小伙伴先将语音收藏，在以下位置找到收藏的这个语音文件（**amr,slk**均可），简称一：

![img](https://oss.caiguoyu.cn/pictures/olds/651335cfgy1g00mueuvknj20u01hcacc.jpg)

让他将这个文件发给你。

2. 接着，你自己发一个语音，以**TIM**为例，在以下位置找到你刚刚发的语音，简称二：


![img](https://oss.caiguoyu.cn/pictures/olds/651335cfgy1g00n5j8knmj20u01hcabt.jpg)

3. 将小伙伴发给你的文件一名字换成文件二，再覆盖掉文件二，你再播放你发送的语音，就可以听到啦。

当然你自己收藏一段语音再替换原理是一样的，**QQ,TIM,微信** 也没有本质区别，在 **Tencent** 文件夹下都可以找到。



**以上是只有一台手机的情况，如果你身边有一台电脑，有更方便的办法。**

#### 2.工具解密

以下是语音解密器：
[语音播放器](https://pan.baidu.com/s/11YoS4p_t549nCq0DQXHIDQ)

1. 第一步参照第一个办法。
2. 将刚才的文件通过`QQ`传输到电脑上，打开刚才下载的工具，直接解密输出即可。

#### 3.后续更新

目前的手机QQ语音位置变化如下：

```tex
file://我的手机/Android/data/com.tencent.mobileqq/Tencent/MobileQQ/你的qq号/ptt/xxxxx.slk 

// 2021.02.12
```

这里就有你自己发送的，或者别人发送的语音，不需要收藏就可以。

如果你成功接收到了消息，就算他撤回也没用，文件还在。

