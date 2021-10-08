
---
title: 'how does go stop the world'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['garbage collector']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-how-does-go-stop-the-world-1ffab8bc8846'
---

# Let's Summarize

STW指的是停止正在运行中的goroutines，一个GC cycle中包含了两次STW，第一次STW是为了打开write barriers，第二次STW是为了将write barriers记录下来的指针修改重新进行扫描标记，避免正被引用的对象被错误地回收掉。

这里其实只是简单介绍了下STW发生后的一些执行逻辑，比如P被抢占，P、M解除关联，M被放入空闲M队列，G被放到global queue中……

至于STW是如何实现的，以及上述过程中的具体实现，都没有详细展开，这里还是要结合源码来进一步学习一下。

# Source Analysis

see runtime/mgc.go

GOGC=off: means no gc

# References
1. https://medium.com/a-journey-with-go/go-how-does-go-stop-the-world-1ffab8bc8846
