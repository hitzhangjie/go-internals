
---
title: 'goroutine and preemption'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['goroutine']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-goroutine-and-preemption-d6bc2aa2f4b7'
---

# Let's Summarize

go1.14之前，在什么情况下一个goroutine可以被标记为可被抢占呢：

- 在函数序言prologue中会判断当前函数是否需要更大的栈空间，编译器会插入runtime.morestack_noctxt(SB)指令来对此做检查，这个插入的函数里面也会检查当前goroutine运行时间是否超过10ms，超过就标记为可被抢占；

ps: 这里的说法可能并不准确，我也没有用之前的版本与验证，这个10ms检查到底是在哪里判断的呢？不知道 TODO

在新版本中，比如现在的go1.16.3中，sysmon中会检查所有的P检查其运行时间是否超过了10ms时间，超过则强制抢占，preemptone(p)，内部会设置g.preempt=true。

- 但是有些循环是计算密集型的，会一直执行，这样可能很久之后才会进入下一个函数调用的prologue中检查到早就该标记为可被抢占了，但是太迟了；

go1.14之前的版本中可以通过一些协作式抢占的办法来实现goroutine抢占，比如在for循环内如果没有 函数调用的话，可以：
- 安插一些无用的函数调用，比较屁的方法；
- 显示执行runtime.Gosched()触发调度；
- 编译的时候打开实验特性，来实现for循环协作式抢占，编译器会安插指令随机得调用runtime.GoSched()，GOEXPERIMENT=preemptibleloops go build，或者go build -gcflags -d=ssa/insert_resched_checks/on；

go1.14中，引入了抢占式调度，来解决上述提及的循环不能抢占的问题：

抢占式调度，不用引入那么多的不必要的检查，引入的运行时开销更低，see https://github.com/golang/proposal/blob/master/design/24543-non-cooperative-preemption.md。

截止到我学习这篇文章时，go早已经实现了抢占式调度，我使用的是go1.16.3，我将在后面文章或者阅读源码时总结go抢占式调度的细节。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-goroutine-and-preemption-d6bc2aa2f4b7
