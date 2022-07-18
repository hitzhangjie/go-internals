
---
title: 'go spec'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['design']
author: 'gophers'
publisher: 'golang'
status: 'Reading'
link: 'https://go.dev/ref/spec'
---

# Let's Summarize

go spec描述了go语言文法（语法），通过阅读这里的内容，可以了解到整个语言在常规写法上的一些内容，一些可能比较隐晦的问题也能搞明白这背后的原因是什么，比如断行规则怎么来的、iota取值怎么来的等等的吧。个人感觉通读一下还是很有帮助的。

—————————————————————————————————————

go spec就是go语言的一些规范，包括：
- 描述了go语言文法（grammar），go spec的文法是通过EBNF定义的。
从这里可以了解到这门编程语言在文法层面是如何定义的，我们写代码的时候写出的源代码必须符合文法定义，编译器也会依照此文法对源代码进行检查（词法分析、语法分析）。
在学习编译原理课程时，我们设计一门语言，假设这门语言的功能支持已经确定了，我们现在也大致确定了这门编程语言的写法，为了指导别人这个语言可以怎么写、编译器该如何解析，就要定义出文法。
文法定义一般通过BNF或者EBNF，后者用的更多些，其在描述编程语言能力上并没有比BNF强很多，但是它可以生成更精炼的规则。要想理解go spec中定义的文法，还是需要理解下EBNF的大致内容，see also：https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form。

- go源代码采用utf8编码，对于特殊字符如0xfeff（bom）的忽略等特殊处理。
- go源码表示
  - characters：newline、unicode_char、unicode_letter、unicode_digit的表示
  - letters and digits：letter、decimal_digit、binary_digit、octal_digit、hex_digit的表示
- go词法元素（lexical elements）
  - 注释、
  - tokens（四类：identifier, keyword, operators 和 punctuation, literals)，whitespace的构成（空格、tab、回车、换行）及什么情况下可忽略，换行EOL和文件结束EOF会替换成分号’;’。
  - semicolons（分号的断行规则），词法分析时什么时候会自动插入分号。这些分号是自动插入的以充当语句结束时的终结符。
  - identifiers的生成规则
  - keywords，不能定义与关键字、保留字相同的标识符
  - operators and punctruation，有几个位运算符有点和其他语言不一样😟
  - integer literals，如何表示一个数是什么进制的数字呢？0b/0B前缀表示二进制数，0/0o/0O表示八进制数，0x/0X表示十六进制数，没有前缀、单独一个0表示十进制数。这些进制数的前缀后面可以通过下划线’_’和数字相连来提高可读性。对于十进制数而言，1_2 == 12（weired! 😟)
  - floating-point literals，略
  - imaginary literals，虚数，略
  - rune literals，主要是这几个：\a（alert or bell），\f （form feed，效果相当于光标下移一行），\r（carriage return，效果相当于移到行首覆盖写），\n（new line，换新行），\t （horizontal tab），\v（vertical tab），\b （backspace，删除前面的输出字符）
  - string literals，这个注释两种模式`raw string`和”interpreted string”，前者string中的转移字符’\’都是普通字符、没有转义动作，而后者里面的字符转义字符就有转义动作。
  - constants，包括bool、rune、integer、浮点、复数、字符串常量，rune、integer、浮点、复数统一看做数值常量。constants可以是有类型的，也可以是无类型的。对于无类型数值常量，可以使用更高的精度（256bits精度），see：https://blog.learngoprogramming.com/learn-golang-typed-untyped-constants-70b4df443b61。
  - variables
  - types，类型确定的是value范围以及对value的操作集合。bool类型true/false，number类型（整数是用补码表示的），string类型（字符串是不可变的，也不能取s[i]的地址），array类型（数组长度是类型的一部分），slice类型（data、cap、len，data指向底层数组，注意slices共享底层数组的情况），struct（如何定义、怎么写tag、字段匿名嵌套及约束）
  - pointers，指针类型（go中的指针没有运算功能，如+1、-1等）
  - function，函数签名只需参数列表、返回值列表有关系，与函数名没有关系。
  - interfaces（接口主要分为eface和iface两种，eface可以接受任何值，iface只能接收实现了接口方法的类型值。接口中存储的值及其类型通常称为dynamic value、dynamic type，eface{dtype, dvalue}，iface{itab, dvalue}，eface和iface在结构上稍有不同，后者主要是为了实现类似c++ vtable一样的功能，通过接口T是否实现了接口X：1）如果T不是接口，T必须实现X的所有方法；2）如果T是接口，T必须包含了X定义的所有方法。实现了接口X的类型T的任何value都实现了这个接口X。
     注意，go后续版本引入了关键字any，any是interface{}的一个alias。
  - map类型，map是通过hash表实现的无序的map，map定义时map[key]value，keytype必须是可比较的，因此function、map、slice这几个都不能作为key类型，如果keytype是interface类型，那么interface中的dynamic type必须是可比较的，即必须支持==和≠的比较。
  - channel类型，通信串行处理csp并发编程范式，channel定义时可以限定发送、接收的方向，channel定义时也可以指定是否为buffered/unbuffered通信。
     unbuffered chan必须有一个sender、receiver就绪才不会阻塞，buffered chan在不满时send不会阻塞，在不空时recv不会阻塞，nil chan上执行send、recv总是阻塞。
     chan recv操作如果是v, ok := ← ch，这里的ok表示的是sent before closed的意思，close(ch)其实只是打个类似结束的标记，所以closed ch的recv动作不会阻塞，但是ok为false。
     轮询多个ch的读写通过select-case来完成，加个default分支可以实现try-send、try-recv操作。
  - type A=B定义类型别名，type A B定义一种新类型。
  - 类型要么完全相同，要么不同。对于named type（有名类型）肯定是与其他类型不同的，对于unnamed type（无名类型）就要比结构，see：https://go.dev/ref/spec#:~:text=that%20is%2C%20they%20have%20the%20same%20literal%20structure%20and%20corresponding%20components%20have%20identical%20types.%20In%20detail%3A。
  - method sets的概念，首先接收器类型不能是pointer或者interface，我们为类型T添加方法，写的时候func (t T) …以及func(t *T)…这里的t T和t T都是针对类型T而言的。通过value去访问方法可以访问到T上定义的方法，通过指针去访问方法可以访问到T以及*T上的方法。注意，这个方法集的理解没有问题。但是呢，现在为了方便调用，编译器做了这方面的支持，例如通过value调用*T上定义的方法时，会做一层中间转换doSomething(t T, args…) { doSomething(t *T, args…) }，就调用到*T上定义的方法了。
  - block，语法块的意思，显示的block和隐式的block，package、file都有自己隐式的block，另外if、for、switch、select也有自己隐式的block，block影响了scope（作用域）。
  - 导出identifier：关注这些，首字母大写的包级别类型名、函数名，或者导出的结构体的首字母大写的成员名。
  - iota的用法，iota用来定义一组相关性很强的数值常量时非常有用。1）iota的值取决于在constspec在constspec list中的索引位置（空行会被删除，空行不算）；2）iota在同一个constspec中出现多次的话值不变。
  - 定义新类型type A B。1）A和B是不同的类型，A也不继承B的方法集，除非B是一个接口；2）如果是type A struct {B}，这种形式的话A则通过嵌套类型B获得了B的方法集。ps：定义别名type A = B，A和B的方法集相同，但是因为A可能出现在与定义B时不同的package内，这时也只能显示调用A的导出方法。
  - 变量声明`var` & 短变量声明`:=`
  - 函数声明，包括函数和方法，比较特殊的是范型函数、泛型函数的类型参数、泛型函数调用前的实例化
  - 表达式：运算符、合法的identifier、组合字面量、函数字面量、method values、index表达式、slice表达式、type assert（类型断言）、函数调用、传递实参（arguments）给形参列表（parameters）、泛型函数的实例化
  - type inference（类型推断）、type unification（fixme？）、function arguments inference（fixme？）、constraint type inference（fixme？）；
  - 运算符及运算符优先级，算术运算符、逻辑运算符、字符串连接、地址运算、chan运算符、类型转换运算符（数值、字符串、slice等）
  - evaluation order，看下语句调用时参数的初始化顺序是怎样，比如`y[f()], ok = g(h(), i()+x[j()], <-c), k()`，初始化顺序为`f(), h(), i(), j(), <-c, g(), and k()`，是按照从左到右的顺序，并且是递归的。
  - 语句，各种各样的语句类型，略。
     - 注意++\—是语句，而非运算符，gospec中对运算符的定义没有包含++\—，而是当做语句来介绍的，see：https://go.dev/ref/spec#:~:text=The%20%22%2B%2B%22%20and%20%22%2D%2D%22%20statements%20increment%20or%20decrement%20their%20operands%20by%20the%20untyped%20constant%201. 
     - switch分为expression switch和type switch，后者可以这么写的`switch v := x.(type) {case int: fmt.Printf(”%d”, v), case …}`，这样写TypeSwitchGuard这里的文法定义了可以这样写，这样写会比较简单，省的在case后在做类型断言并转换了，v就是对应类型的值了。
  - goto，goto并不是能够随意跳转的，goto在c\cpp里面一般是用于函数内跳转的，setjmp/longjmp可以用于函数间跳转。goto是不是在函数内随便就可以跳呢，也不是：1）goto语句只能在相同的block内跳；2）goto语句跳转到的位置不能跳过这个位置处应该有的变量定义语句。
   - fallthrough，expression switch中有个fallthrough允许继续执行到下一个条件去判断，而不是默认break（和c\c++不一样，go里面的switch-case默认会从case分支break出来）
  - defer语句，defer语句将对应的函数放入后进先出的一个栈，函数参数在入栈时已经evaluated了。什么时候执行栈里面的函数呢？return的时候，或者所在的goroutine panicking的时候。联想下panic位置和recover的关系，以及recover什么情况下才能正常recover。
  - recover and panic，panic的序列成为panicking
  - print、println不能保证后续仍然出现在语言中，慎用
  - 其他内置函数以及常见的基础操作，略
  - 源代码组织：package、file、import dependencies
  - 程序执行及包初始化顺序：注意包初始化顺序，see：https://stackoverflow.com/a/49831018
  - runtime.Error是在error接口上包装了下，这么做是为了方便识别运行时错误
  - 其他系统考虑：unsafe下的alignof\offsetof\sizeof……，这里也描述了下go的内存对齐的规则，see https://go.dev/ref/spec#:~:text=The%20following%20minimal,array%27s%20element%20type.
  - 其他一些边边角角的略掉了。



# Source Analysis

- 

# References
1. https://go.dev/ref/spec
