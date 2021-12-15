
---
title: 'context and cancellation by propagation'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['context']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-context-and-cancellation-by-propagation-7a808bbc889c'
---

# Let's Summarize

context有两个特殊的context.TODO()和context.Background()，这两个context是永远不会超时和取消的，实际上它们都是emptyCtx{}。

context tree：

通过一个context可以派生其他子context，从而形成一棵context tree。比如cancelCtx中通过字段children维护了parent context和derived contexts的派生关系。

cancellation propagation：

取消某个childCtx对parentCtx没影响，但是取消一个parentCtx，其下所有的childCtx都会被取消。也经常通过这种方式来通知某件事情的结束，如一个server中包含了多个service（http、kafka consumer、scheduled tasks…），可以通过取消serverCtx来通知各个service取消。

cancelCtx中有个mutex，通过它来实现goroutine并发操作的安全。

context leakage：

ctx.Cancel()中会将ctx.children设置为nil，还会断开parentCtx与当前ctx的连接。如果不执行Cancel()操作，那么上述有些引用关系还会被维持着，GC无法回收对应的内存，会导致内存泄漏。


# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-context-and-cancellation-by-propagation-7a808bbc889c
