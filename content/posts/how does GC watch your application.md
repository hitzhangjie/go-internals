
---
title: 'how does GC watch your application'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['garbage collector']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-how-does-the-garbage-collector-watch-your-application-dbef99be2c35'
---

# Let's Summarize

介绍了Go垃圾回收器的设计目标，减少STW时间，一个GC周期不超过10ms，一个GC周期占用CPU不能超过25%。/// 这些目标是比较有挑战的，运行时加强对进程内存的监控和了解将有助于改善垃圾回收过程。/// go运行时监控heap使用情况GOGC，默认heap使用翻倍触发GC；如果2分钟之内没有触发GC会强制执行一次；mark assist，为了防止某些协程内存申请过快，内存申请时也会与下一次触发GC的heap大小做比较，如果已经达到了触发条件，将当前协程今天用于mark assist去标记内存，为什么这么干呢？就是为了保证垃圾回收内存速度尽量比内存分配速度快；再就是GC标记阶段不能申请超过1/4的P，比如示例中有8个P只有两个P下的mark协程为mark dedicated（不能被抢占），其他的下的mark协程都是GC idle（可以被其他协程抢占）。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-how-does-the-garbage-collector-watch-your-application-dbef99be2c35
