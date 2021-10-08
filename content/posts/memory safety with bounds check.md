
---
title: 'memory safety with bounds check'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['compiler']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-memory-safety-with-bounds-check-1397bef748b5'
---

# Let's Summarize

为了阻止访问越界类问题，go中引入了bounds check，我们可以通过选项-gcflags="-B"关闭bounds check，来查看下访问越界会发生什么？要么访问到一些垃圾值，要么触发段错误崩溃。

简单地说就是，编译器会在涉及slice位置访问的时候（如nums[100])的时候安插一些指令，用来比较索引位置100和cap(nums)的关系，如果索引位置不合法，则直接跳到panicIndex函数panic。

当然编译器更聪明一点，在ssa多轮passes中均有优化处理，如bce、prove等，会做一些优化，避免无脑地安插边界检查指令，感兴趣可以继续深究下。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-memory-safety-with-bounds-check-1397bef748b5
