
---
title: 'a race detector unfurled'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['race detector']
author: 'Kavya Joshi'
publisher: 'youtube'
status: 'Finished'
link: 'https://www.youtube.com/watch?v=4r9Kr_HtGdI&t=639s'
---

# Let's Summarize

Talk by Kavya Joshi.
Race detectors are seriously cool tools that make writing race-free concurrent code easy — they detect the ever so elusive race conditions in a program. The Go race detector is one such tool that ships with Go, thereby making the magic of race detection trivially accessible to you and me.
This talk will present the subtleties of race detection and explore how the Go race detector does it. We will delve into the race detector"s use of vector clocks (from distributed systems!) to detect data races, including its implementation. Finally, we will touch upon the clever optimizations that make the tool practical for use in the real world.

可以详细描述下race detector实现细节。大致通过向量时钟来判断有没有并发的读写逻辑（要么是存在happens-before关系的操作，要么是完全并发的操作），如果存在并发的，则认为存在data race。

TODO 可以继续补充下细节，如向量时钟是什么、怎么实现向量时钟、go运行时中如何使用向量时钟来分析是否存在并发data race操作的、实现细节。


# Source Analysis



# References
1. https://www.youtube.com/watch?v=4r9Kr_HtGdI&t=639s
