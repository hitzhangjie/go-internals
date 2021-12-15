
---
title: 'scheduling in go: part i - os scheduler'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['gpm scheduler']
author: 'William Kennedy'
publisher: 'ardan labs'
status: 'Finished'
link: 'https://www.ardanlabs.com/blog/2018/08/scheduling-in-go-part1.html'
---

# Let's Summarize

本文是这个文集中的第一篇，以操作系统调度器为例，介绍了调度过程中涉及的一些内容：
- PC：线程切换后如何恢复下一条待执行指令的地址；
- 线程状态：线程是running、runnable、waiting状态的，调度器可以调度哪些线程，哪些不能；
- 任务类型：计算密集型、IO密集型，通常后者才会牵扯到任务调度问题；
- 上下文切换：上下文切换也有协作式或者抢占式之分，上下文切换是有开销的，如线程切换一次大约为1.4微秒左右，这点时间现代处理器可以执行1.2w~1.8w条指令，实际值可能会更高；
- 多少个线程合适，过多的线程会给线程调度带来开销，需要根据处理器核数、线程数、处理任务之间寻找一个相对合理的平衡值；
- cache一致性问题，现代处理器存储层次中存在多级cache，多线程程序需要考虑cache一致性问题。cache本身会提高性能，大牛市如果线程切换到不同核执行，可能会带来cache失效问题，也会引入开销；
- 调度决策，如何选择下一个待调度的线程执行；

本文相当于是从操作系统线程的角度出发，将调度器设计实现过程中可能遇到的一些主要问题都做了提纲挈领的一个概述，这些问题虽然是围绕着线程来说的，但是这也是实现一个优秀的协程调度器需要考虑的。

这篇文章将这些，都是为后文深入介绍go运行时调度器做铺垫的。

# Source Analysis



# References
1. https://www.ardanlabs.com/blog/2018/08/scheduling-in-go-part1.html
