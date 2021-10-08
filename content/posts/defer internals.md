
---
title: 'defer internals'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['defer']
author: ''
publisher: ''
status: 'Finished'
link: 'https://tpaschalis.github.io/defer-internals/'
---

# Let's Summarize

本文内容很多，我只关注了其对openDefer的解释，一个openDefer的defer，或者说一个open-coded defer指的是这样的defer，不是在for循环中被调用的defer。

举个例子：

func TestOpenAndNonOpenDefers(t *testing.T) {
    // f() is a more complicated function that is recover()"ed
    for {
        defer f() // <-- non open-coded defer
    }
    defer f() // <-- open-coded defer
}

# Source Analysis



# References
1. https://tpaschalis.github.io/defer-internals/
