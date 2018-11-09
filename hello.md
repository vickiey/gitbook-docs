**测试思路概述**

**准备工作**

1. 打开GitLab [https://g.hz.netease.com/music\_qa/server/music-perftest](https://g.hz.netease.com/music_qa/server/music-perftest)（权限申请找朱青：[hzzhuliqing@corp.netease.com](mailto:hzzhuliqing@corp.netease.com)）  
   拉取rpc\_demo分支和rpc\_grinder\_demo分支的工程到本地

2. 本地安装grinder请参考[https://zhuanlan.zhihu.com/p/32262774](https://zhuanlan.zhihu.com/p/32262774)

3. 申请压测机qatest权限,提工单，以便检查报错信息和删除无用的日志

**一、rpc client封装**

1. idea打开rpc\_demo分支的工程
2. 修改内容详情如下：

   （1）pom.xml文件

   ![](/assets/1.png)

   （2）src---&gt;main---&gt;java---&gt;com.netease.music---&gt;service-→RelatedSongVideoRpc\(改为跟被测应用相关的其它自定义类\)

![](/assets/2.png)

（3）添加单元测试验证接口调用

![](/assets/3.png)![](/assets/4.png)![](/assets/5.png)![](/assets/6.png)

![](/assets/7.png)

1. 接口调试通过后，将工程打成jar包

在本地grinder调试接口打成一个jar包

![](/assets/8.png)

二、grinder脚本书写

1. eclipse打开grinder源码

   单接口测试

   ![](/assets/9.png)

![](/assets/10.png)

![](/assets/11.png)选择grinder调试，调试通过后，才可以在PTP平台压测。

三、PTP压测

（1）将Java工程打成jar包

在ptp压测的时候要打成多个包，因为会有冲突，并且删除一下几个冲突包

asm-5.0.3.jar

slf4j-api-1.7.21.jar

slf4j-log4j12-1.7.12.jar

![](/assets/12.png)

（2）创建轮次

打开ptp平台[http://perf.hz.netease.com/](http://perf.hz.netease.com/perf_rounds)

上传文件包括：grinder的py文件和jar包。并不上传rpc\_grinder\_demo分支中所提到的grinder.properity文件。因为ptp平台在轮次开始执行后会自动生成。

![](/assets/13.png)

![](/assets/14.png)

![](/assets/15.png)

开始执行如果报错信息为：

![](/assets/16.png)

我们rpc项目使用肯定都是JDK1.8，grinder可能日常有的使用1.7（PTP平台默认也是1.7），使用1.8的方法就是在grinder.properties添加如下信息即可

grinder.jvm=/home/qatest/PerformanceTest/jre1.8.0\_66/bin/java（PTP平台JDK1.8的路径一般都是这个，

ptp平台上传时记得把这个文件上传，就不会再使用ptp默认生成的properties文件）

![](/assets/17.png)

解决方法：

![](/assets/18.png)![](/assets/19.png)

