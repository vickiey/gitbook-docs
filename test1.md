## 一.该工程未接入性能环境

## 1.添加性能环境配置

**（1）接入配置中心、故障注入（接口人：包杨）**

* 接入最新版配置中心、接入故障注入，参见wiki链接：[应用接入步骤及注意事项](http://doc.hz.netease.com/pages/viewpage.action?pageId=99649572#id-%E6%95%85%E9%9A%9C%E6%BC%94%E7%BB%83%E5%B9%B3%E5%8F%B0%E6%95%85%E9%9A%9C%E7%B1%BB%E5%9E%8B%E5%AE%9A%E4%B9%89%E4%B8%8E%E6%8E%A5%E5%8F%A3%E6%8F%8F%E8%BF%B0-%E5%9B%9B%E3%80%81%E5%BA%94%E7%94%A8%E6%8E%A5%E5%85%A5%E6%AD%A5%E9%AA%A4%E5%8F%8A%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)
* 接入后在配置中心加上配置项

**（2）环境属性配置迁入配置中心（接口人：汪建伟）**

 配置中心：[https://music-config.hz.netease.com](https://music-config.hz.netease.com/)

* 中间件配置迁移到配置中心，规范参见：[http://doc.hz.netease.com/pages/viewpage.action?pageId=127406210](http://doc.hz.netease.com/pages/viewpage.action?pageId=127406210)

* dao改造支持配置中心，参见：[http://doc.hz.netease.com/pages/viewpage.action?pageId=130241968](http://doc.hz.netease.com/pages/viewpage.action?pageId=130241968)

* 性能环境配置，参见：[http://doc.hz.netease.com/pages/viewpage.action?pageId=130237013](http://doc.hz.netease.com/pages/viewpage.action?pageId=130237013)

**（3）升级RPC 版本（接口人：薛广顺）**

* Rpc 升级到4.2.5以上版本，以便支持rpc管控平台，方便定位

* 升级文档，参见：[http://doc.hz.netease.com/pages/viewpage.action?pageId=111947223](http://doc.hz.netease.com/pages/viewpage.action?pageId=111947223)

* 如果接入正常，[http://music-rpcadmin.igame.163.com/admin/apps](http://music-rpcadmin.igame.163.com/admin/apps)，可以搜索到相关应用rpc信息

**（4）接入日志平台（接口人：晁涛）**

 日志平台：[http://music-pylon.hz.netease.com/cmslog/](http://music-pylon.hz.netease.com/cmslog/)

* 接入文档：[http://doc.hz.netease.com/pages/viewpage.action?pageId=110538247](http://doc.hz.netease.com/pages/viewpage.action?pageId=110538247)
* 产品使用说明：[http://doc.hz.netease.com/pages/viewpage.action?pageId=121158047](http://doc.hz.netease.com/pages/viewpage.action?pageId=121158047)
* 如果接入正常，验证 logs/mlog/${[app.name](http://app.name/)}.log 日志是否正常输出

**（5）接入pylon（接口人：郭元华）**

* 接入文档：[http://doc.hz.netease.com/pages/viewpage.action?pageId=94089227](http://doc.hz.netease.com/pages/viewpage.action?pageId=94089227)

* 如果接入正常，[http://music-tracelog.hz.netease.com/trace/app](http://music-tracelog.hz.netease.com/trace/app)可搜索到相关应用；测试环境看看本地/home/appops/logs/trace/trace.log是否存在

**（6）应用监控接入哨兵（接口人：马宏展）**

 哨兵地址：[https://nss.netease.com](https://nss.netease.com/)

* 自动接入哨兵监控的可参考下面的地址（如果发现性能环境没有自动接入哨兵监控可参考修改）：
  [Java应用监控和配置中心接入流程\#premain2.1.0jar%E5%8C%85%E5%8D%87%E7%BA%A7](http://doc.hz.netease.com/pages/viewpage.action?pageId=108936020#Java%E5%BA%94%E7%94%A8%E7%9B%91%E6%8E%A7%E5%92%8C%E9%85%8D%E7%BD%AE%E4%B8%AD%E5%BF%83%E6%8E%A5%E5%85%A5%E6%B5%81%E7%A8%8B-premain2.1.0jar%E5%8C%85%E5%8D%87%E7%BA%A7)

* 如果接入正常，登陆哨兵系统，进入应用，查看JVM、JavaMethod、music\_rep\_rpc 这个三个监控项数据正常收集并展示正确。

**（7）应用接入nginx（接口人：念杰）**

1、Nginx 机器所在地址：[music24.photo.163.org](http://music24.photo.163.org/)，需要申请appops权限，sudo -iu appops

2、性能测试环境域名：overmind新建环境时的域名，配置文件路径 /etc/nginx/sites-enabled/qa-\*.perf-mmuisc，这个域名的配置，统一在这里维护

![](/assets/2-4-1.png)

3、现在性能测试环境有些配置是之前从功能（测试）环境拷贝过来，有的配置可能还没改，有需要接入nginx 的，请注意检查。

4. 测试配置是否正确： sudo /etc/init.d/nginx configtest

5. 如配置无问题，执行重启：sudo /etc/init.d/nginx reload

6. 如配置有问题，查看具体错误位置： sudo /usr/sbin/nginx -t

**（8）代码整理**

**无论性能环境是不是部署了这个应用，都要改成性能环境约定的key（ 添加perf 标识）**

老模板将性能环境配置写入perf文件，如图\(1\)；新模板将性能环境配置写入perf文件，如图（2）。

![](/assets/2-4-2-1.png)

![](/assets/2-4-2.png)

 图（1）图（2）

2.overmind部署调试

注：性能环境分为性能测试环境和性能回归环境，开发如有压测需求，只需在性能测试环境创建环境即可。

![](/assets/2-4-3.png)

**（1）新建性能测试环境**

![](/assets/2-4-4.png)

![](/assets/2-4-5.png)

**（2）添加/删除应用**

![](/assets/2-4-6.png)

**（3）应用接入batch**

如果部署的应用接入了batch，需要在搭建环境的时候，部署batch应用。

![](/assets/2-4-7.png)

二.该工程已接入性能环境

直接在overmind上部署即可

