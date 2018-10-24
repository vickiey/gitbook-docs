监控工具：哨兵监控平台

监控项：基础 + 内存

![](/assets/5-2.png)



监控项说明：



内存的读写性能要比硬盘快的多，因此，在设计上会充分利用内存进行数据的读取和写入，提高性能，但是内存是有限的，这就引入了物理内存和虚拟内存的概念。

## 物理内存和虚拟内存 {#id-第二节内存-物理内存和虚拟内存}

**物理内存** 是物理硬件的内存大小，称为RAM。  
在Linux下还有虚拟内存的概念，是为了满足物理内存不足的情况下，利用磁盘空间虚拟出的一块逻辑内存，用作虚拟内存的磁盘空间被成为交换空间（swap space）。  
Linux会在物理内存不足的时，使用交换分区的虚拟内存，也就是说，内核会将暂时不用的内存块信息写到交换空间，以释放物理内存。Linux的内存管理采取的是分页存取机制，为了保证物理内存能得到充分的利用，内核会在适当的时候将物理内存中不经常使用的数据块自动交换到虚拟内存中，而将经常使用的信息保留到物理内存。

**swap si/so** 交换区的换进换出  
所有的进程都需要内存，但是不是每个进程都需要一直将对象加载到内存中。基于这点，kernel通过将进程的部分或全部内存换出到磁盘上，来释放物理内存，直到需要再次使用，然后再次读到内存中。kernel采用分页和交换进行内存管理。  
si：将分页被重新读取到物理内存。也称作page-in  
so：将内存的要交换的分页写到磁盘上。也称作page-out  
关于这块更详细的解释请参考：[http://www.linuxjournal.com/article/8178?page=0,0](http://www.linuxjournal.com/article/8178?page=0,0)

## Buffer与Cache {#id-第二节内存-Buffer与Cache}

buffer 和 cache都是通过使用物理内存的一部分，其中A buffer is something that has yet to be "written" to disk. A cache is something that has been "read" from the disk and stored for later use.

但是我们平常对系统资源进行监控时看到的buffer cache，其实都是cache，其中，buffer是buffer cache，cache是page cache。



Buffer为了让不同速度的设备能够同步，建立的一个缓冲区域，写进Buffer的数据是为了从中拿出写入其他设备。  
Cache是为了提高读取速度，将经常或马上需要的数据预读到缓存中，写进Cache的数据是为了其他设备从中去读取。  
从软件这一层来说，Buffer是块设备的缓冲，Cache是文件系统的缓存。以Linux为例，  
Buffer\(Buffer Cache\)以块形式缓冲了块设备的操作，定时或手动的同步到硬盘，它是为了缓冲写操作然后一次性将很多改动写入硬盘，避免频繁写硬盘，提高写入效率。  
Cache\(Page Cache\)以页面形式缓存了文件系统的文件，给需要使用的程序读取，它是为了给读操作提供缓冲，避免频繁读硬盘，提高读取效率。  
总而言之，Buffer里面的东西是为了写到别处去，Cache里面的东西是为了给别处读。

[http://www.penglixun.com/tech/system/buffer\_and\_cache\_diff.html](http://www.penglixun.com/tech/system/buffer_and_cache_diff.html)

## 常见内存性能问题 {#id-第二节内存-常见内存性能问题}

### 系统内存不足，频繁的内存换入换出 {#id-第二节内存-系统内存不足，频繁的内存换入换出}

具体表现：使用哨兵监控，查看swap的si和so是否长期大于0，如果长期大于0，说明系统内存不足，频繁的进行换入换出。



### 系统内存不足，某个服务进程突然不见了 {#id-第二节内存-系统内存不足，某个服务进程突然不见了}

具体表现：某个进程突然不见了，使用dmesg查看被kill掉了。这是系统内存被占用过高，系统无法分配出内存，触发了oom-killer进行强制回收。

### 服务进程内存不足，出现oom错误 {#id-第二节内存-服务进程内存不足，出现oom错误}

### 服务进程内存泄露，无响应或crash {#id-第二节内存-服务进程内存泄露，无响应或crash}



