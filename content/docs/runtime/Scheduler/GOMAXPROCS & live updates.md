
---
title: 'GOMAXPROCS & live updates'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['gpm scheduler']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-gomaxprocs-live-updates-407ad08624e1'
---

# Let's Summarize

介绍了GOMAXPROCS的作用，它控制了最多同时有多少个操作系统线程并发执行。除了这个环境变量，也可以在运行时通过runtime.MAXPROCS(n)来设置，也就是说允许live update（实时更新）。

该值默认等于可见的CPU核数，但是在docker容器里面希望做些资源隔离，比如希望go程序将最大并发执行操作系统线程数设置为分配给容器的CPU核数，而非母机的CPU核数，实际开发过程中有遇到因为容器中获取的不是分配的实际核数导致的调度问题。

GOMAXPROCS通常建议设置为可见CPU数或者核数。如果设置值偏大，则更多的线程被创建，操作系统调度多线程到有限的处理器核上将会引入更多的上下文切换开销，切换后协程相关的调度问题也将引入更多的开销。如果设置更小，并发度低，显而易见不利于获得更高性能。

ps：uber开源了一个库来专门获取、设置容器内CPU的数量。
        see https://github.com/uber-go/automaxprocs


# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-gomaxprocs-live-updates-407ad08624e1
