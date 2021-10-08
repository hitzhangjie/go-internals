
---
title: 'map design by code - part 2'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['map']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-map-design-by-code-part-ii-50d111557c08'
---

# Let's Summarize

mapaccess_faststr, mapaccess_fast64...访问map中元素时，根据key类型不同编译器插入不同的函数调用，函数名后缀表示key的类型，为什么有不同的函数呢？这是为了提高key的hash计算效率和比较效率。/// map提前初始化再赋值，比lazy初始化后再赋值效率高，为什么呢？lazy初始化桶是后面创建的更花时间。但是lazy初始化相比较而言容易节省内存。/// map中kvpairs的存储有考虑内存占用方面的优化，key的类型和value的类型可能不同，所以在数据对齐过程中padding会浪费不少内存，所以go map中的keys和values是分开存储的，先存储keys再存储values。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-map-design-by-code-part-ii-50d111557c08
