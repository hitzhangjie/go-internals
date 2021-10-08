
---
title: 'introduction to the go compiler ssa backend'
score: '⭐️⭐️⭐️'
tags: ['compiler']
author: 'gophers'
publisher: 'golang'
status: 'Finished'
link: 'https://github.com/golang/go/blob/release-branch.go1.13/src/cmd/compile/internal/ssa/README.md'
---

# Let's Summarize

介绍了ssa的关键概念，value、memory、block、function、compiler pass，介绍了查看从源代码到ssa各阶段优化再到最终生成的机器指令的查看方法：GOSSAFUNC=${func} go build *.go，会生成一个ssa.html文件，打开即可查看

# Source Analysis



# References
1. https://github.com/golang/go/blob/release-branch.go1.13/src/cmd/compile/internal/ssa/README.md
