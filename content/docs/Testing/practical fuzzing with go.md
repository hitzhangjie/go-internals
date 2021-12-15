
---
title: 'practical fuzzing with go'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['fuzzy, test']
author: 'Roberto Clapis'
publisher: 'google'
status: 'Finished'
link: 'https://docs.google.com/presentation/d/1KkLrzc8O-dkBQ0itVWcqp3gZbtf_IM6MVfy84FndVlM/edit#slide=id.p'
---

# Let's Summarize

fuzzing test，模糊测试，指的是自动构造一些测试用例来进行测试，有助于节省编写测试用例的时间，有助于发现程序中存在的一些不健壮的处理逻辑、bug。

go新版本也将引入fuzzing test功能，到时候可以直接用。现阶段的话，需要借助一些第三方库来针对待测试函数的参数类型来自动构造用例，比如有些库之处自动填充struct中的字段，类似的库有：
- https://github.com/bxcodec/faker
- https://github.com/brianvoe/gofakeit
- https://github.com/google/gofuzz

# Source Analysis



# References
1. https://docs.google.com/presentation/d/1KkLrzc8O-dkBQ0itVWcqp3gZbtf_IM6MVfy84FndVlM/edit#slide=id.p
