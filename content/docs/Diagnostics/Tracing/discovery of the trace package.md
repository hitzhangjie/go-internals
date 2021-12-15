
---
title: 'discovery of the trace package'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['trace']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-discovery-of-the-trace-package-e5a821743c3c'
---

# Let's Summarize

如何激活trace？

go test -trace，通过选项-trace来激活trace功能，我们可以通过trace package提供的方法来增强默认的trace能力，下面简单总结下。

go test -trace，或者代码中通过trace.Start()/defer trace.Stop来输出trace数据到文件都可以。然后通过go tool trace trace文件，即可进行可视化展示。

trace工作过程？

这里的trace过程大致是：首先Stop the World，然后收集各个goroutines的栈帧信息，收集各个goroutines的snapshots信息，最好再Start the World。这里收集的这些信息会存储到一个bufferlist中。然后go runtime会启动一个专门的goroutine来异步地将bufferlist中的数据写入到trace数据文件中。如果bufferlist没数据的话，这个专门的协程就会被parked。

然后介绍了go tool trace 可视化信息的一些解释，比如GC各个阶段的解释、调度阶段的start、stop、syscall、unblock的解释。

用户自定义trace？

主要有两个层次：

- task层次
taskCtx, task := trace.NewTask(ctx, "task name")
结束的时候需要task.End()结束自定义trace。

- region层次
trace.NewRegion(taskCtx, "region name")
结束的时候需要region.End()标记当前阶段的结束。

这里的trace过程很直观，如果有用过opentracing的话会容易理解这里的用法。

用户自定义的trace，在输出到trace数据文件后，也是可通过go tool trace来进行可视化展示的，在选项卡“user-defined tasks”中。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-discovery-of-the-trace-package-e5a821743c3c
