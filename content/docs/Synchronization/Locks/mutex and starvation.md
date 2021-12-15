
---
title: 'mutex and starvation'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['locks']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-mutex-and-starvation-3f4f4e75ad50'
---

# Let's Summarize

介绍了新版本的go如何优化goroutine获取锁失败的饿死问题。

其实这个问题在我的博客中有十分详细的描述，重点看sync.Mutex协程调度优化部分：https://www.hitzhangjie.pro/blog/2021-04-17-locks%E5%AE%9E%E7%8E%B0%E9%82%A3%E4%BA%9B%E4%B8%8D%E4%B8%BA%E4%BA%BA%E7%9F%A5%E7%9A%84%E6%95%85%E4%BA%8B/%E3%80%82

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-mutex-and-starvation-3f4f4e75ad50
