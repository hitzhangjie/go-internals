
---
title: 'how does GC mark the memory'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['garbage collector']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-how-does-the-garbage-collector-mark-the-memory-72cfc12c6976'
---

# Let's Summarize

介绍了go的垃圾回收器是如何标记正在使用中的内存的，go中采用的是并发三色标记清除算法（concurrent tricolor mark and sweep），先结合字面含义解释几个事情。

基本概念：

- 并发，这里的并发指的是GC逻辑和我们的应用处理逻辑是并发进行的；
- 三色，为了区分哪些对象是可达对象（正在被引用的），哪些是不可达对象（没有被引用的），使用了黑色、白色来区分，因为这个标记过程是通过递归渐进式的扫描，过程也需要用到灰色。

mspan & mspan on scan：

GC扫描标记过程是比较耗时的，如果一个对象中没有任何指针字段，那么完全不需要扫描它，如何识别一个对象有没有指针呢？在内存分配的时候，就可以提前介入处理了。我们知道P下有mcache，mcache根据不同对象大小建立了很多不同大小的span，每个尺寸的span都有两类，一类是普通span，一类是span no scan。后者在GC扫描标记过程中是不需要去扫描的，就是说如果当前扫描到一个对象，发现其是在mspan no scan中分配的，则可以直接将其标记为黑色，结束当前这个对象的递归扫描；而如果是分配在普通mspan中的，那么就应该将其标记为灰色，并将其放入到workpool中，供mark workers取出并继续递归扫描其内部指针。

write barriers：

这里的写屏障可不是处理器提供的锁屏障哦，很多人一听名字一样以为是一个东西。处理器提供的write memory barriers，是一种内存同步原语，而这里的write barriers指的是编译器安插的一些指令，用来跟踪程序和GC并发执行期间对一些指针所做的更改，避免正在被引用的对象被错误地回收掉。

大致GC过程：

进程启动时，就会启动一些mark worker，用来执行一些标记工作。触发GC时，比如显示地执行runtime.GC()，首先会通过抢占式调度通知各个G停下来，M和P解除关系，P被抢占，M被放到空闲M列表，G放到全局queue，打开write barriers，就是一个开关，对指针进行操作时走到一个记录指针修改的分支记录一下。

每个P准备一个mark worker，mark worker开始扫描G的栈上的一些变量，称为roots对象，然后递归地进行扫描。这里用到了前面的三色标记，刚开始所有对象都是白的，然后这些roots对象全部染成灰色的。然后重复执行下述过程：
- pick 1个灰色的，将其染成黑色的；
- 然后将其内部指针指向的对象全部染为灰色的；
重复执行这个过程，最后只有两种颜色的对象：黑色的，白色的。

黑色的就是正在被引用的，白色的就是未被引用的。

GC过程中第一次STW是为了打开write barrier，然后就开始mark，这样标记完一遍之后，其实不彻底，会造成某些被引用的对象被错误地回收。解决办法就是将write barriers记录下来的被修改的指针，重新递归扫描标记一遍，就OK了。

这个扫描过程是借助了一个workpool+mark workers来实现的，实现也算比较优雅吧。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-how-does-the-garbage-collector-mark-the-memory-72cfc12c6976
