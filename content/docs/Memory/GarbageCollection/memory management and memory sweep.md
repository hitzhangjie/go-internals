
---
title: 'memory management and memory sweep'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['garbage collector']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-memory-management-and-memory-sweep-cc71b484de05'
---

# Let's Summarize

未被引用的内存对象被垃圾回收器回收后可以用于后续分配新对象，在GC过程中，sweep阶段就是将标记为未使用的内存空间进行清理，清理后得到的空闲内存可以用来分配新的内存对象。/// go在分配对象所需内存空间时，会进行内存清零操作，将对应bits清零以避免残留垃圾值。/// go如何得知哪些内存有使用哪些没有使用呢？go在每个span内部都维护了一个allocBits，gcmarkBits，这两个字段数据结构完全一样，前者记录当前mspan内哪些内存被分配了，后者GC过程中记录哪些内存被引用了，mark termination阶段把allocBits指向gcMarkBits就完成了内存的释放，妙不！

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-memory-management-and-memory-sweep-cc71b484de05
