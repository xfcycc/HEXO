---
title: Hexo分类页面经常404
copyright: true
date: 2019-03-05 21:07:36
tags: [Hexo,git,Linux]
categories: 疑难杂症
top:
---
#### 问题描述
最近经常发现访问分类页面会404，主要是`LeetCode`分类。
观察发现可能是大小写问题。
于是到服务器里看看。

<!--more-->

```shell
cd /var/www/hexo/categories/
ls
```

果然存在一个文件下是`Leetcode`,git的上传是忽略大小写的，于是我们访问 `server/categories/LeetCode/`就会404。

---
#### 解决
在本地的博客文件夹里，找到`.deploy_git/.git/confit`，将里面的`ignorecase = true`改为`ignorecase = false`，这样上传就不会忽略大小写。
接着git同步即可。

```
hexo d -g
```

---
#### 愚蠢的地球人
由于我要重新同步，想先清空仓库，不小心

```shell
cd /var/repo/hexo.git
rm -rf *
```

这下真的空了，`hexo d`直接报错。
重新建立仓库

```shell
sudo git init --bare hexo.git
```

建立脚本

```shell
vim /var/repo/hexo.git/hooks/post-receive
#   #!/bin/bash
#   git --work-tree=/var/www/hexo --git-dir=/var/repo/hexo.git checkout -f
chmod +x post-receive
```

重新`hexo d -g`，

```shell
/var/www/hexo/categories/
```

发现已经有`LeetCode`文件夹，网页也可以访问，解决。