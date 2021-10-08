
---
title: 'how goroutine stack size evolve'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['goroutine']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-how-does-the-goroutine-stack-size-evolve-447fc02085e5'
---

# Let's Summarize

介绍了goroutine的栈空间的演进，从segmented stack到continous stack，以及栈空间从4K→8K→2K的变化：

- 栈管理最初是分段栈，存在hot split问题，即如果在一个循环内存在函数调用切需要栈增长，那么会频繁发生alloc/free的情况，影响性能，为了减轻hot split，所以从4K改为8K；
- 在实现了连续栈之后，newStkSize=oldStkSize*2，栈空间够用，可以解决hot split问题，又从8K改为了2K；

本文提供了一个简单的函数调用demo（通过局部数组大小控制栈空间分配）、禁用内联、打开runtime.stackDebug来观测栈空间变化。

# Source Analysis

- copystack：拷贝栈实现逻辑
https://sourcegraph.com/github.com/golang/go/-/blob/src/runtime/stack.go#L848

- adjustpointer：创建新栈后，需要调整一下原来goroutine中的引用指针值（oldptr+delta)
https://sourcegraph.com/github.com/golang/go/-/blob/src/runtime/stack.go#L529

# References
1. https://medium.com/a-journey-with-go/go-how-does-the-goroutine-stack-size-evolve-447fc02085e5
