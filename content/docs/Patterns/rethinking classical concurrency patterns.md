
---
title: 'rethinking classical concurrency patterns'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['concurrency']
author: 'Bryan Mills'
publisher: 'google'
status: 'Finished'
link: 'https://drive.google.com/file/d/1nPdvhB0PutEJzdCq5ms6UI58dp50fcAN/view'
---

# Let's Summarize

We started with asynchronous patterns, which deal with goroutines. Then, we looked at condition variables, which sometimes deal with resources.

Now, let"s put them together. The Worker Pool is a pattern that treats a set of
goroutines as resources.

Just a note on terminology: in other languages the pattern is usually called a “thread pool”, but in Go we"re working with goroutines, so we just call them workers.

# Source Analysis



# References
1. https://drive.google.com/file/d/1nPdvhB0PutEJzdCq5ms6UI58dp50fcAN/view
