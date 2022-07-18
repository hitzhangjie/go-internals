---
weight: 2
bookFlatSection: true
title: "简介"
---

# 简介

## Go语言简介

go语言是由Google设计开发的一种编程语言，说go语言师出名门一点不过分，它的三位设计者 [Robert Griesemer](https://en.wikipedia.org/wiki/Robert_Griesemer_(computer_programmer)), [Rob Pike](https://en.wikipedia.org/wiki/Rob_Pike)，以及 [Ken Thompson](https://en.wikipedia.org/wiki/Ken_Thompson)，都是计算机科学技术方面颇有造诣的专家。

- Robert Griesemer，1964年生，其主要贡献包括：Chrome V8 Javascript引擎、Sawzall语言、Java Hotspot虚拟机、Strongtalk（在smalltalk上增加了一些强类型检查支持）；
- Rob Pike，1956年生，其主要贡献包括：分布式操作系统Plan9、分布式操作系统Inferno、编程语言Limbo；
- Ken Thompson，1943年生，Unix操作系统、B语言、和Dennis Ritchie共同发明的C语言、分布式操作系统Plan9；

go设计时吸收了其他编程语言的经验、教训，最终呈现出来的是尽可能实用高效的特性：

- 支持静态类型的编译型语言 see [go programming language][1]；

- 类似c语言的简洁的语法 see [go spec][2]；

- 更好的内存安全性；

- 支持动态内存管理，更简单的GC调优控制；

- 支持结构化类型 see [types checking](https://medium.com/higher-order-functions/duck-typing-vs-structural-typing-vs-nominal-typing-e0881860bf10)；

- 支持通信串行处理风格的并发编程模式。

go语言深受广大开发者喜爱，在[TIOBE 2021编程语言排名][4]上位列第13名，但是我们限定下使用场景的话，强类型、编译型语言、网络服务、大型分布式系统，实际上Go的排名会更加亮眼。结合自己C\C++\Java开发体验来看，go语言无疑是一门不错的编程语言。

| Jul 2022 | Jul 2021 | Change                                                       | Programming Language                                         | Ratings              | Change |        |
| :------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :------------------- | :----- | ------ |
| 1        | 3        | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/up.png) | ![Python page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/Python.png) | Python               | 13.44% | +2.48% |
| 2        | 1        | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/down.png) | ![C page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/C.png) | C                    | 13.13% | +1.50% |
| 3        | 2        | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/down.png) | ![Java page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/Java.png) | Java                 | 11.59% | +0.40% |
| 4        | 4        |                                                              | ![C++ page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/C__.png) | C++                  | 10.00% | +1.98% |
| 5        | 5        |                                                              | ![C# page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/C_.png) | C#                   | 5.65%  | +0.82% |
| 6        | 6        |                                                              | ![Visual Basic page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/Visual_Basic.png) | Visual Basic         | 4.97%  | +0.47% |
| 7        | 7        |                                                              | ![JavaScript page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/JavaScript.png) | JavaScript           | 1.78%  | -0.93% |
| 8        | 9        | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/up.png) | ![Assembly language page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/Assembly_language.png) | Assembly language    | 1.65%  | -0.76% |
| 9        | 10       | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/up.png) | ![SQL page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/SQL.png) | SQL                  | 1.64%  | +0.11% |
| 10       | 16       | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/upup.png) | ![Swift page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/Swift.png) | Swift                | 1.27%  | +0.20% |
| 11       | 8        | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/down.png) | ![PHP page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/PHP.png) | PHP                  | 1.20%  | -1.38% |
| 12       | 13       | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/up.png) | ![Go page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/Go.png) | Go                   | 1.14%  | -0.03% |
| 13       | 11       | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/down.png) | ![Classic Visual Basic page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/Classic_Visual_Basic.png) | Classic Visual Basic | 1.07%  | -0.32% |
| 14       | 20       | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/upup.png) | ![Delphi/Object Pascal page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/Delphi_Object_Pascal.png) | Delphi/Object Pascal | 1.06%  | +0.21% |
| 15       | 17       | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/up.png) | ![Ruby page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/Ruby.png) | Ruby                 | 0.99%  | +0.04% |
| 16       | 21       | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/upup.png) | ![Objective-C page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/Objective_C.png) | Objective-C          | 0.94%  | +0.17% |
| 17       | 18       | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/up.png) | ![Perl page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/Perl.png) | Perl                 | 0.78%  | -0.12% |
| 18       | 14       | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/downdown.png) | ![Fortran page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/Fortran.png) | Fortran              | 0.76%  | -0.36% |
| 19       | 12       | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/downdown.png) | ![R page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/R.png) | R                    | 0.76%  | -0.57% |
| 20       | 19       | ![change](https://www.tiobe.com/wp-content/themes/tiobe/tpci/images/down.png) | ![MATLAB page](https://www.tiobe.com/wp-content/themes/tiobe/tiobe-index/images/MATLAB.png) | MATLAB               | 0.73%  | -0.15% |

see

[1]: https://en.wikipedia.org/wiki/Go_(programming_language)	"Go programming language"
[2]: https://go.dev/ref/spec "go spec"
[3]: https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form	"EBNF (vs BNF)["
[4]: https://www.tiobe.com/tiobe-index	"TIOBE Index"

## 目标读者

我们会把内容重点放在语言核心特性、标准库、优秀三方组件的设计实现的思路上，而非介绍基础的语法、标准库怎么用、并发编程应该怎么写这类问题。本电子书内容不是去介绍“how-to”，而是倾向于介绍“why”。

当然，我们可能会借助一些示例代码来引入设计实现的内容（“why”），这样也能帮助读者更好地掌握如何写代码（“how-to”），但是还是要提一下 :)

如果读者已经熟悉了go，有了一定的编程经验，并且希望来了解下go语言具体的设计实现的时候，我觉得这个时候来读这本书就很合适。

## 本书内容

本电子书内容会尽可能覆盖go语言设计开发所涉及到的各个方面，范围包括编译器、链接器、调试器工具链，包括问题诊断debugging、pprof、tracing使用及工作原理、包括goroutine、go运行时（monitor、scheduler）、内存管理（内存分配器、垃圾回收器）、标准库、goproxy、testing技术等等吧。

每一项内容深究下去都会有非常多的挑战点，这会超越个体的知识极限，所以我不打算自己去琢磨这些内容，而是选择站在巨人肩膀上，在别人已经输出的高价值的内容基础上去学习、完善，所以读者会在本书中看到大量的参考链接，如果我的理解有误、读者发现后也可以求证后给我指出来。

## 作者介绍

一名想变大师傅的小码农 🥷



