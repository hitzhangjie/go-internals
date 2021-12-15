
---
title: 'language semantics on escape analysis'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['mechanics']
author: 'William Kennedy'
publisher: 'ardan labs'
status: 'Finished'
link: 'https://www.ardanlabs.com/blog/2017/05/language-mechanics-on-escape-analysis.html'
---

# Let's Summarize

Anytime a value is shared outside the scope of a function’s stack frame, it will be placed (or allocated) on the heap.

The construction of a value doesn’t determine where it lives. Only how a value is shared will determine what the compiler will do with that value. Anytime you share a value up the call stack, it is going to escape. There are other reasons for a value to escape which you will explore in the next post.

# Source Analysis



# References
1. https://www.ardanlabs.com/blog/2017/05/language-mechanics-on-escape-analysis.html
