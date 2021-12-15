
---
title: 'understand the empty interface'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['interface']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-understand-the-empty-interface-2d9fc1e5ec72'
---

# Let's Summarize

介绍了interface的内部表示，但是只介绍了空接口（方法集为空）。

src/runtime/runtime2.go中区分了空接口和非空接口的表示，分别是eface和iface：
- 它们都有一个动态值字段；
- 关于动态类型字段eface比较直接，直接就是_type类型的字段；
- 关于动态类型字段iface由于除了类型还要包括方法的调用表，与eface稍有不同，其使用itab类型，该类型内部有一个动态类型_type的字段，还有一个方法调用表字段fun。

这部分就先介绍到这里，理解了interface{}的长相，很多东西就容易理解。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-understand-the-empty-interface-2d9fc1e5ec72
