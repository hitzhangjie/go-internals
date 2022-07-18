
---
title: 'go plugin system'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['plugin']
author: 'Eli Bendersky'
publisher: ''
status: 'Finished'
link: 'https://eli.thegreenplace.net/2021/plugins-in-go/'
---

# Let's Summarize

介绍了go的插件机制：
1、一种是编译时插件机制，只需要显示import，然后插件实现里面显示注册，这种比较常见，比如database/sql的驱动实现mysql这种方式；
2、一种是运行时插件机制，这种需要在程序运行期间动态加载，比如将插件编译为共享库文件*.so，然后主程序动态加载并调用初始化插件方法完成初始化；
3、一种是主程序与插件进程隔离，彼此之间通过进程间通信来解决，通信方式可以是pipe、fifo、rpc等，hashicorp/go-plugin为这种插件机制提供了支持。

# Source Analysis



# References
1. https://eli.thegreenplace.net/2021/plugins-in-go/
