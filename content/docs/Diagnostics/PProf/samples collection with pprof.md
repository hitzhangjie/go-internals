
---
title: 'samples collection with pprof'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['pprof']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-samples-collection-with-pprof-2a63c3e8a142'
---

# Let's Summarize

介绍了pprof中CPU profile的工作原理，大致过程是，按照一定的采样频率来生成SIGPROF信号，由gsignal协程接收并执行处理，处理逻辑就是去收集必要的数据并写入一个buffer，最好生成报表。

TODO 大致过程是这样的，细节要看下代码。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-samples-collection-with-pprof-2a63c3e8a142
