
---
title: 'go register ABI'
score: '⭐️⭐️⭐️⭐️'
tags: ['abi']
author: 'Eli Bendersky'
publisher: ''
status: 'Finished'
link: 'https://eli.thegreenplace.net/2022/interface-method-calls-with-the-go-register-abi/'
---

# Let's Summarize

go从1.17开始使用基于寄存器的ABI，以前的时候是通过栈变量的形式来传递函数参数、返回值信息的，现在改成通过寄存器了。go1.17中只有amd64架构采用了基于寄存器的ABI，go1.18中扩展到了更多的架构中。

# Source Analysis



# References
1. https://eli.thegreenplace.net/2022/interface-method-calls-with-the-go-register-abi/
