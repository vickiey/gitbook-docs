# 分析工具 {#id-第二节java诊断工具-分析工具}

前面几个小节分别从内存、线程等方面介绍了java应用的性能分析工具，这些工具普遍都只专注于性能的一个方面，并不能满足一站式的全面的性能监控和分析的需求，而VisualVm和Jconsole就是jdk中自带的可视化分析工具。两者功能相近，详细的使用过程可以参考[visualvm](http://www.ibm.com/developerworks/cn/java/j-lo-visualvm)和[jconsole](http://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html)，下面只简单介绍下它们各自的特色。 

## VisualVm {#id-第二节java诊断工具-VisualVm}

VisualVm的visualgc插件相比于原生的内存监控功能更加直观，比较特殊的一点是visualgc插件必须通过在被监控的机器端启动jstatd进程，而不能只是配置jmx端口进行使用，其界面截图如下，能够十分清晰的展现堆内存各个区域的内存使用情况，各种gc的次数和累积停止时间。  
![](/assets/6-2-1.png)

## Jconsole {#id-第二节java诊断工具-Jconsole}

Jconsole的一大特色是其自带的MBean监控功能。MBean通过JMX这种java的原生协议可以向外界暴露出应用内部的运行时参数，如线程状态、线程池当前线程数等信息，帮助我们了解应用内的实现细节。以下显示了tomcat中的一项MBean监控数据。  
![](/assets/6-2-2.png)

## Jmap {#id-第二节java诊断工具-Jmap}

jdk工具中的jmap是分析java内存的有力工具，其功能是输出某个java进程的当前内存快照，常用的主要有摘要和dump两种模式。  
摘要模式即jmap --histo pid，该命令会显示class名称、实例数和在内存中所占字节数，并按字节数由高到低顺序输出class的列表，如下所示



| `qatest@inspur115:~$ jmap -histo:live 11846headnum #instances #bytes classname&nbsp;----------------------------------------------1: 1370793221440[B&nbsp;2: 13026315976600[C&nbsp;3: 968512535832[I&nbsp;4: 510527500160<constMethodKlass>&nbsp;5: 510526954128<methodKlass>&nbsp;6: 42245107728<constantPoolKlass>&nbsp;7: 820044688968<symbolKlass>&nbsp;8: 383454601400`[`java.net`](http://java.net/)`.SocksSocketImpl&nbsp;9: 1319504222400java.lang.String&nbsp;10: 361953251768[Ljava.util.HashMap$Entry;&nbsp;11: 42243247176<instanceKlassKlass>&nbsp;12: 36243156032<constantPoolCacheKlass>&nbsp;13: 755903023600java.lang.ref.Finalizer&nbsp;14: 897242871168java.util.HashMap$Entry&nbsp;15: 1551132481808java.lang.Object&nbsp;16: 350172009592[Ljava.lang.Object;&nbsp;17: 383291839792`[`java.net`](http://java.net/)`.SocketInputStr` |
| :--- |




其中有一些特殊的类名表示，如\[B表示byte\[\]，\[Ljava.lang.Object表示Object\[\]，详见[http://docs.oracle.com/javase/7/docs/api/java/lang/Class.html\#getName%28%29](http://docs.oracle.com/javase/7/docs/api/java/lang/Class.html#getName%28%29)  
Dump模式使用命令jmap --dump:live,format=b,file=heap.bin pid，可以将java进程的当前堆内存以hprof二进制格式dump到文件中，供后续其他工具\(如jhat/mat\)进行分析。

## Jstack {#id-第二节java诊断工具-Jstack}

JDK中的jstack是了解线程运行状态的有力工具，其典型用法及输出如下



| `qatest@app-66:~$ jstack 16186| less"Grinder thread 39"daemon prio=10tid=0x00007fc454518000nid=0x3f7crunnable [qa:0x00007fc46034e000]java.lang.Thread.State: RUNNABLEat `[`java.net`](http://java.net/)`.SocketInputStream.socketRead0(Native Method)at `[`java.net`](http://java.net/)`.SocketInputStream.read(SocketInputStream.java:146)at …(此处省略部分堆栈)at org.apache.http.impl.client.AbstractHttpClient.execute(AbstractHttpClient.java:820)at org.apache.http.impl.client.AbstractHttpClient.execute(AbstractHttpClient.java:776)"Grinder thread 39"：线程名字Prio=10：线程优先级Nid=0x3f7c: 线程idjava.lang.Thread.State: RUNNABLE 线程状态"DEADLOCK_TEST-1"daemon prio=6tid=0x000000000690f800nid=0x1820waiting formonitor entry [qa:0x000000000805f000]java.lang.Thread.State: BLOCKED (on object monitor)at c.h.ThreadDeadLockState$DeadlockThread.goMonitorDeadlock(ThreadDeadLockState.java:197)- waiting to lock <0x00000007d58f5e60> (a c.h.ThreadDeadLockState$Monitor)at c.h.ThreadDeadLockState$DeadlockThread.monitorOurLock(ThreadDeadLockState.java:182)- locked <0x00000007d58f5e48> (a c.h.ThreadDeadLockState$Monitor)at c.h.ThreadDeadLockState$DeadlockThread.run(ThreadDeadLockState.java:135)` |
| :--- |




这是BLOCKED状态线程的例子，它持有一把锁&lt;0x00000007d58f5e48&gt;，同时又在等待另一把锁&lt;0x00000007d58f5e60&gt;的释放。



## Jstat {#id-第二节java诊断工具-Jstat}

参考资料：[http://xueliang880107.iteye.com/blog/954073](http://xueliang880107.iteye.com/blog/954073)  
用以判断JVM是否存在内存问题呢？如何判断JVM垃圾回收是否正常？一般的top指令基本上满足不了这样的需求，因为它主要监控的是总体的系统资源，很难定位到java应用程序。

Jstat是JDK自带的一个轻量级小工具。全称“Java Virtual Machine statistics monitoring tool”，它位于java的bin目录下，主要利用JVM内建的指令对Java应用程序的资源和性能进行实时的命令行的监控，包括了对Heap size和垃圾回收状况的监控。可见，Jstat是轻量级的、专门针对JVM的工具，非常适用。

jstat -gcutil



| `[root@localhostbin]# jstat -gcutil 2544410005S0     S1     E      O      P     YGC     YGCT    FGC    FGCT     GCT73.540.0099.0467.5298.491660.25260.3310.58373.540.0099.0467.5298.491660.25260.3310.58373.540.0099.0467.5298.491660.25260.3310.58373.540.0099.0467.5298.491660.25260.3310.58373.540.0099.0467.5298.491660.25260.3310.583` |
| :--- |




可以看到，5次young gc之后，垃圾内存被从Eden space区\(E\)放入了Old space区\(O\)，并引起了百分比的变化，导致Survivor space使用的百分比从73.54%\(S0\)降到0%\(S1\)。有效释放了内存空间。绿框中，我们可以看到，一次full gc之后，Old space区\(O\)的内存被回收，从99.05%降到67.52%。  
图中同时打印了young gc和full gc的总次数、总耗时。而，每次young gc消耗的时间，可以用相间隔的两行YGCT相减得到。每次full gc消耗的时间，可以用相隔的两行FGCT相减得到。例如红框中表示的第一行、第二行之间发生了1次young gc，消耗的时间为0.252-0.252＝0.0秒。  
常驻内存区\(P\)的使用率，始终停留在98.49%左右，说明常驻内存没有突变，比较正常。  
如果young gc和full gc能够正常发生，而且都能有效回收内存，常驻内存区变化不明显，则说明java内存释放情况正常，垃圾回收及时，java内存泄露的几率就会大大降低。但也不能说明一定没有内存泄露。  
GCT 是YGCT 和FGCT的时间总和。

## Jprofiler {#id-第二节java诊断工具-Jprofiler}

Jprofiler可以用来分析Java程序CPU热点调用，查看哪些调用占用CPU时间比较多。也可以分析内存、线程等。  
是性能问题定位与分析的利器。但是因为其工具本身比较重，对性能指标影响比较大，因此，推荐用于问题分析，不建议性能评估时开启。  
Jprofiler安装与使用：[http://doc.hz.netease.com/pages/viewpage.action?pageId=36451057](http://doc.hz.netease.com/pages/viewpage.action?pageId=36451057)



## MAT {#id-第二节java诊断工具-MAT}

MAT即Eclipse Memory Analyzer和jdk工具jhat都能对java内存dump文件进行分析。虽然两者的数据源是一样的，但相比较而言，MAT展示的信息更丰富，功能更强大，可参考[http://www.ibm.com/developerworks/cn/opensource/os-cn-ecl-ma/index.html](http://www.ibm.com/developerworks/cn/opensource/os-cn-ecl-ma/index.html)。  
**经验**：一般情况下我们都在windows系统下导入dump二进制文件，但对于dump文件过大\(这种情况其实十分普遍，如jvm内存配置大于1G的服务器应用等，dump文件一般大于内存大小\)，而本地内存有限的情况下会导致MAT在解析时自身内存溢出终止运行，这时可以先在大内存的linux机器上用linux版本MAT下的ParseHeapDump.sh对dump文件进行分析，生成结果文件，然后把这些结果文件连同dump文件一起上传到windows机器上，在GUI界面下打开dump文件，此时MAT会检测到结果文件而跳过解析dump文件的步骤，我们也能直接查看报告了。

## 总结 {#id-第二节java诊断工具-总结}

最后对以上提到的java性能分析工具做一个小结，方便大家从最简单常用的工具入手，希望能够帮助大家找到适合自己的性能分析方法。

| 性能关注点 | 推荐工具 |
| :--- | :--- |
| 内存 | Jmap、MAT、jhat、Jprofiler |
| 垃圾回收 | gc.log、jstat |
| 线程 | Jstack、Jprofiler |
| CPU热点 | Visualvm、top、Jprofiler |



