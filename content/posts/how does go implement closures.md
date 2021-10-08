
---
title: 'how does go implement closures'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['closure']
author: 'zhangjie'
publisher: 'tencent'
status: 'Finished'
link: 'https://www.hitzhangjie.pro/blog/2018-05-19-golang-function-closure%E5%AE%9E%E7%8E%B0%E6%9C%BA%E5%88%B6/'
---

# Let's Summarize

介绍了go中闭包是如何实现的，包括闭包中引用的外部变量何时采用值捕获（readonly且数据量较小），何时采用引用捕获（readwrite，or数据量偏大）。编译器对闭包进行处理时，会自动完成上述判断与代码的转换。

# Source Analysis



# References
1. https://www.hitzhangjie.pro/blog/2018-05-19-golang-function-closure%E5%AE%9E%E7%8E%B0%E6%9C%BA%E5%88%B6/
