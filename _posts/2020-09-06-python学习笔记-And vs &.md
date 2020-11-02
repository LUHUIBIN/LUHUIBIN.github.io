---
layout:     post
title:      python学习笔记-And vs &
subtitle:   And 和 &的区别
date:       2020-09-06
author:     HB
header-img:
catalog: true
tags:
    - Python
---

### and vs &
#### &为两个数值在内存上二进制表示的按位与

1&2为1和2的二进制表示01与10按位与，为00，所以结果为0。

2&3为2和3的二进制表示10与11按位与，为10，所以结果为2。
####  and 为逻辑上的真假判断。


```
>>> 17&1
1
>>> 16and 1
1
>>> 17and 1
1
1and 17
17
>>>2&3
2
>>>2and 0
0
>>>0and 3
0
>>>1 and 6
6
```
若两个数值都为非零则返回后一个数字。
