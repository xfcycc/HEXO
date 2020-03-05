---
title: Hexo功能升级
tags:
  - Hexo
  - css
categories:
  - 疑难杂症
copyright: true
date: 2019-10-26 22:55:48
top:
---



### 直接升级
```shell
git pull
```
失败，停止维护了，换了新仓库

原版本：5.1.4
升级版本：7.4.2

### 克隆新仓库

官方推荐的方式。

先备份

**克隆仓库**

```shell
$ git clone https://github.com/theme-next/hexo-theme-next themes/next-reloaded
```

**切换配置**   

主配置文件：
```yaml
language: zh-CN
------
theme: next-reloaded
```

**比对配置文件**

改动完毕后先测试，测试完成。

**头像设置**

新头像设置移到了主题配置文件下，主题配置文件会覆盖主配置文件

```yaml
avatar:
  url: #https://
```
**版权信息**

新版本版权信息不是 *copyright* 了，改为以下信息

```yaml
creative_commons:
  license: by-nc-sa
  sidebar: false
  post: true
  language:
```

**去除下划线**

见别片（位置稍微有改变）

**侧边栏设置**

如下位置，主要是新版本友情链接有点问题

![image](https://oss.caiguoyu.cn/pictures/20191026/1.png)

**底部文字修改**

``\layout\_partials\footer.swig``

删除支援信息，不过新版本可以直接在配置文件中去除。

```css
{% if theme.footer.powered %}
<div class="BbeiAn-info">
{{ __('苏ICP备')}} - 19010692号
</div>
{% endif %}

{% if theme.footer.powered %}
<div class="BbeiAn-info">
{{ __('')}} 
<a href="https://996.icu"><img src="https://img.shields.io/badge/link-996.icu-red.svg"></a>
</a>
</div>
{% endif %}
```
**更改分类名字**

``C:\Users\caigu\Desktop\GitGit\HexoManager\themes\next-reloaded\languages``  

**搜索设置**  
主题配置文件：

```yaml
local_search: true
```

**更改背景图片和缩放**

新版本在主题配置文件中使自定义CSS生效，然后把文件放在指定位置。**注意是根目录路径**
![image](https://oss.caiguoyu.cn/pictures/20191026/2.png)

![image](https://oss.caiguoyu.cn/pictures/20191026/3.png)

![image](https://oss.caiguoyu.cn/pictures/20191026/4.png)

具体配置见附录



**阅读量显示错误**

报错： *Counter not initialized! More info at console err msg.*

改动：

```yaml
valine:
  visitor: true
leancloud_visitors:
  security: false
```



**字体**

```yaml
font:
  enable: true

  # Uri of fonts host, e.g. //fonts.googleapis.com (Default).
  host:

  # Font options:
  # `external: true` will load this font family from `host` above.
  # `family: Times New Roman`. Without any quotes.
  # `size: x.x`. Use `em` as unit. Default: 1 (16px)

  # Global font settings used for all elements inside <body>.
  global:
    external: true
    family: Lato
    size:

  # Font settings for site title (.site-title).
  title:
    external: true
    family: Long Cang
    size: 2

  # Font settings for headlines (<h1> to <h6>).
  headings:
    external: true
    family: Noto Serif SC
    size: 1.6

  # Font settings for posts (.post-body).
  posts:
    external: true
    family:

  # Font settings for <code> and code blocks.
  codes:
    external: true
    family: Source Code Pro
    
```

### 附录

<!--more-->

```css
// styles.styl
// Custom styles.

//导航区背景
.site-meta {
  background: url("../images/header-bg.jpg");
  background-position: 70% 20%;
  padding: 18px 0;
}

//页面背景
body {
  background-image: url("../images/body-bg.png");
  background-repeat: repeat;
  background-attachment: fixed;
  background-position: 50% 50%; 
}

//文章页卡片
.post-block, #posts > article + article .post-block {
  margin-top: $site-top-margin;
  margin-left: 3px; 
  border-radius: $site-card-radius;
//  -webkit-box-shadow: 0 0 14px #cacbcb;
//  -moz-box-shadow: 0 0 14px #cacbcb;
//  box-shadow: 0 0 14px #cacbcb;
//  background: #fff;
  
  @media (max-width: 767px) {
    padding: 25px 0 15px !important;
    margin: 0 15px 20px;
  }
}

//二级菜单
.sub-menu {
  margin-top: $site-top-margin; 
  border-radius: $site-card-radius;
  margin-left: 3px; 
  
  @media (max-width: 767px) {
    margin: 5px 10px 0;
  }
}

#sub-menu.menu .menu-item a:hover::after {
  background-color: transparent;
}

//页面最上面黑细条
.headband {
  display: none;
}

//左侧卡片样式
.site-title {
  font-weight: 900;
}

//副标题
.site-subtitle {
  font-family: $font-family-kaiti;
  font-weight: bold;
  color: #fff;
}

.header-inner {
  margin-top: $site-top-margin; 
  border-radius: $site-card-radius;
    
  @media (max-width: 767px) {
    margin-top: 0; 
    border-top-left-radius: 0;
    border-top-right-radius: 0;
    border-bottom-right-radius: $site-card-radius;
    border-bottom-left-radius: $site-card-radius;
  }
}

.sidebar-inner {
  margin-top: 12px; 
  border-radius: $site-card-radius;
}

.sidebar {
  background: transparent;
}

//返回最上按钮
.sidebar-toggle, .back-to-top {
  background: #3a5c6b;
}

//评论区
.comments{
  margin-left: 5px;
  border-radius: $site-card-radius;
  
  @media (max-width: 767px) {
    padding: 15px;
    margin: 0 15px 20px;
  }
}
//评论区设备信息隐藏
.v .vlist .vcard .vhead .vsys { 
  display: none !important;
}

//文章标题下信息
.posts-expand .post-meta {
  margin: 3px 0 40px 0;
}
.posts-expand .post-meta time {
  border-bottom: none;
  cursor: initial;
}

//文章标题
.posts-expand .post-title {
  font-weight: 900;
}

//归档、标签、分类页文章标题
.posts-collapse .post-title a {
  font-family: $font-family-base;
}

//链接文本样式
.post-body a{
  color: #0477ab;
  border-bottom: none;

  &:hover {
    text-decoration: underline;
  }
}

//段落中代码样式
code {
  background: none;
  color: #dd4b39;
}

//引用文字字体
blockquote p, .post-body .note {
  font-family: $font-family-kaiti;
}

//文章图片边框取消
.posts-expand .post-body img {
  border: 0px;
}

//分类页样式
@media (max-width: 767px) {
  .category-all-page .category-list-item {
    margin: 5px 40px;
  }
}
@media (min-width: 767px) {
  .category-all-page .category-list-item {
    margin-left: 15px;
  }
  ul.category-list {
    text-align: center;
  }
  li.category-list-item  {
    display: inline-block;
  }
  li.category-list-item a {
    -webkit-box-shadow: $site-buttom-shadow;
    -moz-box-shadow: $site-buttom-shadow;
    box-shadow: $site-buttom-shadow;
    transition: 0.2s ease-out;
    padding: 10px 15px;
    background: #649ab6;
    color: #fff
    border-bottom: none;
    border-radius: 15px;
    line-height: 4;
    word-break: keep-all;

    &:hover {
    text-decoration: none;
    -webkit-box-shadow: $site-buttom-shadow-hover;
    -moz-box-shadow: $site-buttom-shadow-hover;
    box-shadow: $site-buttom-shadow-hover;
    }
  }
  .category-all-page .category-list {
    padding-top: 10px;
  }
}

//页码栏
.pagination, .pagination .prev, .pagination .next, .pagination .page-number {
  border:none;
}
.pagination .page-number.current {
  border-radius: 100%;
  background: #34495e;
}
.pagination {
  background: none;
  box-shadow: none;
}

//修改阅读全文按钮样式
.post-button {
  text-align: right;
  margin-top: 15px;
  
  @media (max-width: 767px) {
    margin-right: 18px !important;
  }
}
.btn {
  padding: 3px 15px
  color: #fff !important;
  background-color: #bdc3c7;
  border: 0px;
  border-radius: 15px;

  &:hover {
    color: #fff !important;
    background: #34495e;
    text-decoration: none !important;
  }
}


//文章页内标签样式
.posts-expand .post-tags a {
  -webkit-box-shadow: $site-buttom-shadow;
  -moz-box-shadow: $site-buttom-shadow;
  box-shadow: $site-buttom-shadow;
  transition: 0.2s ease-out;
  padding: 3px 5px;
  margin: 5px;
  background: #f5f5f5;
  border-bottom: none;
  border-radius: 15px;

  &:hover {
  background: $site-buttom-background-hover;
  color: #fff;
  -webkit-box-shadow: $site-buttom-shadow-hover;
  -moz-box-shadow: $site-buttom-shadow-hover;
  box-shadow: $site-buttom-shadow-hover;
  }
}

//标签云样式
.tag-cloud a {
  -webkit-box-shadow: $site-buttom-shadow;
  -moz-box-shadow: $site-buttom-shadow;
  box-shadow: $site-buttom-shadow;
  transition: 0.2s ease-out;
  padding: 2px 10px;
  margin: 8px;
  background: #f5f5f5;
  border-bottom: none;
  border-radius: 12px;

  &:hover {
  text-decoration: none;
  background: $site-buttom-background-hover;
  color: #fff !important;
  -webkit-box-shadow: $site-buttom-shadow-hover;
  -moz-box-shadow: $site-buttom-shadow-hover;
  box-shadow: $site-buttom-shadow-hover;
  }
}

.card {
  overflow: hidden;
  transition: .3s ease-in-out;
  border-radius: 8px;
  background-color: #ddd;
}
.ImageInCard img {
  padding: 0 0 0 0;
  border-radius: 8px;
}

//代码框背景颜色
.highlight-wrap {
  background: #008b8b;
}

//页脚
.footer, .footer a{
  color: #666;
}
```

```css
//variables.styl
$content-desktop-large        = 1024px
$content-desktop-largest      = 60%
$site-top-margin              = 12px
$site-card-radius             = 8px
$site-buttom-shadow           = 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24)
$site-buttom-shadow-hover     = 0 8px 16px 0 rgba(0,0,0,0.2), 0 6px 20px 0 rgba(0,0,0,0.19)
$site-buttom-background-hover = rgba(100,154,182,0.902)
$font-family-kaiti            = 'Palatino Linotype', 'Book Antiqua', Palatino, STKaiti, KaiTi, SimKai, DFKai-SB, $font-family-posts
```

附录内容来自 

[github](<https://github.com/lei2rock/blog>)

