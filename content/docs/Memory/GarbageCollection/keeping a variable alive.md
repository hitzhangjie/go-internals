
---
title: 'keeping a variable alive'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['garbage collector']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-keeping-a-variable-alive-c28e3633673a'
---

# Let's Summarize

介绍了finalizer的使用，介绍了如何通过runtime.KeepAlive(p）来避免p指向的对象被GC掉，其实该函数的实现没有什么特殊的，就是引用了一下p指向的对象而已，在这个函数调用之前的位置是不可能被GC掉的。那我们自己引用以下行不行比如用q := p, _ = q，可能不行，编译器优化有很多遍，比如deadcode移除、函数内联等，这样下来我们自己的写法，可能会因为编译器的一些优化给优化了，导致无效，建议还是使用go提供的方式来来阻止被优化掉。关于这个函数的具体实现，see：https://utcc.utoronto.ca/~cks/space/blog/programming/GoRuntimeKeepAliveNotes。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-keeping-a-variable-alive-c28e3633673a
