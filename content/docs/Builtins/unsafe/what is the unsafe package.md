
---
title: 'what is the unsafe package'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['unsafe']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-what-is-the-unsafe-package-d2443da36350'
---

# Let's Summarize

package unsafe，见名知意，就是不安全，而且有可能代码后续会不兼容，因为unsafe的实现依赖go内部实现，比如数据类型的内部表示。

go文档中有明确指出：
- package unsafe包含了一些可能破坏go类型安全的操作；
- 引用package unsafe的代码兼容性差，并且不受Go 1 兼容性指引保护；

1 类型安全

我们可与通过uint8(int8(1))这种方式进行显示的类型转换操作，但是对于一个复杂的数据类型，如type A struct{ a int}，type B struct { b int}，虽然其内存数据表示完全相同，但是其仍然是不同的数据类型，我们不能使用上述的类型转换将一个B对象转换为为A对象。

package unsafe允许我们直接访问原始的内存，只要内存底层数据表示相同，我们就可以完成强制类型转换，比如var a = A{a:1}，我们可以通过var b = *((*B)(unsafe.Pointer(&a)))。

我们如果想查看string、slice、array等数据类型的表示，也可以通过这种方式来实现。

2 Go 1 兼容性指引

指引中明确告知unsafe的使用可能会破坏代码兼容性，因为unsafe这个包的实现依赖了语言的内部实现，如果语言内部实现发生了变化，unsafe的使用就可能无法正常工作，举个极端的例子，比如SliceHeader{data,cap,len}中字段顺序调整为SliceHeader{cap,len,data}。

理解这点就好了，应用开发中应该尽量避免unsafe包使用，如果可以的话。

详细指引，see：https://golang.org/doc/go1compat#expectations。

3 reflection & sync & runtime

这两个package下都大量使用了unsafe：
- 反射需要直接操作内存，这个很好理解；
- sync中sync.Pool中用到了对指针的操作，也需要用到unsafe；
- runtime中goroutine stack操作，也涉及到对内存的直接操作；

更多信息可以查看下源码。

4 Usage as a developer

前面提及的数据类型type A struct和type B struct的互转，或者涉及到cgo类的操作要大量用到unsafe.Pointer，go:linkname导出一个函数或者与绑定一个函数，等等吧，还是有很多场景可以使用的。

慢慢积累吧。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-what-is-the-unsafe-package-d2443da36350
