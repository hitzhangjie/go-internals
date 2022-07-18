
---
title: 'duck typing, structural typing, nominal typing'
score: '⭐️⭐️⭐️⭐️'
tags: ['types']
author: 'Saurabh Nayar'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/higher-order-functions/duck-typing-vs-structural-typing-vs-nominal-typing-e0881860bf10'
---

# Let's Summarize

首先说结论，go语言类型是structural typing，可以理解成它是一种在duck typing之上增加了编译时类型安全检查的typing，所以也会看到有人称其为type-safe duck typing。
下面简单总结下这几种typing的异同点：
- duck typing，最灵活，但是类型安全性不够，容易导致编译时无法发现的运行时错误，因为duck typing机制下，obj.callMethod()这里的callMethod是否有在obj下定义是没有编译时检查保证的，在运行时才会去检查。比如python、js是支持duck typing的；
- norminal typing，这种通过显示的声明类型实现了哪个接口，编译时类型检查器就可以根据这个声明的依赖关系去检查类型是否实现了接口所声明的所有方法。这种方式能保证类型安全，但是开发人员需要显示写的代码也变多了，而且类型、接口之间的关系是存在比较强的绑定，没那么灵活。
- structural typing，可以理解成duck typing和nominal typing的一种折中。首先开发人员在写代码的时候可以像duck typing那样去写代码，不需要显示声明类型实现了哪个接口，这样写代码写起来简单。另外，在编译时类型检查器可以做些类型安全检查，检查某个类型是否隐式实现了某个期望的接口。这样的话相当于吸收了duck typing、nominal typing各自的优点。

ps：将go称之为duck typing是不够严谨的，如果说成是type-safe duck typing还可以，准确地说还是应该用structural typing最准确。

# Source Analysis



# References
1. https://medium.com/higher-order-functions/duck-typing-vs-structural-typing-vs-nominal-typing-e0881860bf10
