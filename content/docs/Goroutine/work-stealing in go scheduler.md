
---
title: 'work-stealing in go scheduler'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['goroutine, gpm scheduler']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-work-stealing-in-go-scheduler-d439231be64d'
---

# Let's Summarize

GMP调度模型中，每个P的local queue长度为256，创建g时，如果p的local queue满了，就会往global queue里面放了。

为了保证各个P的负载均衡，采用work-stealing调度方式，当一个P上的M要执行一个G时，G从哪里获取呢？

- 尝试从P的local queue获取，没有则走下一步；
- 尝试从global queue获取，没有则走下一步；
- 尝试从netpoller获取，没有则走下一步；
- 尝试从其他P的local queue中获取，没有就真的没有了；

如果真的没有，就要考虑idleM、idleP的处理了。

ps：系统调用阻塞的goroutine恢复执行时，会将其加入到global queue中，因此其可能破坏了原来的GMP之间的调度粘性，可能在不同的P上由不同的M来执行。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-work-stealing-in-go-scheduler-d439231be64d
