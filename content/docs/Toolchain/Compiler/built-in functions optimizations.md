
---
title: 'built-in functions optimizations'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['compiler']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-built-in-functions-optimizations-70c5abb3a680'
---

# Let's Summarize

- len、cap函数
slice对应的len、cap操作，其实是没有对应的函数体实现的。编译器会跟踪对slice的操作，从而能够直接获取到其len、cap。如果是slice作为参数，编译器会直接根据内存中sliceheader的字段len、cap字段来获取；

- unsafe.Sizeof\Alignof\Offsetof
这几个函数也没有对应的函数体实现，Sizeof返回的是描述符的大小，如sliceheader的大小而非占用的所有内存大小，所以编译器是可以直接知道大小的，包括其对齐方式、内部字段的偏移量；

# Source Analysis

系统内置函数有不少都是编译器层面实现的，builtin.go中只是添加一些godoc注释，方便开发者使用：
https://sourcegraph.com/github.com/golang/go@f24eac47710b0170fd45611ab1867e87701e0a95/-/blob/src/builtin/builtin.go#L6。

真正的实现要看编译器里面的操作，下面以cap为例进行说明。编译器会将源代码进行词法分析、语法分析、语义分析，最终生成AST，AST中每个节点Node代表了源码中的某种程序构造，比如cap(x)这里的cap函数对应的是节点类型OpSliceCap，编译器处理的时候会将其转换为OpCopy cap，cap取自`SliceMake ptr len cap`中的cap，还有len、copy等函数都是按照类似的方式来实现的。

# References
1. https://medium.com/a-journey-with-go/go-built-in-functions-optimizations-70c5abb3a680
