
---
title: 'slice and memory management'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['compiler']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-slice-and-memory-management-670498bb52be?source=---------4-----------------------'
---

# Let's Summarize

slice其结构用slice header来表示，包含data、len、cap 3个字段，这个很多文章提过了，现在提下slice操作中对内存操作方面的一点优化：
- Copy：如果要删除slice nums中索引位置x中的元素，可以通过copy([x:],[x+1:])，然后x=[x:len(x)-1]来完成，也可以通过x = append(x[:x],[x+1:])来完成，这里会涉及到个别索引位置overlap的问题，编译器会转换成使用runtime.memmove来处理，这个函数会解决overlap的情况，比如从头拷贝会覆盖的话就用从后面拷贝来解决，实现稍复杂；
- Reset：有时一个slice被复用，复用之前希望清空它，可以写一个for循环把对应元素全部清0，我们可以这么写，编译器1.5之后会识别此类代码并将其转换为runtime.memclr*函数，这个效率比较高，应该是类似于memset之类的吧。
- Allocate & Copy：其实新创建完一个slice时都会清0也是用的memclr*函数。如果是新创建完(make)之后立即跟着一个copy语句怎么办，那么清零就有点多余了，编译器也会识别这种情况，这种就不清零了。

go编译器一直在演进，让这门语言变得更加"聪明"！

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-slice-and-memory-management-670498bb52be?source=---------4-----------------------
