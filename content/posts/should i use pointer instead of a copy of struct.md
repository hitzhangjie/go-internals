
---
title: 'should i use pointer instead of a copy of struct'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['pointer']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-should-i-use-a-pointer-instead-of-a-copy-of-my-struct-44b43b104963'
---

# Let's Summarize

什么时候使用pointer，什么时候使用value copy？

- 如果涉及密集的数据分配，适合用value copy而非指针，这样可以减少引入的GC开销；
- 而如果是涉及密集的函数调用，传参的时候适合用指针，可以减少值拷贝带来的开销；

总结一下，在涉及自动内存管理的语言中，使用指针代替值拷贝来提升性能的想法并不总是有效的，因为如果涉及的内存对象逃逸到了heap就会加重GC开销，如果作为函数参数的话，一般不涉及逃逸的情况，使用指针则可以减少值拷贝带来的开销，当然这里讨论的对象是些结构体之类相对较大的数据类型。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-should-i-use-a-pointer-instead-of-a-copy-of-my-struct-44b43b104963
