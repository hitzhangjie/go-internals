
---
title: 'introduction to the go compiler'
score: '⭐️⭐️⭐️'
tags: ['compiler']
author: 'gophers'
publisher: 'golang'
status: 'Finished'
link: 'https://github.com/golang/go/blob/release-branch.go1.13/src/cmd/compile/README.md'
---

# Let's Summarize

go编译器工作过程主要分为这么几个阶段：
- 解析阶段：对每个源文件进行词法分析、语法分析，并构建对应的语法树；
- 类型检查和语法树转换：进行类型检查，如名字解析、类型推断、函数定义是否结束、是否存在但定义未使用的问题。然后还会转换为抽象语法树AST，这个过程中还会根据类型信息做一系列调整优化，如函数内联、deadcode移除等；

以上两个阶段经常成为编译器的frontend，那后端backend指的是哪几个阶段呢？

- generic SSA：AST被转换成SSA（静态单赋值）形式，它是一种中间代码表示，在它基础上可以方便做优化，并转换为机器指令。这个阶段有些rewrite规则，编译器会使用一些高度优化的指令来替换掉一些特殊的内置函数，如cap、len、copy等（前面提过这些函数是没有函数体实现的），了解更多see https://en.wikipedia.org/wiki/Intrinsic_function。这个阶段还会有些节点的形式被做进一步转换，如copy、range别转换成为mov、for-loop等。然后会做有多遍与机器无关的操作和重写，如deadcode移除、nilcheck等等；
- 生成机器指令：编译器中机器相关的优化从ssa lower pass就开始了，会不断的做出一些更加接近机器低级细节的优化，直到达到机器低级特性之后，最终代码优化就开始了。比如deadcode移除，将value移到最近访问的地方，移除无用的局部变量和不必要的寄存器分配。还有会对栈帧中的变量计算好偏移量，访问更快，并计算GC  safepoint处哪些栈上的指针可以保持liveness。ssa生成阶段，go函数被转换为一系列的obj.Prog指令，然后再由汇编器生成目标文件，其中包含了反射数据、导出数据、调试信息。

# Source Analysis



# References
1. https://github.com/golang/go/blob/release-branch.go1.13/src/cmd/compile/README.md
