---
layout: post
title: Python如此优雅，你知道么?
category: Python
---

不知道从什么时候开始，很多人桌上都有了一本Python基础教程或者学习手册类的书，这门语言迅速风靡了码农圈。而它的优雅，你全知道了吗？

1. Python的截取可以用负值表示位置
2. join只能对str，那么如果是int列表怎么办呢？ `'.'.join('%s' % id for id in dataList)` 瞧，多么优雅
3. 列表倒置 dataList[::-1]