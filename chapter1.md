# GitBook调研

## GitBook简介

GitBook是一个命令行工具（和Node.js库），用GitHub / Git和Markdown（或AsciiDoc）来编排精美的书籍。GitBook既可以在您的计算机上构建本地书籍，也可以在legacy.gitbook.com上托管它们。

* 基础功能：新建、编辑、配置书籍（包括设置书籍主题、集成GitHub、绑定域名等）
* 高级功能：

  1. 个性化配置：配置book.json，对书本信息进行设置

  2. 插件：gitbook提供了很多实用的插件，对书本格式进行设置

GitBook使用手册：[http://www.chengweiyang.cn/gitbook/customize/book.json.html](http://www.chengweiyang.cn/gitbook/customize/book.json.html)

## GitBook安装

### 搭建GitBook环境

* 安装nodejs
* cnpm安装gitbook
* 解压书籍文件，并cd到书籍文件目录
* gitbook serve
* 浏览器访问localhost:4000

详细链接：[https://blog.csdn.net/zerorm/article/details/79229053](https://blog.csdn.net/zerorm/article/details/79229053)

### 基本使用方式

#### 使用命令创建基本GitBook

#### 使用网页在线编辑器创建、编辑GitBook

#### 安装GitBook可视化编写工具（推荐）

* 安装后运行，首页选择右下角灰字do that later（因为翻墙的原因，这里无法通过login绑定GitHub，后面介绍如何绑定）
* 点击“+NewBook”，新建书本
* 点击“+Add an article”，新建文章

下载地址：[https://legacy.gitbook.com/editor](https://legacy.gitbook.com/editor)

教程详细链接：[https://www.jianshu.com/p/cf4989c20bd8](https://www.jianshu.com/p/cf4989c20bd8)

### GitBook绑定GitHub

* 创建文章后，点击页面右上角publish，弹出框需要填入Git仓库的https地址

详细链接：[https://segmentfault.com/a/1190000011440899](https://segmentfault.com/a/1190000011440899)

### 未完待续

* 自定义域名





