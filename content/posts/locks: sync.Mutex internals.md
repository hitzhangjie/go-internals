
---
title: 'locks: sync.Mutex internals'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['locks']
author: 'zhangjie'
publisher: 'tencent'
status: 'Finished'
link: 'https://www.hitzhangjie.pro/blog/2021-04-17-locks%E5%AE%9E%E7%8E%B0%E9%82%A3%E4%BA%9B%E4%B8%8D%E4%B8%BA%E4%BA%BA%E7%9F%A5%E7%9A%84%E6%95%85%E4%BA%8B/'
---

# Let's Summarize

介绍了内存屏障的类型及由来，介绍了CAS、spinlock、futex的工作原理，介绍了sync.Mutex的设计实现及针对协程调度方面的一些优化措施。算是讲清楚了锁的来龙去脉了吧。

ps：在线程切换的时候，内核会显示插入全内存屏障，来保证线程切换前的写操作对线程切换后的操作可见。

# Source Analysis



# References
1. https://www.hitzhangjie.pro/blog/2021-04-17-locks%E5%AE%9E%E7%8E%B0%E9%82%A3%E4%BA%9B%E4%B8%8D%E4%B8%BA%E4%BA%BA%E7%9F%A5%E7%9A%84%E6%95%85%E4%BA%8B/
