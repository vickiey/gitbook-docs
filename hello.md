**测试思路概述**

**准备工作**

1. 打开
   GitLab 
   [https://g.hz.netease.com/music\_qa/server/music-perftest](https://g.hz.netease.com/music_qa/server/music-perftest)（权限申请找朱丽青：[hzzhuliqing@corp.netease.com](mailto:hzzhuliqing@corp.netease.com)）
   拉取rpc\_demo分支和rpc\_grinder\_demo分支的工程到本地

2. 本地安装grinder请参考
   [https://zhuanlan.zhihu.com/p/32262774](https://zhuanlan.zhihu.com/p/32262774)
3. 申请压测机qatest权限,提工单，以便检查报错信息和删除无用的日志

**一、rpc client封装**

1. idea打开rpc\_demo分支的工程
2. 修改内容详情如下：

   （1）pom.xml文件
 
   ![](/assets/1.png)
 
   （2）src---
   &gt;
   main---
   &gt;
   java---
   &gt;
   com.netease.music---
   &gt;
   service-→RelatedSongVideoRpc\(改为跟被测应用相关的其它自定义类\)

![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2020%3A26%3A54.png?version=1&modificationDate=1541593614000&api=v2)

（3）添加单元测试验证接口调用

![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2020%3A35%3A36.png?version=1&modificationDate=1541594137000&api=v2)![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2020%3A32%3A30.png?version=1&modificationDate=1541593950000&api=v2)![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2020%3A38%3A20.png?version=1&modificationDate=1541594301000&api=v2)![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2020%3A39%3A11.png?version=1&modificationDate=1541594351000&api=v2)

![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2020%3A40%3A25.png?version=1&modificationDate=1541594425000&api=v2)

3. 接口调试通过后，将工程打成jar包

在本地grinder调试接口打成一个jar包

![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2020%3A47%3A0.png?version=1&modificationDate=1541594821000&api=v2)

二、grinder脚本书写

1. eclipse打开grinder源码
 
   单接口测试
 
   ![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2021%3A12%3A29.png?version=1&modificationDate=1541596349000&api=v2)

![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2021%3A18%3A4.png?version=1&modificationDate=1541596684000&api=v2)

![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2021%3A20%3A50.png?version=1&modificationDate=1541596850000&api=v2)选择grinder调试，调试通过后，才可以在PTP平台压测。



三、PTP压测

（1）将Java工程打成jar包

在ptp压测的时候要打成多个包，因为会有冲突，并且删除一下几个冲突包

asm-5.0.3.jar

slf4j-api-1.7.21.jar

slf4j-log4j12-1.7.12.jar

![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2020%3A50%3A47.png?version=1&modificationDate=1541595047000&api=v2)

（2）创建轮次

打开ptp平台[http://perf.hz.netease.com/](http://perf.hz.netease.com/perf_rounds)

上传文件包括：grinder的py文件和jar包。并不上传rpc\_grinder\_demo分支中所提到的grinder.properity文件。因为ptp平台在轮次开始执行后会自动生成。

![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2021%3A24%3A48.png?version=1&modificationDate=1541597088000&api=v2)

![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2021%3A28%3A37.png?version=1&modificationDate=1541597317000&api=v2)

![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2021%3A29%3A23.png?version=1&modificationDate=1541597363000&api=v2)

开始执行如果报错信息为：

![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2021%3A33%3A18.png?version=1&modificationDate=1541597598000&api=v2)

我们rpc项目使用肯定都是JDK1.8，grinder可能日常有的使用1.7（PTP平台默认也是1.7），使用1.8的方法就是在grinder.properties添加如下信息即可

grinder.jvm=/home/qatest/PerformanceTest/jre1.8.0\_66/bin/java（PTP平台JDK1.8的路径一般都是这个，

ptp平台上传时记得把这个文件上传，就不会再使用ptp默认生成的properties文件

）

![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2021%3A34%3A21.png?version=1&modificationDate=1541597661000&api=v2)

解决方法：

![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2021%3A36%3A12.png?version=1&modificationDate=1541597772000&api=v2)![](http://doc.hz.netease.com/download/attachments/163091448/image2018-11-7%2021%3A37%3A46.png?version=1&modificationDate=1541597866000&api=v2)



