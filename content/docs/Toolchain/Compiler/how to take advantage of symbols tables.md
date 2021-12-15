
---
title: 'how to take advantage of symbols tables'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['compiler']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-how-to-take-advantage-of-the-symbols-table-360dd52269e5'
---

# Let's Summarize

go在编译过程中会检查使用的标识符是否已经定义过，编译器通过符号表来记录已经定义的标识符。程序构建完成之后，其实就不再需要符号表了，为了程序尺寸可以考虑从binary中剥离符号表：
- 可以通过其他二进制工具来从binary中剔除符号表；
- 也可以考虑在编译时指定选项-ldflags="-s"在编译链接完成后剔除符号表；

我们可以通过nm或者go tool nm来查看binary中的符号表信息，也可以通过-ldflags="-X $pkg.$var=$value"的方式来设置一些包级别的变量值。

根据程序规模不同，符号表大小可能会导致binary尺寸增加，为了加速程序加载启动可以考虑删掉符号表。如果考虑到调试方便，则可以保留符号表。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-how-to-take-advantage-of-the-symbols-table-360dd52269e5
