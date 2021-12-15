
---
title: 'instrumentation in go'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['instrumentation']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-instrumentation-in-go-e845cdae0c51'
---

# Let's Summarize

介绍了go中织入代码的应用，对于go程序的测试覆盖率，它会在现有代码基础上织入一些统计每行语句执行的代码，用来实现语句测试覆盖率的统计。

对于cpu profile，其实不是通过代码织入的方式，而是定期地暂停程序并获取cpu、运行时状态信息，用来显示哪些代码段执行cpu比较花时间。

对于mem profile，这部分能力其是内置在内存分配器里面的，直接执行对应的profile逻辑就可以完成。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-instrumentation-in-go-e845cdae0c51
