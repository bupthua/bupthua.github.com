---
layout: post
title: Real Bugs
category: Other
---


--------------------
size_t 是无符号整数， 当str为空字符串时，用 int size = str.size() - 1 得到的不是 -1
