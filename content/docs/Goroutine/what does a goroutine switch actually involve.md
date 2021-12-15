
---
title: 'what does a goroutine switch actually involve'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['goroutine']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-what-does-a-goroutine-switch-actually-involve-394c202dddb7'
---

# Let's Summarize

介绍了go程序中goroutine切换的时机、切换的方式、切换的开销。

1 切换时机

我们类比一下加深对goroutine切换时机的理解。

- 处理器是在指令周期结束时，检查有没有中断信号到达，有则切换到对应的中断服务程序去执行；
- 操作系统是在系统调用结束返回时检查进程是否应该切换到其他进程去执行（或者执行信号处理程序）；
- 进程中切换协程，一般是在协程出现网络IO等数据未就绪、sync/*操作导致阻塞、chan操作导致阻塞、进入阻塞系统调用时导致，需要调度器调度其他协程来继续执行，高效利用CPU。还有就是在函数prologue的时候、或者收到SIGURG执行抢占调度的时候，也会涉及到协程的切换；

2 切换方式

切换的方式，对于go scheduler而言，就是需要通过特殊的协程g0来中转，比如现在运行的是g1，现在g1因为chan操作阻塞了，就需要先保存当前上下文，然后切换到g0，g0查找下一个要调度的协程g2，恢复其上下文，这个时候就执行到g2协程去了。

3 切换开销

goroutine切换的开销，以g1切换到g2为例，主要包括3个阶段：
- 保存g1当前的上下文信息，包括pc、sp，然后切换到g0，耗时10微秒左右；
- g0查找下一个待调度的协程g2，这个比较耗时，可能要100微秒左右；
- 保存g0当前的上下文信息，包括pc、sp，并恢复g2的上下文并执行g2，耗时10微秒左右；

这里的性能测量结果可能并不精准，我们了解下就可以了。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-what-does-a-goroutine-switch-actually-involve-394c202dddb7
