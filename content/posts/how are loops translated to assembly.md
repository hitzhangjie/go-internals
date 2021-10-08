
---
title: 'how are loops translated to assembly'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['compiler']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-how-are-loops-translated-to-assembly-835b985309b3'
---

# Let's Summarize

介绍了for循环如何被转换成汇编的，主要是理解转换成的汇编的含义。本文还提及了go1.10之前生成for循环汇编指令时会生成一个指针，并且这个指针存在past-the-end的问题，会导致程序难以进入safepoint，不容易被抢占。

在非协作式抢占的建议草案中也有提及这里的生成的临时指针past-the-end问题，该问题会影响到scheduler，for循环体中不容易被其他goroutine抢占，非协作式抢占设计实现中提及了此问题。

TODO：我没有看太明白这里生成的临时指针past-the-end问题，究竟会导致什么样的不安全问题？

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-how-are-loops-translated-to-assembly-835b985309b3
