
---
title: 'understanding compiler directives'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['compiler']
author: 'gophers'
publisher: 'golang'
status: 'Finished'
link: 'https://golang.org/cmd/compile/'
---

# Let's Summarize

介绍了常见的编译器指令，一般遵循//go:$directive的形式
- noescape，用在函数签名前（非函数定义，实现非go语言），表示不会将指针用作参数，参数不会发生逃逸；
- uintptrescape，用在函数定义前，有些指针已经转成了uintptr做参数，但是需要做逃逸分析；
- noinline，用在函数定义前，表示禁止内联优化；
- norace，禁止做race detector做并发读写分析；
- nosplit，禁止做栈越界检查；
- linkname，指定编译器使用importpath.name作为当前localname的符号名，或者省略importpath.name只将localname导出给外部使用；

# Source Analysis



# References
1. https://golang.org/cmd/compile/
