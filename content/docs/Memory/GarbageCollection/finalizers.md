
---
title: 'finalizers'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['garbage collector']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-finalizers-786df8e17687'
---

# Let's Summarize

runtime.SetFinalizer(p, fn)，运行时提供了这个函数来在p被GC时执行函数fn。

只有一个专门的协程来执行所有的finalizers，所以finalizers的执行是串行执行的，如果某一个finalizer的逻辑比较重，或者耗时比较久，应该启动一个独立的协程来执行该逻辑。

当一个对象obj被垃圾回收器识别为不再被引用时，其存在关联的finalizer的话，首先解除该关联关系，然后将该finalizer(obj)交给上面提的那个专门的协程去执行，至于什么时候执行完成，是没有保证的，可能程序退出时也不能保证已经执行完成了。

在obj关联你的finalizer被执行时，finalizer(obj)又重新引用了该对象obj，不可达对象又变成可达了，这个时候GC不能将其回收，但是因为已经去掉了obj和finalizer的关联，下一轮GC时该对象obj将能够被回收。

finalizer通常用来释放一些不再使用的内存资源、关闭文件等清理工作，因为其什么时候执行是不方便准确预测的，也只适合来做些类似不再使用的资源的清理工作。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-finalizers-786df8e17687
