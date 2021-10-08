
---
title: 'inline strategy & limitation'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['compiler']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-inlining-strategy-limitation-6b6d7fc3b1be'
---

# Let's Summarize

inline就是将一些短小简单的函数给展开，消除栈帧构建销毁的开销，多简单算简单呢？
- 函数对应的AST语法树节点数不能超过预算，预算是80个；
- 不能有复杂的程序构造，如for-loop、closure、defer、recover、select等；
- 函数前不能有noinline directive，禁止内联肯定不能内联；
- 函数前不能有uintptrescapes，因为内联会导致逃逸信息丢失；
- 其他规则；
详见：https://github.com/golang/go/wiki/CompilerOptimizations#function-inlining。

可以通过编译选项-gcflags="-m"来查看编译过程中对哪些函数进行了内联，如果使用编译选项-gcflags="-m -m"可以看到更详细的信息，如每个函数是否内联的原因：ORANGE不能处理，或者过于复杂、开销过大等等。

内联可能也会给开发者带来一些问题，较早的go版本可能会对内部包含panic的函数做内联，但是最终panic、recover时打印的stacktrace显示的panic位置不准确，对开发者很不友好。应该是go1.13及后续版本中做了优化，内部维护了一个表pc to file及lineno，stacktrace中可以还原出精确的panic位置。我测试go1.16中带panic的简单函数也是可以内联的，并且stacktrace报出的位置也很准确。

函数创建过程中涉及到栈帧创建、寄存器保存恢复、栈帧销毁等工作，和内联后直接执行指令相比，是有开销的，做了部分性能测试发现内联后比内联前有6%的性能提升。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-inlining-strategy-limitation-6b6d7fc3b1be
