
---
title: 'init functions'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['init']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-init-functions-319dbb12831c'
---

# Let's Summarize

介绍了go程序中func init()函数的调用时机以及如何避免重复调用的。

package a依赖package b，那么先执行b中的全局变量初始化、func init函数，再执行a中的全局变量初始化、func init函数，这些都是在执行main.main之前完成的。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-init-functions-319dbb12831c
