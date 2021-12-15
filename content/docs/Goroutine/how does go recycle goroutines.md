
---
title: 'how does go recycle goroutines'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['goroutine']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-how-does-go-recycle-goroutines-f047a79ab352'
---

# Let's Summarize

go fn()创建一个goroutine去执行函数fn，这里的创建一个goroutine其实重要的是分配一个栈空间以及一个goroutine描述信息g，维护一下函数fn的指令地址等等信息。

我们说创建一个g，其实涉及了栈内存空间的分配动作，涉及到对象分配的，我们都知道通过对象池可以优化内存分配问题，goroutine这里也不例外。

当一个goroutine执行完成函数fn时，并不意味着这个goroutine就被彻底销毁了，它会被保存到P的gFree字段中，后续如果需要创建goroutine时就可以复用，当然了gFree中如果g比较多，也会被迁移到调度器的g空闲链表中，方便其他P复用。

因为g是有栈空间的，而且栈空间会增大，当g执行fn完成时，可能栈空间不小了，比如超过了2KB，这种时候再保留这个栈空间池化就太浪费内存了，所以这种栈空间大的就会释放其栈空间，所以在调度器的g空闲链表可以分为两类：
- 带栈空间的g空闲链表；
- 栈空间被销毁的g空闲链表；

这里的g被重复利用，只是为了提高g创建效率，和我们通过一些workerpool来限制goroutines数量的初衷是不重复的，workerpool一般并不是为了提高g创建效率，而是为了限制g数量，避免吃爆内存。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-how-does-go-recycle-goroutines-f047a79ab352
