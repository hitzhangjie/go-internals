
---
title: 'introduction to the escape analysis'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['compiler']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-introduction-to-the-escape-analysis-f7610174e890'
---

# Let's Summarize

escape analysis不只是go中才有的概念，java se 6u23及更新版本均也支持逃逸分析，see：
- https://en.wikipedia.org/wiki/Escape_analysis

go查看逃逸分析结果，可以通过给编译器传递选项-m，如源文件为main.go，可执行：
- go build -gcflags="-m" main.go
- go tool compile -m main.go

go里面有几种情况会发生逃逸：
- 一个函数内部new(obj)并返回指针，或者声明变量并返回指针，该指针在该函数外被继续使用，会发生逃逸；
- 一个for循环体内new(obj)创建对象并赋值给外部指针，或者用其他方式声明如`var a int`然后取地址赋值，会发生逃逸；
- 一个闭包内通过new(obj)创建对象并赋值给外部指针，或者用其他方式声明如`var a int`然后取地址赋值，会发生逃逸；

ps：在一个普通的{}构成的块作用域内new(obj)或者对声明变量取地址赋值给外部指针，都是不会发生逃逸的，因为在同一个栈帧内，并不存在outlive the stack frame的情况，根本不需要讨论逃逸的问题。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-introduction-to-the-escape-analysis-f7610174e890
