---
layout:     post
title:      cConfusingPoints
date:       2020-11-02
author:     HB
header-img:
catalog: true
tags:
    - C
---

## static

#### 一、限制符号的作用域只在本程序文件
若变量或函数（统称符号）使用static修饰，则只能在本程序文件内使用，其他程序文件不能调用（非static的可以通过extern 关键字声明该变量是在其他文件内定义的，此文件可调用）。不加static修饰的，则默认是可以被其他程序文件调用的。


#### 二、指定变量的存储位置
对于函数内的变量。auto变量（函数局部变量）都是在**栈内**存区存放，函数结束后就自动释放。

但是全局的和函数内定义的static变量都是存放在数据区的，且只存一份，只在整个程序结束后才自动释放。

由于static变量只存一份即同一地址，所以不管函数调用多少次，函数内定义static变量的语句只会在第一次调用时执行，后面调用都不执行也不再初始化，而是对该地址内的数据进行操作。
```c
#include<iostream>
using namespace std;
void test()
{
    static int a = 1;
    a++;
    cout << a << endl;
    cout << &a << endl;
}
int main
{
    test();
    test();
    test();
    test();
}

输出：
2
00C90008
3
00C90008
4
00C90008
5
00C90008
//可见地址只有一个
```



## const
```c
const int *A; //const修饰指向的对象，A可变，A指向的对象不可变
int const *A; //const修饰指向的对象，A可变，A指向的对象不可变
int *const A; //const修饰指针A， A不可变，A指向的对象可变
const int *const A;//指针A和A指向的对象都不可变
```
**分析上述代码可以看出，程序从左向右逐个读取，前两个例子，const修饰的都是int,而第三个例子从左往右依次读取会发现const修饰的是*，即指针A自身的内存不可变，A保存的整型的地址是可读写的。**

![](https://ftp.bmp.ovh/imgs/2020/11/00466dc50c449270.jpg)


## pointer

![](https://ftp.bmp.ovh/imgs/2020/11/c0a217a31dd0e5ba.jpg)
