---
title: hexo 去除友情链接下划线
copyright: true
date: 2019-10-13 17:45:05
tags: [Hexo,css]
categories:
- 疑难杂症
top:
---

查找网页文件，如下

![image](https://oss.caiguoyu.cn/pictures/20191013/1.png)

经过多次尝试，生效的css文件位置如下路径

```
..\public\css\main.css
```
![image](https://oss.caiguoyu.cn/pictures/20191013/2.png)

但是由于hexo的特殊性，无法直接在这里修改，于是找对应的样式文件。

路径如下

```
..\themes\next\source\css\_common\components\sidebar
```

![image](https://oss.caiguoyu.cn/pictures/20191013/3.png)

，为了不破坏源文件的完整性，尽量不删除语句，只要在这里的a标签加入 ``border-bottom: none;`` 就可以了。

接着，输入命令，即可看到效果。

```
hexo s
```

```
hexo d -g
```

重新打包上传后,在 **public** 文件夹里的css文件应当可以见到这个属性，或者网页里面查找css文件。
![image](https://oss.caiguoyu.cn/pictures/20191013/4.png)

>  如果没有效果，按Ctrl + F5 刷新。

> ~~据悉，该解决方案有某资深前端人士的功劳~~