
---
title: 'concurrency & scheduler affinity'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['goroutine']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-concurrency-scheduler-affinity-3b678f490488'
---

# Let's Summarize

GM模型

go1.1之前的调度模型是GM模型，有一个全局goroutine队列global queue，它的问题是：

- 访问global queue中的g，需要通过一个全局锁，锁粒度大，锁竞争严重；
- global queue中的g被恢复执行后，不一定在原来的线程上恢复，也不一定在原来的核上执行，cache命中率低；

GMP模型

go1.1开始，引入了新的调度器实现GMP模型，引入了一个局部的local queue，这个改进能够在P local queue有g时避免去锁定global queue，也就减少了锁定了整个scheduler的情况。

goroutine调度粘性

破坏了调度粘性

因为引入了P，M会优先执行P下的local queue中的g，g调度到哪个m执行就有了一定的调度粘性（affinity），但是这个调度粘性也会在某几种情况下被打破，比如：

- GMP是一个work-stealing调度器，m会在本地P local queue空时，尝试从其他地方获取一部分g来运行，比如从global queue，这里没有的话还会从netpoller中获取网络IO事件就绪的g，再没有就从其他P的local queue中获取一部分，这样相当于其他P的g没有在原来P关联的M上执行，打破了这里的调度粘性；

- 系统调用，当一个系统调用发生时（文件操作、http调用、数据库操作等），go会将当前正在运行的操作系统线程给挂起（不可中断等待状态），并且会创建一个新的操作系统线程M来处理这个P上的local queue中的g，后续执行系统调用的线程恢复后有可能会去处理其他P上的g，这也打破了这里的调度粘性；

保护调度粘性

为了减少打破这里的调度粘性，这两个限制可以尽可能去避免，以优化性能。

g、m之间的粘性，m、p之间的粘性，说白了都跟运行时依赖的缓存数据有关系，如果打破了粘性，缓存命中率下降，性能就会受影响，这个很好理解。所以go中也针对上述问题做了优化，比如一个陷入阻塞系统调用的m恢复执行后可以通过steal或者retake的方式来争取获取原来的P，也是一个办法吧，这部分了解就可以了。

对于chan send/recv引起的goroutine阻塞恢复问题，如果goroutine恢复后排在P的local queue的末尾，如果前面有其他goroutine执行，那么大概率这个goroutine会被其他的P上的M偷走，那么当前这个g就要和之前的M、P脱离关系了，一些缓存数据就无法复用了，为了减少打破这里的粘性，赋予了chan阻塞恢复的g更大的调度优先级，比如不将其放到P的local queue，而是将其放到P的runnext中，这样下次就可以立即执行了。

调度粘性的优势

p上有mcache、gFree，m上有tls，m运行g申请小于32K的内存是从p.mcache中分配，维持g、m、p之间的关系有助于复用之前p上建立的mcache，也有助于m创建新的g时复用p上之前维护的空闲g列表。

当然可能还有一些其他的原因，这里暂时先不展开了，想全了再展开。TODO

see：https://sourcegraph.com/github.com/golang/go/-/blob/src/runtime/runtime2.go#L613

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-concurrency-scheduler-affinity-3b678f490488
