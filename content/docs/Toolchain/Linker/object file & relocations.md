
---
title: 'object file & relocations'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['linker']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-object-file-relocations-804438ec379b'
---

# Let's Summarize

介绍了go编译过程中符号链接的大致过程：
- 编译过程中会按照编译单元进行构建，生成一系列的*.o文件，在将它们合并成一个可执行程序时，里面涉及到一些符号的可重定位操作；
- 比如main.o中有依赖fmt.o，其中有个函数调用fmt.Println，因为这个函数不是在main.o中定义的，编译器是不知道到底这个符号在哪里的，就需要链接器来处理这个事情，并将最终函数调用fmt.Println处的位置改成一个相对地址，以使得函数调用得以完成；

通过go tool compile -S -l main.go可以看到生成了一个main.o文件，通过go tool nm main.o可以看到其中的一些符号信息，有些符号前面有个大写的U，这种表示符号未在当前编译单元中定义，需要链接器后面重定位一下。

go tool link就是完成链接过程了，最终生成可执行文件，我们通过objdump -dS main就可以查看对应的汇编信息，并且能看到fmt.Println函数调用处已经替换成了CALL+相对地址。相对地址的计算也简单：call指令地址+call指令本身字节数-fmt.Println地址。

# Source Analysis

编译器生成的对象文件格式，是go团队根据plan9的习惯定义的吧，和我们操作系统平台提供的*.o文件还不一样，详细的可以参考这个：https://golang.org/pkg/cmd/internal/objabi/

# References
1. https://medium.com/a-journey-with-go/go-object-file-relocations-804438ec379b
