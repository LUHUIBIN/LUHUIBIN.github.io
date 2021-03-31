---
layout:     post
title:      embedded knowledge
date:       2021-3-27
author:     HB
header-img:
catalog: true
tags:
    - embedded
---

# 按键去抖
硬件消抖

在键数较少时可用硬件方法消除键抖动。下图所示的RS触发器为常用的硬件去抖。

![](http://news.eeworld.com.cn/uploadfile/mcu/uploadfile/201208/20120806045711275.jpg)

图中两个“与非”门构成一个RS触发器。当按键未按下时，输出为1;当键按下时，输出为0。此时即使用按键的机械性能，使按键因弹性抖动而产生瞬时断开（抖动跳开B），中要按键不返回原始状态A，双稳态电路的状态不改变，输出保持为0，不会产生抖动的波形。也就是说，即使B点的电压波形是抖动的，但经双稳态电路之后，其输出为正规的矩形波。这一点通过分析RS触发器的工作过程很容易得到验证。

另一种硬件消抖的方法利用电容的放电延时，采用并联电容法，也可以实现硬件消抖，如图3所示：

![](http://news.eeworld.com.cn/uploadfile/mcu/uploadfile/201208/20120806045712217.jpg)

软件消抖

如果按键较多，常用软件方法去抖，即检测出键闭合后执行一个延时程序，5ms～10ms的延时，让前沿抖动消失后再一次检测键的状态，如果仍保持闭合状态电平，则确认为真正有键按下。当检测到按键释放后，也要给5ms～10ms的延时，待后沿抖动消失后才能转入该键的处理程序。还可以利用定时器中断来消抖。




------------
# http协议
## HTTP请求
下图是在网上找的一张图，觉得能很好的表达HTTP请求的所发送的数据格式。
HTTP请求正文


![](https://pic2.zhimg.com/80/v2-12836e928e97f0d1acf375b34981a071_720w.jpg)
由上图可以看到，http请求由请求行，消息报头，请求正文三部分构成。

### HTTP请求状态行
请求行由请求Method, URL 字段和HTTP Version三部分构成, 总的来说请求行就是定义了本次请求的请求方式, 请求的地址, 以及所遵循的HTTP协议版本例如：

GET /example.html HTTP/1.1 (CRLF)
HTTP协议的方法有： GET： 请求获取Request-URI所标识的资源 POST： 在Request-URI所标识的资源后增加新的数据 HEAD： 请求获取由Request-URI所标识的资源的响应消息报头 PUT： 请求服务器存储或修改一个资源，并用Request-URI作为其标识 DELETE： 请求服务器删除Request-URI所标识的资源 TRACE： 请求服务器回送收到的请求信息，主要用于测试或诊断 CONNECT： 保留将来使用 OPTIONS： 请求查询服务器的性能，或者查询与资源相关的选项和需求

### HTTP请求头

HTTP请求报文
只有在发送POST请求时才会有请求正文，GET方法并没有请求正文。
![](https://pic4.zhimg.com/80/v2-839818777263adb12e93aafda6595633_720w.jpg)


## HTTP响应报文

![](https://pic1.zhimg.com/80/v2-d85efb19aec970b506b8cc7d2a2821dc_720w.jpg)

# 状态机
https://www.yanbinghu.com/2019/11/14/38034.html


# GDB调试
[GDB调试指南守望的个人博客](https://www.yanbinghu.com/2019/04/20/41283.html "GDB调试指南")



# 深入理解 STM32 双堆栈机制
https://www.shaoguoji.cn/2020/03/18/understand-stm32-stack/

# 深入理解堆和栈
https://blog.imallen.wang/2016/11/20/2016-11-20-shen-ru-li-jie-dui-he-zhan/

# 对于malloc、alloc、calloc、realloc的区别浅显的理解 
http://www.yanceymichael.com/2018/03/07/%E5%AF%B9%E4%BA%8Emalloc%E3%80%81alloc%E3%80%81calloc%E3%80%81realloc%E7%9A%84%E5%8C%BA%E5%88%AB%E6%B5%85%E6%98%BE%E7%9A%84%E7%90%86%E8%A7%A3/


# 实时操作系统
check wiki
# FreeRTOS
chech wiki

# linux下交叉编译windows程序
http://www.xefan.com/archives/83663.html

# https原理与过程
https://blog.imallen.wang/2016/11/20/2016-11-20-httpsyuan-li-yu-guo-cheng/


# 嵌入式软件工程师杂谈之一 —– BSP工程师
https://luomuxiaoxiao.com/?p=170

# 模拟实现atoi函数
https://dmdada.github.io/2018/05/27/atoi%E6%A8%A1%E6%8B%9F%E5%AE%9E%E7%8E%B0/
# GDP TCP 和IP数据报
https://dmdada.github.io/

# Http协议的三次握手，四次挥手
https://www.bilibili.com/read/cv5467505/

# 为什么连接的时候是三次握手，关闭的时候却是四次握手？

这是因为服务端的LISTEN状态下的SOCKET当收到SYN报文的建连请求后，它可以把ACK和SYN（ACK起应答作用，而SYN起同步作用）放在一个报文里来发送。但关闭连接时，当收到对方的FIN报文通知时，它仅仅表示对方没有数据发送给你了；但未必你所有的数据都全部发送给对方了，所以你未必会马上会关闭SOCKET,也即可能还需要发送一些数据给对方之后，再发送FIN报文给对方来表示你同意现在可以关闭连接了，所以它这里的ACK报文和FIN报文多数情况下都是分开发送的。



------------

一个有10个指针的数组，该指针是指向一个整型数的。（An array of 10 pointers to integers）
一个指向有10个整型数数组的指针（ A pointer to an array of 10 integers）

# volatile修饰符在C语言中的用法
http://forever.blog.chinaunix.net/uid-28614218-id-4737758.html

# 队列和栈的区别
 队列是先进先出，只能在一端插入另一端删除，可以从头或尾进行遍历（但不能同时遍历），
 栈是先进后出，只能在同一端插入和删除，只能从头部取数据

# C和c++的不同
 c和c++的一些不同点（从语言本身的角度）：
 1）c++源于c，c++最重要的特性就是引入了面向对象机制，class关键字。
 2）c++中，变量可以再任何地方声明；c中，局部变量只能在函数开头声明。
 3）c++中，const型常量是编译时常量；c中，const常量只是只读的变量。
 4）c++有&引用;c没有
 5）c++的struct声明自动将结构类型名typedef；c中struct的名字只在结构标签名字空间中，不是作为一种类型出现
 6）c语言的main函数可以递归调用;c++中则不可以
 7）c中，void *可以隐式转换成其他指针类型；c++中要求现实转换，否则编译通不过
 
# 下面的代码输出是什么，为什么？
```
void foo(void)
{
    unsigned int a = 6;
    int b = -20;
    (a+b > 6) ? puts("> 6") : puts("<= 6");
}```
解答：这个问题测试你是否懂得C语言中的整数自动转换原则，我发现有些开发者懂得极少这些东西。不管如何，这无符号整型问题的答案是输出是 ">6"。原因是当表达式中存在有符号类型和无符号类型时所有的操作数都自动转换为无符号类型。因此-20变成了一个非常大的正整数，所以该表达式 计算出的结果大于6。

还有一个重要的知识点：

通常情况下，在对int类型的数值作运算时，CPU的运算速度是最快的。在x86上，32位算术运算的速度比16位算术运算的速度快一倍。C语言是一个注重效率的语言，所以它会作整型提升，使得程序的运行速度尽可能地快。因此，你必须记住整型提升规则，以免发生一些整型溢出的问题。

整型提升是C程序设计语言中的一项规定，在表达式计算时（包括比较运算、算术运算、赋值运算等），比int类型小的类型（char, signed char, unsigned char, short, unsigned short等）首先要提升为int类型，然后再执行表达式的运算。

至于提升的方法，是根据原始类型进行位扩展（如果原始类型为unsigned char，进行零扩展，如果原始类型为signed char，进行符号位扩展）到32位。也就是说：

对于unsigned char，进行零扩展，即在左边的高位用 0 填充至32位；
对于signed char，进行符号位扩展。如果其符号位为0，则左边的高位用 0 填充至32位；如果其符号位为1，则左边的高位用 1 填充至32位。

# 尽管不像非嵌入式计算机那么常见，嵌入式系统还是有从堆（heap）中动态分配内存的过程的。那么嵌入式系统中，动态分配内存可能发生的问题是什么？

解答：动态分配将不可避免会产生问题：

内存泄露：内存泄露通常是程序自身编码缺陷造成，常见的 malloc内存后没有free等类似的操作， 系统在运行过程当中反复的malloc，吃掉系统内存，造成内核OOM，将某个进程需要申请内存的杀死而退出。
内存碎片：内存碎片是一个系统问题，反复的malloc和 free，而free后的内存又不能马上被系统回收利用。这个是因为负责动态分配内存的分配算法使得这些空闲的内存无法使用，这一问题的发生，原因在于这些空闲内存以小且不连续方式出现在不同的位置。



