
---
title: 'scheduling in go: part ii - go scheduler'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['gpm scheduler']
author: 'William Kennedy'
publisher: 'ardan labs'
status: 'Finished'
link: 'https://www.ardanlabs.com/blog/2018/08/scheduling-in-go-part2.html'
---

# Let's Summarize

GMP调度模型，P代表了逻辑核的数量，比如Intel酷睿i7处理器是支持超线程的，一个超线程可以认为是一个虚拟核，go运行时看到的核数实际是虚拟核的数量。/// GMP调度模型和操作系统调度器类比，后者是将线程调度到不同的处理器核上执行，前者是将不同的goroutines调度到不同的线程上执行。/// 操作系统调度器是抢占式调度，go运行时调度器在以前版本（1.14以前）是协作式调度，后面也支持了抢占式调度。/// go调度器什么时候检查要不要执行goroutines切换呢？有这么几个时机，使用go func(){}创建新的协程，执行GC，执行系统调用，执行同步操作。/// 介绍了上述几种情况下的一些调度细节。/// work stealing调度器工作方式，为什么没有用work sharing，后者需要用把全局锁或者其他同步措施来同步，是有开销的，而且还比较明显，另外容易破坏goroutines的调度粘性，影响执行效率。

# Source Analysis



# References
1. https://www.ardanlabs.com/blog/2018/08/scheduling-in-go-part2.html
