---
layout:     post
title:      C_for_interviews
date:       2020-11-02
author:     HB
header-img:
catalog: true
tags:
    - C
---
# 数据类型大小

![此处输入图片的描述][1]


  [1]: https://img-blog.csdnimg.cn/20190614110118525.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwNTAxODIw,size_16,color_FFFFFF,t_70
  
  一个字节（Byte）=8bit
一个float数据占用32bit,double数据占用64bit

# 什么是定义？什么是声明？它们之间的区别是什么？
所谓定义就是（编译器）创建一个对象，为这个对象分配一块内存，并给它取上一个名字，这个名字就是就是我们经常所说的变量名或对象名。

声明有2重含义：

（1） 告诉编译器，这个名字已经匹配到一块内存上，下面的代码用到变量或者对象是在别的地方定义的。声明可以出现多次。

（2） 告诉编译器，这个名字已经被预定了，别的地方再也不能用它来作为变量名或对象名。
**定义创建对象并为这个对象分配了内存，声明没有分配内存。**


# extern
可以置于变量或者函数前，以标示变量或者函数的定义在别的文件中，提示编译器遇到此变量和函数时在其他模块中寻找其定义。此外extern也可用来进行链接指定。extern用在变量声明中常常有这样一个作用，你在*.c文件中声明了一个全局的变量，这个全局的变量如果要被引用，就放在*.h中并用extern来声明。

# 语言中变量存储位置
https://0202zc.github.io/2020/02/01/C-variable-storage-2/
局部变量、静态局部变量、静态全局变量…
一、C语言中，常量存储在哪儿？static全局变量和static局部变量存储在哪儿？

全局变量（外部变量）的说明之前再冠以static就构成了静态的全局变量。全局变量本身就是静态存储方式，静态全局变量也是静态存储方式。这两者在存储方式上并无不同。这两者的区别虽在于

    非静态全局变量的作用域是整个源程序，
    当一个源程序由多个源文件组成时，非静态的全局变量在各个源文件中都是有效的，
    而静态全局变量则限制了其作用域。
    即只在定义该变量的源文件内有效，

在同一源程序的其他源文件中不能使用它。由于静态全局变量的作用域局限于一个源文件内，只能为该源文件内的函数公用，因此可以避免在其他源文件中引起错误。
二、static全局变量与普通的全局变量有什么区别？

    static全局变量只初始化一次，防止在其他文件单元中被是引用。

三、static局部变量与普通的局部变量有什么区别？

    static局部变量只被初始化一次，下一次依据上一次结果值。

四、局部变量、静态局部变量、静态全局变量存储位置
变量类型 	存储位置
局部变量 	静态区（全局区）
局部静态变量 	静态区（全局区）的常量区
全局静态变量 	静态区（全局区）
五、各存储区的定义

    栈区（stack） —— 由编译器自动分配释放，存放函数的参数值，局部变量的值等，其操作方式类似于数据结构中的栈。

    堆区（heap） —— 一般由程序员分配释放。若程序员不释放，程序结束时可能由OS回收。注意它与数据结构中的堆是两回事，分配方式倒是类似于链表。

    全局区（静态区）（static） —— 全局变零和静态变量的存储是放在一起的，初始化的全局变量和静态变量在一块区域，未初始化的全局变量和未初始化的静态变量在相邻的另一块区域，- 程序结束后由系统释放。

    文字常量区 —— 常量字符串就是放在这里的。- 程序结束后由系统释放。

    程序代码区 —— 存放函数体的二进制代码。

六、NOTES

    栈，就是那些由编译器在需要的时候分配，在不需要的时候自动清除的变量的存储区。里面的变量通常是局部变量、函数参数等。

    堆，就是那些由new分配的内存块，他们的释放编译器不去管，由应用程序控制，一般一个new就要对应一个delete。如果程序员没有释放掉，那么在程序结束后，操作系统会自动回收。

    自由存储区，就是那些由malloc分配的内存块，它和堆十分相似，不过它是用free来结束自己的生命。

    全局/静态存储区，全局变量和静态变量被分配到同一块内存中，在以前的C语言中，全局变量又分为初始化的和未初始化的，在C++里面没有这个区分，它们共同占用一块内存区。

    常量存储区，这是一块比较特殊的存储区，它们存放的是常量，不允许被修改。

# size_t是啥
size_t在C语言中就有了。
它是一种“整型”类型，里面保存的是一个整数，就像int, long那样。这种整数用来记录一个大小(size)。size_t的全称应该是size type，就是说“一种用来记录大小的数据类型”。
通常我们用sizeof(XXX)操作，这个操作所得到的结果就是size_t类型。
因为size_t类型的数据其实是保存了一个整数，所以它也可以做加减乘除，也可以转化为int并赋值给int类型的变量。

# 预处理 编译 汇编 链接
https://luomuxiaoxiao.com/?p=235

https://blog.csdn.net/qq_40501820/article/details/92715694?spm=1001.2014.3001.5501
# const关键字到底该怎么用？
https://www.yanbinghu.com/2019/01/28/7442.html

# 指针数组和数组指针的区别 
https://dmdada.github.io/2018/05/26/%E6%8C%87%E9%92%88%E6%95%B0%E7%BB%84%E5%92%8C%E6%95%B0%E7%BB%84%E6%8C%87%E9%92%88-md/


# 指针和引用的区别 

https://dmdada.github.io/2018/08/14/%E6%8C%87%E9%92%88%E5%92%8C%E5%BC%95%E7%94%A8%E7%9A%84%E5%8C%BA%E5%88%AB/

# 面试题之strcpy/strlen/strcat/strcmp的实现 
https://songlee24.github.io/2015/03/15/string-operating-function/

# C语言中的联合体Union
https://www.lujianxin.com/x/art/1ubkkobagqyq


# 万恶的Const  
```c
const int *A; //const修饰指向的对象，A可变，A指向的对象不可变
int const *A; //const修饰指向的对象，A可变，A指向的对象不可变
int *const A; //const修饰指针A， A不可变，A指向的对象可变
const int *const A;//指针A和A指向的对象都不可变
```
**分析上述代码可以看出，程序从左向右逐个读取，前两个例子，const修饰的都是int,而第三个例子从左往右依次读取会发现const修饰的是*，即指针A自身的内存不可变，A保存的整型的地址是可读写的。**

丑丑字的笔记
[![B6mOsK.png](https://s1.ax1x.com/2020/11/03/B6mOsK.png)](https://imgchr.com/i/B6mOsK)

##  easy pointer
这张图足以说明一切
[![B6nVeS.md.png](https://s1.ax1x.com/2020/11/03/B6nVeS.md.png)](https://imgchr.com/i/B6nVeS)

# define
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
用宏来修改移植代码更加便捷，代码更容易使人读懂。。。。.

test
下面代码的含义：
```c
#define IS_GPIO_MODE(MODE) (((MODE) == GPIO_Mode_AIN) || ((MODE) == GPIO_Mode_IN_FLOATING) || \
                            ((MODE) == GPIO_Mode_IPD) || ((MODE) == GPIO_Mode_IPU) || \
                            ((MODE) == GPIO_Mode_Out_OD) || ((MODE) == GPIO_Mode_Out_PP) || \
                            ((MODE) == GPIO_Mode_AF_OD) || ((MODE) == GPIO_Mode_AF_PP))
```

可以理解为定义了一个函数，函数名是IS_GPIO_MODE，参数MODE，后面的一大串为函数内部实现方法.
