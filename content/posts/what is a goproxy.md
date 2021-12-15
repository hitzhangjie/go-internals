---
title: "what is a goproxy"
score: '⭐️⭐️⭐️⭐️⭐️'
author: 'Ankush Chadha'
publisher: 'jfrog'
tags: ['goproxy']
status: 'Ready to Start'
weight: 1
link: 'https://jfrog.com/blog/why-goproxy-matters-and-which-to-pick/'
---

# Let's summarize

介绍了goproxy的用途，保证“构建的确定性”和“构建时依赖的可用性”。

public goproxy和private goproxy通过环境变量GOPROXY和GOPRIVATE进行区分，通常我们访问公共的代码库要通过GOPROXY中的配置去获取，而访问公司内私有仓库则访问GOPRIVATE中配置的去访问。

其实就是要获取的module importPath去和GOPRIVATE匹配，匹配成功则走importPath中的域名去拉取，反之则全部走GOPROXY去拉取。

也有中办法通过配置一个集中式的GOPROXY来代替public、private模块请求，它内部再去区分对待，比如JFrog Artifactory，腾讯内部也是自己搭了一个集中的proxy来代理public、private modules所有请求。

# Source Analysis

# Reference

- https://jfrog.com/blog/why-goproxy-matters-and-which-to-pick/'

