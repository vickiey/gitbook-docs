## 搭建gitbook环境

1. 安装nodejs
2. 在本地 clone 该仓库后，可以即时预览，具体步骤如下：

###### 安装依赖： {#安装依赖：}

```
npm install
```

###### 启动预览服务： {#启动预览服务：}

```
npm start
```

3.在浏览器中打开[http://localhost:4000/](http://localhost:4000/)就能看到效果了，文档修改后，页面会自动更新。

首先如果之前你已经在本地安装过这个仓库的依赖，请依次运行下述命令将安装的文件删除：

```
rm -rf node_modules

rm -rf ~/.gitbook
```

## 编写gitbook文档

1. 使用markdown语法编写，参考markdown语法
2. 使用gitbook编辑器，自动生成md文档，下面介绍使用步骤：

安装后运行，首页选择右下角灰字do that later

* 点击“+NewBook”，新建书本
* 点击“+Add an article”，新建文章
* 注意生成的文档最好直接拷贝到相关目录下，而不要复制内容，否则中文显示容易出现乱码

下载地址：[https://legacy.gitbook.com/editor](https://legacy.gitbook.com/editor)

教程详细链接：[https://www.jianshu.com/p/cf4989c20bd8](https://www.jianshu.com/p/cf4989c20bd8)



**SUMMARY.md文档**

该配置文档存放gitbook目录，如果要使上传的文档显示，必须将其加入该配置文档中

```
<!--SUMMARY.md-->
# Summary

* [文件名](文件地址)
* [重要说明](README.md)
    * [贡献方法](readme/contribution.md)
    * [Markdown 语法](readme/markdown.md)
```



## 文档贡献方法

* 创建新分支，比如`feature/todo_demo`，然后在对应的目录中添加 markdown 文档\(如果不清楚放在哪个目录，请咨询自己的组长\)。

* 添加自己为[贡献者](http://music-rtfm.hz.netease.com/frontend-book/contributors.html)
* 文档编写完后，创建`merge request`，具体操作步骤和如下：
  * 合并的目标分支（target branch）选择`master`。
  * 在描述（Description）区域中，建议**@至少两名 Review 人员**。
  * 合并负责人（Assignee）统一选择自己的组长。
  * 虽然后续会有邮件通知，建议还是通过泡泡或者其他渠道通知相关 Review 人员和合并负责人，告诉他们要及时审阅。
  * 合并负责人确定文档无误后，合并请求，至此，文档正式上线。



