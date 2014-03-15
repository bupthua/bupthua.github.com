---
layout: post
title: Structure and Algorithm
category: Basic
---


### 3-11
1. 找出所有元素出现了两次后加入的一个元素的问题(xor)，扩展为加入两个的问题(xor, split, xor)
2. 最大子数组和的问题 `end[i] = max(end[i - 1] + arr[i], arr[i]), all[i] = max(end[i - 1] + arr[i],  all[i - 1])`。扩展为可循环数组？找最小子数组和。更有意思的是从推到`end[i] = max(end[i - 1] + arr[i], arr[i])`看出end[i - 1] < 0是 end[i]需要重新累加，因此直接相加比最大就行了。
3. 最长公共子序列 `d[i][j]=d[i - 1][j - 1] + 1 or max(d[i - 1][j], d[i][j - 1])`
4. 最长公共子串 `d[i][j]=d[i - 1][j - 1] + 1 or 0`

### 3-12 海量数据处理
1. 从大量中找出返回频率最高的N个。【首先hash到M个文件，然后使用hash在单个文件统计出现次数，对每个文件使用堆排序得到前N个数据，对MN个得到top N
2. 多个分机只能与主机慢速通信，每个分机有大量数据，如何找出所有数据的Frequent TOP K。每个分机先排序，然后中位数提交（median_v, median_p)，比较k vs sum(median_p1, p2, ...., pn)
3. 找不重复的数，用bitmap or 2-bitmap， 还可以通过最高位不断将区间化小
4. 为什么要使用B+树而不是红黑树？ MyISAM的非聚集索引和InnoDB的聚集索引

### 3-14
1. 卡特兰数 f(n)=f(0)f(n - 1) + f(1)f(n - 2) + ...... + f(n - 1)f(n) = C(2n, n) / (n + 1) = C(2n, n) - C(2n, n + 1)，找钱问题，递归打印可能的序列，凸多边形划分问题
