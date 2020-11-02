---
layout:     post
title:      CKeywords
date:       2020-11-02
author:     HB
header-img:
catalog: true
tags: static,const,define
    - C
---

## Static

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



## Const
```c
const int *A; //const修饰指向的对象，A可变，A指向的对象不可变
int const *A; //const修饰指向的对象，A可变，A指向的对象不可变
int *const A; //const修饰指针A， A不可变，A指向的对象可变
const int *const A;//指针A和A指向的对象都不可变
```
**分析上述代码可以看出，程序从左向右逐个读取，前两个例子，const修饰的都是int,而第三个例子从左往右依次读取会发现const修饰的是*，即指针A自身的内存不可变，A保存的整型的地址是可读写的。**

丑丑字的笔记
![photo_2020-11-02_21-09-32.jpg](https://i.loli.net/2020/11/02/mlPQjo6yRMWCahr.jpg)

## Pointer
这张图足以说明一切
![photo_2020-11-02_21-09-32.jpg](https://i.loli.net/2020/11/02/mlPQjo6yRMWCahr.jpg)


## define
```c
#define ADD(a,b)   a+b
```
在一般使用的时候是没有问题的，但是如果遇到如：c * Add(a,b) * d的时候就会出现问题，代数式的本意是a+b然后去和c，d相乘，但是因为使用了define（它只是一个简单的替换），所以式子实际上变成了 ca + bd 所以，用#define要注意顺序

一般我个人用#define在单片机程序上的话，我一般只做简单的替换。
```c
#define TIME_NUM   (60*60*24)UL//定义一个一天时间有多少秒
```
另外举一个例子：
```c
#define pin (int*);
pin a,b;
```
本意是a和b都是int型指针，但是实际上变成int* a,b;
a是int型指针，而b是int型变量。
这是应该使用typedef来代替define，这样a和b就都是int型指针了。
所以我们在定义的时候，养成一个良好的习惯，建议所有的层次都要加括号。

而且，宏在单片机代码中用的很多，常数的替换、地址的偏移，等等都用得上
用宏来修改移植代码更加便捷，代码更容易使人读懂。。。。

#### test
下面代码的含义：
```c
#define IS_GPIO_MODE(MODE) (((MODE) == GPIO_Mode_AIN) || ((MODE) == GPIO_Mode_IN_FLOATING) || \
                            ((MODE) == GPIO_Mode_IPD) || ((MODE) == GPIO_Mode_IPU) || \
                            ((MODE) == GPIO_Mode_Out_OD) || ((MODE) == GPIO_Mode_Out_PP) || \
                            ((MODE) == GPIO_Mode_AF_OD) || ((MODE) == GPIO_Mode_AF_PP))
```

可以理解为定义了一个函数，函数名是IS_GPIO_MODE，参数MODE，后面的一大串为函数内部实现方法.
