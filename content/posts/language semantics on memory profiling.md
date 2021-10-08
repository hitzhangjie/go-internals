
---
title: 'language semantics on memory profiling'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['mechanics']
author: 'William Kennedy'
publisher: 'ardan labs'
status: 'Finished'
link: 'https://www.ardanlabs.com/blog/2017/06/language-mechanics-on-memory-profiling.html'
---

# Let's Summarize

Go has some amazing tooling that allows you to understand the decisions the compiler is making as it relates to escape analysis. Based on this information, you can refactor code to be sympathetic with keeping values on the stack that don’t need to be on the heap. You are not going to write zero allocation software but you want to minimize allocations when possible.

That being said, never write code with performance as your first priority because you don’t want to be guessing about performance. Write code that optimizes for correctness as your first priority. This means focus on integrity, readability and simplicity first. Once you have a working program, identify if the program is fast enough. If it’s not fast enough, then use the tooling the language provides to find and fix your performance issues.

# Source Analysis



# References
1. https://www.ardanlabs.com/blog/2017/06/language-mechanics-on-memory-profiling.html
