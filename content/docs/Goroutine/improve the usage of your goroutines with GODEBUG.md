
---
title: 'improve the usage of your goroutines with GODEBUG'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['goroutine']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-improve-the-usage-of-your-goroutines-with-godebug-4d1f33970c33'
---

# Let's Summarize

这篇文章介绍了通过goroutine调度latency来分析程序中增加更多的goroutines数量是否有必要，这个示例中的goroutine大部分会因为请求服务端数据而阻塞，这个阻塞时间比较长，严重影响计算，这里增加很多的goroutines并不能充分地利用起计算资源，主要是这里大部分都会阻塞，并不是会切来切去地，无助于提高并发效率。

1 GODEBUG=schedtrace=1 go test
2 runtime/trace, trace.Start(), defer trace.Stop()

输出信息的解释：
see https://github.com/golang/go/wiki/Performance#scheduler-trace：

下面是个例子：

```bash
SCHED 1004ms: gomaxprocs=4 idleprocs=0 threads=11 idlethreads=4 runqueue=8 [0 1 0 3]
SCHED 2005ms: gomaxprocs=4 idleprocs=0 threads=11 idlethreads=5 runqueue=6 [1 5 4 0]
SCHED 3008ms: gomaxprocs=4 idleprocs=0 threads=11 idlethreads=4 runqueue=10 [2 2 2 1]
```

- The first number ("1004ms") is time since program start. Gomaxprocs is the current value of GOMAXPROCS. 
- Idleprocs is the number of idling processors (the rest are executing Go code). 
- Threads is the total number of worker threads created by the scheduler (threads can be in 3 states: execute Go code (gomaxprocs-idleprocs), execute syscalls/cgocalls or idle). 
- Idlethreads is the number of idling worker threads. 
- Runqueue is the length of global queue with runnable goroutines. The numbers in square brackets ("[0 1 0 3]") are lengths of per-processor queues with runnable goroutines. Sum of lengths of global and local queues represents the total number of goroutines available for execution.

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-improve-the-usage-of-your-goroutines-with-godebug-4d1f33970c33
