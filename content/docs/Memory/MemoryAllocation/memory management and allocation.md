
---
title: 'memory management and allocation'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['memory management']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-memory-management-and-allocation-a7396d430f44'
---

# Let's Summarize

runtime.newobject 分配内存对象，runtime.mallocgc管理堆内存。/// go中堆内存分配分为两种情况，小对象和大对象。/// 小对象，小于32KB，分配时从当前P的mcache中申请，mcache中维护了很多大小不同的mspan（又分为scan和no scan），用完内存后回收也不是真的归还给操作系统，而是标记对应mspan没有使用，后面再讨论如何回收归还给操作系统的问题。如果mcache中内存不够用了，就从全局共享的mcentral来申请对应的空余mspan，如果mcentral中也没有空余的了，则通过mheap申请内存，mheap是向操作系统申请，一次申请一个arena（64位系统下申请64MB，其他4MB），并建立pages和mspan之间的映射关系，然后将其中的mspan交给mcentral使用。绝大多数情况可以通过P.mcache解决，并且是无锁操作，分配效率会比较高。mcache中的mspan大小从8B,16B,32B…到最大32K，一共有70个不同尺寸的class，每个class都对应一个链表，里面mspan大小相同，并且分为scan和no scan两个链表，简化了GC扫描任务。/// 大内存对象分配，超过32KB，直接在mheap中分配。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-memory-management-and-allocation-a7396d430f44
