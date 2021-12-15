
---
title: 'ordering in select statements'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['chan, select-case']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-ordering-in-select-statements-fd0ff80fd8d6'
---

# Let's Summarize

select中允许通过多个case分支对多个chan进行send、recv操作，如果同时有多个case分支满足时，应该选择激活哪一个分支呢？

每次执行select-case操作时会先将多个case分支打乱顺序（shuffle)，然后再逐个检查哪个分支条件满足。注意，select-case不支持去重，比如有一个case分支是对chan ch1执行操作，有9个分支是对chan ch2执行操作，那么ch2相关的case分支执行到的概率约为90%，而不是50%。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-ordering-in-select-statements-fd0ff80fd8d6
