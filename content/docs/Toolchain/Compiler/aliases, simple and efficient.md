
---
title: 'aliases, simple and efficient'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['compiler']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-aliases-simple-and-efficient-8506d93b079e'
---

# Let's Summarize

go提供了定义类型别名的能力，`type A = B`，这样就将A定义为了类型B的别名，后面可以使用A来代替类型B。有什么好处呢：
- 做一些重构类的工作，假如之前代码中有个类型Type1被大量使用，现在重新实现了一个类型Type2希望能替换掉Type1，可以在使用Type1的地方通过`type Type1 = Type2`来创建一个别名已完成重构（当然也可以不用这种方式）；
- 提高可读性，比如有些函数的参数可能是一个函数，如filepath.Walk(path, func(fp string, inf os.FileInfo, err error) error)，现在还好，如果参数更多些就很难看了，如果定义`type WalkFunc = func(fp string, inf os.FileInfo, err error) error`，然后filepath.Walk(path, WalkFunc)`可读性就大大提升了；

运行时会对type alias做何处理呢？比如`type A = B`，如果给一个emptyInterface赋值了一个变量A：
- 那么类型断言它应该是A还是B呢？都必须断言成功！
- 那么反射获取其类型应该是谁呢？应该是B！
到底是如何处理的呢？编译器会在编译时，将对尝试需要类型A的地方使用类型B的信息，处理起来就简单了。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-aliases-simple-and-efficient-8506d93b079e
