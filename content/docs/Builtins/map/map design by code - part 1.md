
---
title: 'map design by code - part 1'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['map']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-map-design-by-example-part-i-3f78a064a352?source=---------45-----------------------'
---

# Let's Summarize

本文介绍了map的内部数据结构，每个桶8个kvpairs，超过了可以用溢出桶，但是溢出桶会降低map性能，所以会创建新的bucket将数据迁到新bucket里面。///   一个kvpairs存储在哪个bucket里面呢，首先根据key计算hash，然后对buckets数量取余，再放到对应桶里面，如果有空位置就放入，没有就需要走前面提到的溢出桶的逻辑。/// 根据key计算出的hash除了计算key分布在哪个桶，还有其他用途，每个桶里都有一个top hash构成的数组，是为了map访问时加快查询key所在的数组索引的，通过减少比较key的耗时来加速访问。/// 装填因子，是用来控制map装填的元素数量，即元素数量除以桶数量。装填因子过小容易浪费内存空间，过大容易引发更多的碰撞冲突导致性能下降。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-map-design-by-example-part-i-3f78a064a352?source=---------45-----------------------
