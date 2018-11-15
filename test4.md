|  |
| :--- |


## 文档贡献方式 {#Gitbook使用手册-文档贡献方式}

* 文档所在地址：
  [https://g.hz.netease.com/music\_qa/server/music-perf-book](https://g.hz.netease.com/music_qa/server/music-perf-book)
* 创建新分支，比如feature/todo\_demo，然后在对应的目录中添加 markdown 文档\(如果不清楚放在哪个目录，请咨询自己的组长\)。
* 文档编写完后，创建merge request，具体操作步骤和如下：
* * 合并的目标分支（target branch）选择master。
  * 在描述（Description）区域中，建议
    **@**
    **至少两名**
    ** Review **
    **人员**
    。
  * 合并负责人（Assignee）统一选择自己的组长。
  * 虽然后续会有邮件通知，建议还是通过泡泡或者其他渠道通知相关 Review 人员和合并负责人，告诉他们要及时审阅。
  * 合并负责人确定文档无误后，合并请求，至此，文档正式上线。

## 编写gitbook文档 {#Gitbook使用手册-编写gitbook文档}

1. 使用markdown语法编写，参考markdown语法：
   [https://music-rtfm.hz.netease.com/frontend-book/readme/markdown.html](https://music-rtfm.hz.netease.com/frontend-book/readme/markdown.html)

      2. 使用gitbook编辑器，自动生成md文档，下面介绍使用步骤：

      安装后运行，首页选择右下角灰字do that later

* 点击“+NewBook”，新建书本
* 点击“+Add an article”，新建文章
* **注意生成的文档最好直接拷贝到相关目录下，而不要复制内容，否则中文显示容易出现乱码**

下载地址：[https://legacy.gitbook.com/editor](https://legacy.gitbook.com/editor)

教程详细链接：[https://www.jianshu.com/p/cf4989c20bd8](https://www.jianshu.com/p/cf4989c20bd8)

**  
**

**SUMMARY.md文档**

该配置文档存放gitbook目录，如果要使上传的文档显示，必须将其加入该配置文档中



&lt;!--[SUMMARY.md](http://summary.md/)--&gt;

\# Summary

\* \[文件名\]\(文件地址\)

\* \[重要说明\]\([README.md](http://readme.md/)\)

    \* \[贡献方法\]\(readme/[contribution.md](http://contribution.md/)\)

    \* \[Markdown 语法\]\(readme/[markdown.md](http://markdown.md/)\)



**显示图片的方法**

图片统一放在[music-perf-book](https://g.hz.netease.com/music_qa/server/music-perf-book)仓库的image文件夹中，导入图片的语法如下：

!\[\]\(/image/路径/xx.png\)



**上传可下载文件的方法**

1. 先将下载文件上传至网易云：
   [https://c.163yun.com/dashboard\#/m/nos/detail/object/list/?nid=music-perf-video&lc=HZ](https://c.163yun.com/dashboard#/m/nos/detail/object/list/?nid=music-perf-video&lc=HZ)

       视频文件统一放在music-perf-video，其余文件统一放在music-perfbook

![](/assets/g-1.png)

![](/assets/g-2.png)

       2. 复制文件地址，语法如下，\[\]内显示超链接，填入文件名，\(\)内链接替代即可：

![](/assets/g-3.png)

## gitbook本地调试（可选） {#Gitbook使用手册-gitbook本地调试（可选）}

1. 安装nodejs
2. 在本地 clone 该仓库后，可以即时预览，具体步骤如下：

          定位到仓库目录后，安装依赖：

              npm install

          定位到仓库主目录，不要进入某一文件夹，启动预览服务：

              npm start

      3. 在浏览器中打开[http://localhost:4000/](file:///C:/Users/yusheng01/AppData/Local/GitBook_Editor/app-7.0.12/resources/app.asar/editor.html?config=eyJzdG9yYWdlS2V5IjoiXy9SRHBjWjJsMGJHRmljSEp2WEdkcGRHSnZiMnN0Wkc5amN3PT0tMTUzOTkxNTMxNTAwNCIsImhvc3QiOiJodHRwOi8vbG9jYWxob3N0OjQ0MjQ0IiwidXNlcm5hbWUiOiJBbm9ueW1vdXMiLCJ0b2tlbiI6IiIsImNvbW1pdHRlciI6eyJuYW1lIjoi5L2Z55ubIiwiZW1haWwiOiJ5dXNoZW5nMDFAY29ycC5uZXRlYXNlLmNvbSJ9LCJhbmFseXRpY3MiOnsiZGVidWciOjB9LCJib29rIjp7fSwiYXBpIjp7Imhvc3QiOiJodHRwczovL2FwaS5naXRib29rLmNvbS8iLCJ1c2VybmFtZSI6IkFub255bW91cyIsInRva2VuIjoiIn0sInJlcG9zaXRvcnkiOiJfL1JEcGNaMmwwYkdGaWNISnZYR2RwZEdKdmIyc3RaRzlqY3c9PSIsInJlcG9zaXRvcnlQYXRoIjoiRDpcXGdpdGxhYnByb1xcZ2l0Ym9vay1kb2NzIn0=)就能看到效果了，文档修改后，页面会自动更新，如不能自动更新，重新输入启动命令



如果之前你已经在本地安装过这个仓库的依赖，请依次运行下述命令将安装的文件删除：

rm -rf node\_modules

rm -rf ~/.gitbook

## gitbook功能介绍 {#Gitbook使用手册-gitbook功能介绍}

**1.`SUMMARY`文件支持`include`指令**

首先，`SUMMARY`文件支持`include`指令（支持嵌套），方便将一个大的 SUMMARY 文件分割成多个小的 SUMMARY 文件，这样不同的团队就可以维护自己的 SUMMARY 文件了。比如：

```
<
!--SUMMARY.md--
>
```

```
# Summary
```

```
* [重要说明](README.md)
```

```
    * [贡献方法](readme/contribution.md)
```

```
    * [Markdown 语法](readme/markdown.md)
```

```
{ % include SUMMARY_pubtec.md % }
```

###### **2.启动时可以指定**`SUMMARY`**文件** {#Gitbook使用手册-2.启动时可以指定SUMMARY文件}

将 SUMMARY 文件分割的目的，就是为了能在启动时指定 SUMMARY 文件，比如在`package.json`文件的`scripts`字段有一条命令是：

```
"pubtec": "gitbook serve . public --log=debug --debug --summary=SUMMARY_pubtec.md"
```

此时就可以运行`npm run pubtec`命令，它只会转换[`SUMMARY_pubtec.md`](http://summary_pubtec.md/)中指定的文件。

###### **3.默认转换所有markdown文件** {#Gitbook使用手册-3.默认转换所有markdown文件}

默认会转换所有 markdown 文件，但不包括根目录中的文件。也可以通过`hidden`参数指定要转换文件的[glob](file:///C:/Users/yusheng01/AppData/Local/GitBook_Editor/app-7.0.12/resources/app.asar/editor.html?config=eyJzdG9yYWdlS2V5IjoiXy9SRHBjWjJsMGJHRmljSEp2WEdkcGRHSnZiMnN0Wkc5amN3PT0tMTUzOTkxNTMxNTAwNCIsImhvc3QiOiJodHRwOi8vbG9jYWxob3N0OjQ0MjQ0IiwidXNlcm5hbWUiOiJBbm9ueW1vdXMiLCJ0b2tlbiI6IiIsImNvbW1pdHRlciI6eyJuYW1lIjoi5L2Z55ubIiwiZW1haWwiOiJ5dXNoZW5nMDFAY29ycC5uZXRlYXNlLmNvbSJ9LCJhbmFseXRpY3MiOnsiZGVidWciOjB9LCJib29rIjp7fSwiYXBpIjp7Imhvc3QiOiJodHRwczovL2FwaS5naXRib29rLmNvbS8iLCJ1c2VybmFtZSI6IkFub255bW91cyIsInRva2VuIjoiIn0sInJlcG9zaXRvcnkiOiJfL1JEcGNaMmwwYkdGaWNISnZYR2RwZEdKdmIyc3RaRzlqY3c9PSIsInJlcG9zaXRvcnlQYXRoIjoiRDpcXGdpdGxhYnByb1xcZ2l0Ym9vay1kb2NzIn0=)模式，比如：

```
"pubtec": "gitbook serve . public --log=debug --debug --summary=SUMMARY_pubtec.md --hidden=group_pubtec/**/*.md"
```

此时只会转换 group\_pubtec 目录下面的所有以`md`为后缀的文件。另外，在查找这些隐藏文件时，也可以通过`ignore`参数指定不需要查找的目录，默认值是`{public,node_modules}/**`，也就是不会查找 public 和 node\_modules 目录。

###### **4.修改单个文件时，只转换该文件** {#Gitbook使用手册-4.修改单个文件时，只转换该文件}

为了提升文章编写时的体验，在修改单个文件时，只会转换被修改的文件。但如果修改的是非文章文件（比如[`SUMMARY.md`](http://summary.md/)），此时会将所有文章重新转换一遍。

###### **5.相关实用插件** {#Gitbook使用手册-5.相关实用插件}

如果需要在gitbook中加入插件，需要配置book.json和package.json两个文件，有需求可以在插件官网中查找相关插件，在此不过多举例。

目前支持视频播放功能，使用HTML5可以实现。

