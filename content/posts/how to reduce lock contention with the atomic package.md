
---
title: 'how to reduce lock contention with the atomic package'
score: '⭐️⭐️⭐️⭐️⭐️'
tags: ['locks']
author: 'Vincent Blanchon'
publisher: 'medium'
status: 'Finished'
link: 'https://medium.com/a-journey-with-go/go-how-to-reduce-lock-contention-with-the-atomic-package-ba3b2664b549'
---

# Let's Summarize

atomic、mutex、rwmutex，写多读少直接用mutex，读多写少用rwmutex，如果要考虑提升性能，可以考虑atomic。

# Source Analysis



# References
1. https://medium.com/a-journey-with-go/go-how-to-reduce-lock-contention-with-the-atomic-package-ba3b2664b549
