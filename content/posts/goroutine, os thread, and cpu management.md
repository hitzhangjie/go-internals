
---
title: 'goroutine, os thread, and cpu management'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['goroutine']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-goroutine-os-thread-and-cpu-management-2f5a5eaf518a'
---

# Let's Summarize

首先介绍了GMP调度模型中G、M、P的概念以及意义，介绍了大致的执行过程，如M需要获得一个P来执行G。

针对以下两种情形进行了简单总结：

系统调用：介绍了如果M执行阻塞型系统调用后的情况，P被释放交给其他M使用，M恢复后尝试获取原来的P（有线程之前的数据cache性能更好），被占用了就获取空闲的P，没有则将当前goroutine放到全局等待队列中，并将当前M park掉放到空闲m队列中，等待调度器调度其他goroutine时复用。

网络调用：网络库基于IO多路复用+非阻塞进行了实现，线程虽然不会因为网络IO进行阻塞了，但是数据没准备好goroutine还是不能执行的。这个工作不能交给内核来做了，需要runtime+netpoller来配合完成。runtime执行schedule()函数查找一个runnable的goroutine时，除了从global queue、p的local queue、其他p的local queue中进行查找外，也会询问netpoller，当前有没有IO事件就绪的goroutine，有就给我一个列表我好执行。当然当前M知会执行一个goroutine，netpoller返回的就绪列表中的其他goroutine会被加入到global queue中。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-goroutine-os-thread-and-cpu-management-2f5a5eaf518a
