---
layout: post
title: 一个python的随机字符串发生器
category: Python
---

不得不承认Python语言是一种很优雅的语言。那次我在网上搜了下如何获取随机字符串，有很多种方法，但是有这么一句话深深的吸引了我：

	''.join(map(lambda xx:(hex(ord(xx))[2:]),os.urandom(3)))

这里面的每个单词我都认识，但几乎每个单词都需要help，一个一个来

+ os.urandom: Return a string of n random bytes suitable for cryptographic use
+ ord:  Return the integer ordinal of a one-character string
+ hex: Return the hexadecimal representation of an integer or long integer
+ lambda:  a shorthand to create anonymous functions
+ map: Return a list of the results of applying the function to the items of the argument sequence(s).

所以这个函数的意思就是： 对于os.urandom产生的每一个字符， 把他们用十六进制表示的字符串（不含0x）连接起来。比如如果 os.urandom(3)产生了'abc', 因为 ord('a') = 97 = 0x61， 所以最后得到的是 616263。 

最后，这个函数产生的随机数位数是不固定的，虽然这个函数很酷，还是要少用，不易阅读，不过用来学习Python最好不过了.
