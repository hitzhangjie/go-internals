
---
title: 'how does defer statement work'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['defer, panic']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-how-does-defer-statement-work-1a9492689b6e?source=---------48-----------------------'
---

# Let's Summarize

介绍了defer、panic、recover的使用及实现方式。

g里面有_defer成员，它其实是一个LIFO的栈，每次调用defer的时候会通过runtime.deferfunc（内部通过newdefer）来创建一个新的defer对象并加到g._defer栈顶；

g内部panic的时候gopanic会设置g._panic；

调用recover的时候gorecover会检查当前g的_panic；

文中还介绍了优化defer性能的CL，see https://go-review.googlesource.com/c/go/+/29656/。这个CL的核心思想是减少newdefer时导致的g被抢占、栈增长、defer函数参数内存拷贝问题。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-how-does-defer-statement-work-1a9492689b6e?source=---------48-----------------------
