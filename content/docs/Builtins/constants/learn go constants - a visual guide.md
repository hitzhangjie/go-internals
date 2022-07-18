
---
title: 'learn go constants - a visual guide'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['design']
author: 'Inanc Gumus'
publisher: 'medium'
status: 'Finished'
link: 'https://blog.learngoprogramming.com/learn-golang-typed-untyped-constants-70b4df443b61'
---

# Let's Summarize

介绍了go中的常量，有类型常量、无类型常量之间的区别，重点描述了无类型数值常量的高精度优势（untyped numerics constants），比如浮点默认是256位精度的。
gospec中规定这种无类型数值常量的精度可以是任意精度的，只不过在实现的时候编译器可能会采用有限精度，比如256bits，gospec里是有写明的：https://go.dev/ref/spec#:~:text=numeric%20constants%20have%20arbitrary%20precision%20in%20the%20language%2C%20a%20compiler%20may%20implement%20them%20using%20an%20internal%20representation%20with%20limited%20precision。

# Source Analysis



# References
1. https://blog.learngoprogramming.com/learn-golang-typed-untyped-constants-70b4df443b61
