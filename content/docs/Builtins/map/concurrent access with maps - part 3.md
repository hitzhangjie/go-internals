
---
title: 'concurrent access with maps - part 3'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['map, race detector']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-concurrency-access-with-maps-part-iii-8c0a0e4eb27e'
---

# Let's Summarize

1 map

map中的并发读写问题，go提供了如下方式进行检查：

- data race detection：通过选项-race来检测是否存在data race，关于data race检测的问题，kavya joshi的分享里有介绍；

- 并发写操作检测：map对应的数据结构hmap中有个字段flags来记录当前的map操作，比如当前执行m[1]=1，是一个kv的赋值，对应的函数是mapassign_fast64，如果执行的是delete(m, 1)，对应的函数是mapdelete_fast64，这里的map修改操作对应的函数内部会将hmap.flags^=hashWriting，如果已经有一个写操作在执行，后面又有一个写操作执行，后面的写操作就有很大概率检测到flags的hashWriting位被设置了，此时就会抛出错误“concurrent map writes”错误；

关于map为什么不直接提供并发安全的版本，原因也简单。并发安全的版本是有同步开销的，但是很多时候并不需要并发安全的版本，如果默认实现是并发安全的，性能上就要大打折扣了。不考虑并发安全问题的话，map比sync.Map要快7~10倍。

2 sync.Map

sync.Map是并发安全的实现，它对某些场景下的并发读写做了性能方面的优化：
goblogs: "The Map type is optimized for two common use cases: (1) when the entry for a given key is only ever written once but read many times, as in caches that only grow, (2) when multiple goroutines read, write and overwrite entries for disjoint sets of keys. In these two cases, use of a Map may significantly reduce lock contention compared to a Go map paired with a separate Mutex or RWMutex."

意思就是说，sync.Map对于像缓存（caches）这种写一次（或次数很少）但是读取次数多的场景就很适用，或者存在多个goroutines并发读写，但是读写的keys集合是不相交的。

3 shardedmap

sync.Map对于需要频繁执行删除的场景、更广泛的写场景，没有对其进行足够的优化，这两个场景可以参考shardedmap实现。

see: 
- https://github.com/orcaman/concurrent-map/blob/master/concurrent_map.go
- https://golangexample.com/a-simple-and-efficient-thread-safe-sharded-hashmap-for-go/

4 benchmark

对map、sync.Map、concurrent_map（shardedmap）进行了benchmark，结果如下：

BenchmarkDeleteEmptyMap-8 20000000 86.9 ns/op
BenchmarkDeleteEmptySyncMap-8 300000000 5.16 ns/op
BenchmarkDeleteEmptyCMap-8 50000000 34.8 ns/op

BenchmarkDeleteMap-8 10000000 131 ns/op
BenchmarkDeleteSyncMap-8 10000000 135 ns/op
BenchmarkDeleteCMap-8 30000000 37.0 ns/op

BenchmarkLoadEmptyMap-8 20000000 87.9 ns/op
BenchmarkLoadEmptySyncMap-8 300000000 5.03 ns/op
BenchmarkLoadEmptyCMap-8 100000000 17.1 ns/op

BenchmarkLoadMap-8 20000000 111 ns/op
BenchmarkLoadSyncMap-8 100000000 12.8 ns/op
BenchmarkLoadCMap-8 100000000 22.5 ns/op

BenchmarkSetMap-8 10000000 187 ns/op
BenchmarkSetSyncMap-8 5000000 396 ns/op
BenchmarkSetCMap-8 20000000 84.9 ns/op

benchmark结果表明：
- map+rwmutex这种方式，锁粒度比加大，增删该查操作耗时相对来说都是比较明显的；
- sync.Map这种方式，写少读多的情况是非常合适的，效率比较明显，优于map、concurrent_map；
- concurrent_map，考虑了并发写比较频繁的情况，特别是删除，多shard执行删除操作时效率非常明显；

举个应用选型的例子：连接池明明显属于读多写少的场景，建议用sync.Map代替（key为ip:port，value为connection），后面transport如果要实现双工模式的时候，需要维护req.seqno\req的映射关系，增删频繁，可以考虑用concurrent_map（key为req.seqno，value为req）。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-concurrency-access-with-maps-part-iii-8c0a0e4eb27e
