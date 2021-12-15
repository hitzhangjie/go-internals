
---
title: 'asynchronous preemption'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['goroutine']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-asynchronous-preemption-b5194227371c'
---

# Let's Summarize

这里的异步抢占，就是我们说的抢占式调度了，是通过SIGURG信号、信号处理、协程调度来共同实现的。

首先，正如前面介绍的，go程序中有一个sysmon线程，它会定期检查所有的P，检查其是否运行时间超过了10ms，如果超过了则执行抢占逻辑，preemptone(p)，其内部其实是设置P上当前g的preempt标记位为true，然后再尝试去抢占p.m，preemptM(p.m)，这个preemptM内部会给m这个线程发送一个SIGURG信号。

前面介绍gsignal时我们提过了，sighanlder这里会区分信号类型并做处理，这里的SIGURG信号就是go中选定的抢占式信号sigPreempt，然后执行抢占逻辑，这个逻辑也简单，就是保存当前g上下文，并切换到g0，g0选择下一个要调度的g并恢复其上下文执行。抢占就完成了。

关于为什么抢占信号选择SIGURG，也不是凭空选的，主要是考虑了下面几点：
It should be a signal that’s passed-through by debuggers by default.
- It shouldn’t be used internally by libc in mixed Go/C binaries […].
- It should be a signal that can happen spuriously without consequences.
- We need to deal with platforms without real-time signals […].

异步抢占，可以通过设置环境变量来关闭，GODEBUG=asyncpreemptoff=1.

# Source Analysis

SIGURG，在信号处理函数runtime/signal_unix.go:sighandler(...)函数中又看到对sigPreempt的处理。

SIGURG实现抢占式调度：
对应这个函数doSigPreempt，检查当前g是不是wantAsyncPreempt，ok的话检查是不是isAsyncSafePoint，ok的话，sigctxt.pushCall(funcPC(asyncPreempt), newpc)，这个函数调整PC并注入一个对asyncPreempt的调用。

TODO wantAsyncPreempt对应的判断参数是谁去设置的，什么时候设置的？

TODO isAsyncSafePoint，safepoint的含义？这个函数的注释以及代码中的if-else已经足够结实清楚什么是safepoint了，以及safepoint的意义了。

看下asyncPreempt的逻辑，该函数是在汇编中实现的，首先保存寄存器的值，然后调用asyncPreempt2执行其他处理。

g.preemptStop决定是挂起g还是重新调度g：
- 如果被抢占的g的g.preemptStop为true，则执行mcall(preemptPark)挂起该g，g的状态被改为preempted，后面什么时机会重新调度它吧。然后执行schedule调度其他goroutine执行；
- 如果g.preemptStop为false，则mcall(gopreempt_m)将g从running改为runnable重新调度一次。

大致的抢占式调度逻辑就是这样的。

ps: func mcall(fn func(*g))，mcall switches from the g to the g0 stack and invokes fn(g),
where g is the goroutine that made the call.

# References
1. https://medium.com/a-journey-with-go/go-asynchronous-preemption-b5194227371c
