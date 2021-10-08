
---
title: 'string & conversion optimization'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['string']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-string-conversion-optimization-767b019b75ef'
---

# Let's Summarize

b := genBytes() []byte { return []byte{"a","b"} }

switch string(b) { ... }：这里的string(b)做了优化不会执行拷贝，直接用了原来b的底层数组做为string的底层数组；

访问map元素时：m := map[string]int{}, m[string(b)] 这里的key对应的string底层数组也是直接用的b的底层数组；

字符串连接时：println("("+string(b)+")")，这字符串连接结果肯定要分配新空间，但是string(b)自己是没有再分配新空间的；

字符串比较时：这种情况和switch时的比较类似，先比较string长度，再比较底层bytes数组长度，再比较string内容本身；


# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-string-conversion-optimization-767b019b75ef
