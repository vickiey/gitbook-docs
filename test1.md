校园红人压测需求---[校园红人计划](http://doc.hz.netease.com/pages/viewpage.action?pageId=157327463)

需求详情：

![](/assets/1-1.png)

1.     确定需求

（1）     确定要压测的目的

* redis代替mongo优化效果
* 业务接口性能拐点

（2）     确定要压测的接口

此次压测接口是获取校园红人接口（api/nearby/campusstar/get）和redis搜索能力测试接口（/api/redis/geo/test）

2.     明确方案

根据压测需求，设计压测方案。

（1）     压测范围与目标

l  redis的搜索处理能力

l  压力测试，检测方案在峰值流量时的表现，以及所能承受的最大负载。

| **压测场景** | **接口信息** | 方法 | 参数 |
| :--- | :--- | :--- | :--- |
| redis搜索 | /api/redis/geo/test | get | 经度：lon、纬度：lat、搜索范围：radius |
| 单机处理能力 | api/nearby/campusstar/get | post | 经度：lon、纬度：lat |



（2）     熟悉被测系统，整理调用链路图，如下：

![](/assets/1-2.png)

（3）压测风险分析

线下压测使用新申请的redis，压测完成后，清理数据。ddb保存红人相关数据在测试库中，可以不删除。

（4）性能测试方案编写



3.压测准备

（1）工具—平台

NEI（[https://nei.netease.com](https://nei.netease.com/)）：查看接口信息

overmind（[http://overmind.hz.netease.com/env/env\_list](http://overmind.hz.netease.com/env/env_list)）：环境搭建

PTP（[http://perf.hz.netease.com](http://perf.hz.netease.com/)）：执行压测

（2）数据准备

在给定经纬度范围内，随机生成10W用户的经纬度信息，以CSV文件形式保存

（3）机器准备

中间件申请：redis

压测机：

[hzbdg-qa-app-001.server.163.org](http://hzbdg-qa-app-001.server.163.org/)

[hzbdg-qa-app-002server.163.org](http://hzbdg-qa-app-001.server.163.org/)

[hzbdg-qa-app-003.server.163.org](http://hzbdg-qa-app-001.server.163.org/)

[hzbdg-qa-app-004.server.163.org](http://hzbdg-qa-app-001.server.163.org/)

[hzbdg-qa-app-005.server.163.org](http://hzbdg-qa-app-001.server.163.org/)

（4）环境搭建

在overmind上面搭建环境。步骤如下：

a.打开overmind平台：[http://overmind.hz.netease.com/env/env\_list](http://overmind.hz.netease.com/env/env_list)

![](/assets/1-3.png)

![](/assets/1-4.png)





4.开始压测

打开PTP平台：[http://perf.hz.netease.com/](http://perf.hz.netease.com/)

操作步骤如下：

（1）新建

![](/assets/1-5.png)![](/assets/1-6.png)![](/assets/1-8.png)![](/assets/1-7.png)

![](/assets/1-9.png)

![](/assets/1-10.png)![](/assets/1-11.png)



提交即可

（3）查看结果

![](/assets/1-12.png)

（4）  增加并发量，直至性能拐点

* 重建轮次

![](/assets/1-13.png)

* 性能指标分析图
 
  ![](/assets/1-14.png)

5.分析压测结果并优化

