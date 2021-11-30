
---
title: 'how "go build" works'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['compiler, linker']
author: 'Graham Jenson'
publisher: 'medium'
status: 'Finished'
link: 'https://maori.geek.nz/how-go-build-works-750bb2ba6d8e'
---

# Let's Summarize

介绍了go编译过程中的一系列步骤，这里的介绍不是从编译器编译经过几个步骤，而是从工具角度来说，重点做了什么工作：
- 创建临时目录$WORK；
- 根据源码构建action graph，根节点是main package，对应的构建子目录是b001，其他依赖也有对应的节点，也有对应构建目录，目录编号通常是递增的；
- 构建过程中从叶子节点开始构建，然后构建父节点，持续下去直到根节点构建完成；
- 在构建过程中，每个编译单元对应的*.o或者*.a文件包括最后的可执行程序都会写入一个buildid，它包括actionid/contentid两部分构成，它用于创建索引缓存之前的编译输出，提升后续编译过程中的效率；

# Source Analysis

关于action及action graph，可以参考：https://github.com/golang/go/blob/master/src/cmd/go/internal/work/action.go

每个依赖对应的编译目录，可以参考：https://github.com/golang/go/blob/master/src/cmd/go/internal/work/action.go#L318

这些是些琐碎的细节信息，可以先忽略。

# References
1. https://maori.geek.nz/how-go-build-works-750bb2ba6d8e
