
---
title: 'design philosophy on data and semantics'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['mechanics']
author: 'William Kennedy'
publisher: 'ardan labs'
status: 'Finished'
link: 'https://ardanlabs.com/blog/2017/06/design-philosophy-on-data-and-semantics.html'
---

# Let's Summarize

“Value semantics keep values on the stack, which reduces pressure on the Garbage Collector (GC). However, value semantics require various copies of any given value to be stored, tracked and maintained. Pointer semantics place values on the heap, which can put pressure on the GC. However, pointer semantics are efficient because only one value needs to be stored, tracked and maintained.” - Bill Kennedy

A consistent use of value/pointer semantics, for a given type of data, is critical if you want to maintain integrity and readability throughout your software. Why? Because, if you are changing the semantics for a piece of data as it is passed between functions, you are making it difficult to maintain a clear and consistent mental model of the code. The larger the code base and the team becomes, the more bugs, data races and side effects will creep unseen into the code base.

# Source Analysis



# References
1. https://ardanlabs.com/blog/2017/06/design-philosophy-on-data-and-semantics.html
