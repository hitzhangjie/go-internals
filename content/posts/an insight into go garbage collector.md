
---
title: 'an insight into go garbage collector'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['garbage collector']
author: 'Fabio Falzoi'
publisher: ''
status: 'Finished'
link: 'https://golangpiter.com/system/attachments/files/000/001/718/original/GP_2019_-_An_Insight_Into_Go_Garbage_Collection.pdf?1572419303'
---

# Let's Summarize

goroutine栈内存是从mheap申请而来，栈空间小于32K的时候也是从P.mcache中分配的，减小锁竞争，当栈空间大于32K时就从mheap中分配了。/// stack split指的是stack growth和stack shrink这种情况。/// stack销毁开销更小，调整下栈指针寄存器即可。heap对象销毁则要依赖垃圾回收。/// 并发三色标记清除算法，黑色表示可达并且已经分析完了其内部指针的对象，灰色表示可达但是还没有分析完其内部指针，白色表示不可达对象。为了维持三色不变性需要通过write barrier来记录mutator对指针做的修改，新版本中已经是用的混合写屏障了，综合了dijkstra write barrier和yuasa write barrier，并且做了优化实现了bufferred write barrier，允许每个P维护一个buffer必要时flush以提GC性能。/// go GC追求更低的停顿时间，希望GC给goroutine执行引入的延迟更低！

# Source Analysis



# References
1. https://golangpiter.com/system/attachments/files/000/001/718/original/GP_2019_-_An_Insight_Into_Go_Garbage_Collection.pdf?1572419303
