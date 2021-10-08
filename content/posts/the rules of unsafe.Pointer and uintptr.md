
---
title: 'the rules of unsafe.Pointer and uintptr'
score: '⭐️⭐️⭐️⭐️'
tags: ['garbage collector']
author: 'gophers'
publisher: 'golang'
status: 'Finished'
link: 'https://golang.org/pkg/unsafe/#Pointer'
---

# Let's Summarize

unsafe.Pointer和uintptr可以互转，但是要注意转换时是否是有效的，有可能一个uintptr对应的对象已经被GC掉了，这个时候将其转换为指针其实是一个野指针。go编译器提供了一些patterns来识别什么时候unsafe.Pointer转为uintptr时不要让垃圾回收器GC掉指针对应的内存。

通常可以用go vet来检查一些误用情况，如果存在误用，会提示错误：possible misuse of unsafe.Pointer，但是只是possible misuse，不是misuse。

go vet也确实存在误报的情况，而且可能这个误报比率还有点高：https://github.com/golang/go/issues/41205.

这里也有人提过这个问题，如何绕过go vet检查：https://github.com/golang/go/issues/44836#issuecomment-792419407，但是我不建议使用这种方式，系统调用返回的uintptr如果是非go heap管理的，可以完全不用care go vet的误报，没必要为了绕过go vet的误报而做这种看上去有损可读性的编码。

# Source Analysis



# References
1. https://golang.org/pkg/unsafe/#Pointer
