---
layout: post
title: Structure and Algorithm
category: Basic
---

1. 找出所有元素出现了两次后加入的一个元素的问题(xor)，扩展为加入两个的问题(xor, split, xor)
2. 最大子数组和的问题 `end[i] = max(end[i - 1] + arr[i], arr[i]), all[i] = max(end[i - 1] + arr[i],  all[i - 1])`。扩展为可循环数组？找最小子数组和。更有意思的是从推到`end[i] = max(end[i - 1] + arr[i], arr[i])`看出end[i - 1] < 0是 end[i]需要重新累加，因此直接相加比最大就行了。
3，最长公共子序列 `d[i][j]=d[i - 1][j - 1] + 1 or max(d[i - 1][j], d[i][j - 1])`
4，最长公共子串 `d[i][j]=d[i - 1][j - 1] + 1 or 0`
