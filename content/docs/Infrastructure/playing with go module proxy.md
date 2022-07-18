
---
title: 'playing with go module proxy'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['goproxy']
author: 'Roberto Selbach'
publisher: ''
status: 'Finished'
link: 'https://roberto.selbach.ca/go-proxies/'
---

# Let's Summarize

介绍了goproxy的大致工作原理，根据goproxy protocol的官方设计说明，只要实现go module query必要的那些接口就可以算作是实现了goproxy。
其实我们可以自己实现简单的goproxy，有两个办法：1）因为goproxy protocol支持file://，因此我们可以直接将~/go/pkg/mod/cache/download这个路径设置为GOPROXY=file:///Users/<username>/go/pkg/mod/cache/download，这样也可以。2）另一种方法也可以直接启动一个FileServer返回上述目录中的东西，然后将GOPROXY指向这个FileServer监听地址。
要理解为什么这样能工作，其实只需要知道go mod query的过程即可，大致分为这么几步，比如要查询module github.com/a/b@version这个版本：
- 首先查询这个module的版本的list请求，获取版本列表；
- 然后根据请求的版本从list结果中选择版本，然后查询info请求，获得该版本的信息；
- 然后查询mod请求可能检查下有没有更新信息；
- 然后请求下载module-version.zip，这里面包含了go文件，将来会解压到~/go/pkg/mod/下面。

# Source Analysis



# References
1. https://roberto.selbach.ca/go-proxies/
