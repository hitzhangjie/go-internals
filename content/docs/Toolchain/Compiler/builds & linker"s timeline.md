
---
title: 'builds & linker"s timeline'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['compiler, linker']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-builds-linkers-timeline-b312084ddf7d'
---

# Let's Summarize

go build涉及到的工作步骤包括：
- 创建临时工作目录；
- 编译各个package及其依赖；
- 链接器连接成可执行程序；
- 将可执行程序移动到当前目录，并删除临时工作目录；

`go build -x`会显示整个编译过程中执行的命令，在编译链接过程中，由于编译可能会涉及到应用编译缓存，链接器链接部分的耗时则会变得很突出，如何优化链接器提升其效率就变得很重要。

linker的目的是为了构建一个可执行程序，其步骤包括：
- 加载已经编译好的各个package及其依赖，并收集其中的符号信息；
- 移除deadcode，如所有未使用的函数，这个过程无法在编译阶段完成，因为编译阶段是各个package独立编译的，不知道它们之间的依赖关系，只有链接器知道；
- DWARF调试信息生成，并将其压缩存储到二进制程序中；
- 组织好pc-value表，function表，符号表，方便内部使用；
- 重定位，编译阶段因为是独立编译各package，引用的其他package中的函数的具体位置是不知道的，只有在最后这个阶段链接器能知道，要靠链接器把函数调用出替换为准确的函数地址。
最后一个可执行程序就生成了。

linker也分为internal linker和external linker，涉及到cgo调用、生成共享库等的时候会使用external linker，其他情况会默认使用internal linker。

可以给linker传递选项来减轻链接阶段的耗时，如`go build -ldflags="-w"` or go tool link -w 来禁用调试信息生成，internal linker还支持对生成的调试信息进行压缩，如`go build -ldflags="dwarfcompress=true"`。

go之前提供的linker实现不能说完美吧，所以也有构建更好的linker的想法，详情可见：http://golang.org/s/better-linker。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-builds-linkers-timeline-b312084ddf7d
