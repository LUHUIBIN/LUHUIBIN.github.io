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
状态机由状态寄存器和组合逻辑电路构成，能够根据控制信号按照预先设定的状态进行状态转移，是协调相关信号动作、完成特定操作的控制中心。有限状态机简写为FSM（Finite State Machine），主要分为2大类：
***第一类，若输出只和状态有关而与输入无关，则称为Moore状态机
第二类，输出不仅和状态有关而且和输入有关系，则称为Mealy状态机***

## 基本信息
状态机由状态寄存器和组合逻辑电路构成，能够根据控制信号按照预先设定的状态进行状态转移，是协调相关信号动作,完成特定操作的控制中心。状态机分为摩尔（Moore）型状态机和米莉（Mealy）型状态机。 [1] 
状态机就是状态转移图。举个最简单的例子，人有三个状态：健康，感冒，康复中。触发的条件有淋雨（t1），吃药（t2），打针（t3），休息（t4）。所以状态机就是健康-（t4）->健康；健康-（t1）->感冒；感冒-（t3）->健康；感冒-（t2）->康复中；康复中-（t4）->健康，等等。就是这样状态在不同的条件下跳转到自己或不同状态的图。

# GDB调试
[GDB调试指南守望的个人博客](https://www.yanbinghu.com/2019/04/20/41283.html "GDB调试指南")



# 堆和栈的区别是什么

1.管理方式:
对于栈来讲,是由编译自动管理,无需我们手工控制;对于堆来说,释放工作由程序员控制,容易产生内存泄漏.
2.申请大小:
栈:在Windows下,栈是向低地址扩展的数据结构,是一块连续的内存区域.就是栈顶的地址和栈的最大容量是系统预先规定好的,在windows下,栈的大小为2m(也有说1m,总之是一个编译时就确定的常数),如果申请的空间超过栈的剩余空间时,将提示overflow.因此能从栈获得的空间较小.
堆:堆是向高地址扩展的数据结构,是不连续的内存区域.这是由于系统是用链表来存储的空闲内存地址,自然是不连续的,而链表的遍历方向是由低地址向高地址.堆得大小受限于计算机系统中有效的虚拟内存.由此可见,堆获得的空间比较灵活,也比较大.
3.碎片问题:
对于堆来讲,频繁的new/delete势必会造成内存空间的不连续,从而造成大量的碎片,使程序效率降低.对于栈来讲,则不会存在这个问题,因为栈是先进后出的队列,他们是如此的--对应,以至于永远都不可能有一个内存块从栈中间弹出.
4.分配方式:
堆都是动态分配的,没有静态分配的堆.栈有两种分配方式:静态分配和动态分配.静态分配是编译器完成的,比如局部变量的分配.动态分配由alloc函数进行分配,但是栈的动态分配和堆是不同的,他的动态分配是由编译器进行释放,无需我们手工实现.
5.分配效率:
栈是机器系统提供的数据结构,计算机会在底层对栈提供支持:分配专门的寄存器存放栈的地址,压栈出栈都有专门的指令执行,这就决定了栈的效率比较高.堆则是c/c++函数提供的,他的机制很复杂.

# malloc()与 alloc()区别
C语言跟内存 分配方式
（ 1） 从静态存储区域分配。内存在程序编译的时候就已经分配好，这块内存在程序的整个运行期间都存在。例如全局变量，static变量。
（ 2） 在栈上创建。在执行函数时，函数内局部变量的存储单元都可以在栈上创建，函数执行结束时这些存储单元自动被释放。栈内存分配运算内置于处理器的指令集中，效率很高，但是分配的内存容量有限。
（ 3 ） 从堆上分配，亦称动态内存分配。程序在运行的时候用 malloc 或 new 申请任意多少的内存，程序员自己负责在何时用 free 或 delete 释放内存。动态内存的生存期由我们决定，使用非常灵活，但问题也最多
C语言跟内存申请相关的函数主要有 alloca,calloc,malloc,free,realloc,sbrk等.
alloca是向栈申请内存,因此无需释放。
malloc 分配的内存是位于 堆中 的,并且没有 初始化内存的内容 ,因此基本上malloc之后,调用函数memset来初始化这部分的内存空间,需要用 Free 方式释放空间.
calloc则将初始化malloc这部分的内存,设置为0. 
realloc则对malloc申请的内存进行大小的调整.
free将malloc申请的内存最终需要通过该函数进行释放. 
sbrk则是增加数据段的大小;


# **FreeRTOS**

是一个热门的[[1]](https://zh.wikipedia.org/zh-cn/FreeRTOS#cite_note-EETimes2012-1)[嵌入式设备](https://zh.wikipedia.org/wiki/%E5%B5%8C%E5%85%A5%E5%BC%8F%E8%A3%9D%E7%BD%AE "嵌入式设备")用[即时操作系统](https://zh.wikipedia.org/wiki/%E5%8D%B3%E6%99%82%E4%BD%9C%E6%A5%AD%E7%B3%BB%E7%B5%B1 "即时操作系统")核心[[2]](https://zh.wikipedia.org/zh-cn/FreeRTOS#cite_note-2)[[3]](https://zh.wikipedia.org/zh-cn/FreeRTOS#cite_note-3)，它于2003年由Richard Barry设计，并已被经成功移植到35种不同的[微控制器](https://zh.wikipedia.org/wiki/%E5%BE%AE%E6%8E%A7%E5%88%B6%E5%99%A8 "微控制器")上[[4]](https://zh.wikipedia.org/zh-cn/FreeRTOS#cite_note-Official_Website-4)。FreeRTOS采用[MIT许可证](https://zh.wikipedia.org/wiki/MIT%E8%AE%B8%E5%8F%AF%E8%AF%81 "MIT许可证")许可。

FreeRTOS的设计小巧且简易，整个核心代码只有3到4个C文件，为了让代码容易阅读、移植和维护，大部分的代码都是以[C语言](https://zh.wikipedia.org/wiki/C%E8%AA%9E%E8%A8%80 "C语言")编写，只有一些函数（多数是架构特定排班副程序）采用[汇编语言](https://zh.wikipedia.org/wiki/%E7%B5%84%E5%90%88%E8%AA%9E%E8%A8%80 "汇编语言")编写。

FreeRTOS提供许多方法以实现多[线程](https://zh.wikipedia.org/wiki/%E7%BA%BF%E7%A8%8B "线程")（threads）、多[作业](https://zh.wikipedia.org/wiki/%E4%BD%9C%E6%A5%AD_(%E9%9B%BB%E8%85%A6)) "作业 (电脑)")（task）、[互斥锁](https://zh.wikipedia.org/wiki/%E4%BA%92%E6%96%A5%E9%94%81 "互斥锁")（mutex）、[信号量](https://zh.wikipedia.org/wiki/%E4%BF%A1%E8%99%9F%E6%A8%99 "信号标")（semaphore）和[软件计时器](https://zh.wikipedia.org/wiki/%E8%BB%9F%E9%AB%94%E8%A8%88%E6%99%82%E5%99%A8 "软件计时器")（software timer），有个为低耗电应用程序提供的[无嘀嗒](https://zh.wikipedia.org/wiki/%E6%97%A0%E5%98%80%E5%97%92%E5%86%85%E6%A0%B8 "无嘀嗒内核")（tick-less）模式，线程的优先权管理也有支持，此外，FreeRTOS提供了四种存储器配置的模式：

* 仅配置（allocate only）
* 以非常简易但快速的算法进行配置与释放
* 搭配[存储器合并](https://zh.wikipedia.org/w/index.php?title=%E8%A8%98%E6%86%B6%E9%AB%94%E5%90%88%E4%BD%B5&action=edit&redlink=1)，以较复杂但快速的算法进行配置与释放
* 搭配互斥保护，以 C 库配置进行配置与释放

FreeRTOS中没有一些像[Linux](https://zh.wikipedia.org/wiki/Linux "Linux")、[Microsoft Windows](https://zh.wikipedia.org/wiki/Microsoft_Windows "Microsoft Windows")等典型操作系统具有的先进特征，例如[设备驱动程序](https://zh.wikipedia.org/w/index.php?title=%E8%A3%9D%E7%BD%AE%E9%A9%85%E5%8B%95%E7%A8%8B%E5%BC%8F&action=edit&redlink=1)、先进[存储器管理](https://zh.wikipedia.org/wiki/%E8%A8%98%E6%86%B6%E9%AB%94%E7%AE%A1%E7%90%86 "存储器管理")机制、用户管理和网络管理，FreeRTOS着重在运行的简洁与速度，FreeRTOS有时会被视为是一个‘线程库’而非‘操作系统’，尽管可以找到[命令行接口](https://zh.wikipedia.org/wiki/%E5%91%BD%E4%BB%A4%E5%88%97%E4%BB%8B%E9%9D%A2 "命令行接口")和类似[POSIX](https://zh.wikipedia.org/wiki/POSIX "POSIX") I/O 接口的插件。

FreeRTOS实现了多线程，主程序会在规律的短时间区间内调用一个线程时计方法，这个方法会以[循环制](https://zh.wikipedia.org/wiki/%E5%BE%AA%E7%92%B0%E5%88%B6 "循环制")依照任务的优先级进行任务切换，一般来说，这个短时间区间介于 1/1000 秒与 1/100 秒之间，透过一个硬件时计中断来计时，但这个区间经常随着特定的应用而改变。

从FreeRTOS官网（[FreeRTOS.org](http://www.freertos.org/)（[页面存档备份](https://web.archive.org/web/20160815221433/http://www.freertos.org/)，存于[互联网档案馆](https://zh.wikipedia.org/wiki/%E4%BA%92%E8%81%94%E7%BD%91%E6%A1%A3%E6%A1%88%E9%A6%86 "互联网档案馆")））所下载到的代码包含准备用来移植或编译的配置文件和演示代码，让用户可以快速地进行应用程序设计。

## 主要特色

* 存储器足迹非常小，低[负担](https://zh.wikipedia.org/w/index.php?title=%E8%B2%A0%E6%93%94_(%E8%A8%88%E7%AE%97)&action=edit&redlink=1)（overhead）且运行非常快速
* 提供低电耗应用程序无计时选项
* 对操作系统新手而言，很适合作为入门教材，对于专业开发者来说则适合用于商业产品开发
* [调度器](https://zh.wikipedia.org/wiki/%E6%8E%92%E7%A8%8B%E5%99%A8 "调度器")可以设置成[可抢先](https://zh.wikipedia.org/wiki/%E6%8A%A2%E5%8D%A0%E5%BC%8F%E5%A4%9A%E4%BB%BB%E5%8A%A1%E5%A4%84%E7%90%86 "抢占式多任务处理")（preemptive）或[共同运作](https://zh.wikipedia.org/w/index.php?title=%E5%8D%8F%E4%BD%9C%E5%BC%8F%E5%A4%9A%E4%BB%BB%E5%8A%A1%E5%A4%84%E7%90%86&action=edit&redlink=1)（cooperative operation）
* 提供[共享副程序](https://zh.wikipedia.org/wiki/%E5%8D%8F%E7%A8%8B "协程")（coroutine），在FreeRTOS中，共享副程序是一个存储器[堆栈](https://zh.wikipedia.org/wiki/%E5%91%BC%E5%8F%AB%E5%A0%86%E7%96%8A "调用堆栈")用量非常有限但非常简易轻巧的[任务](https://zh.wikipedia.org/wiki/%E4%BD%9C%E6%A5%AD_(%E9%9B%BB%E8%85%A6)) "作业 (电脑)")
* 支持使用（generic[trace macros](http://www.freertos.org/index.html?http://www.freertos.org/rtos-trace-macros.html)（[页面存档备份](https://web.archive.org/web/20200802115843/http://www.freertos.org/index.html?http%3A%2F%2Fwww.freertos.org%2Frtos-trace-macros.html)，存于[互联网档案馆](https://zh.wikipedia.org/wiki/%E4%BA%92%E8%81%94%E7%BD%91%E6%A1%A3%E6%A1%88%E9%A6%86 "互联网档案馆")）. ）

---

# 实时操作系统

**实时操作系统**（Real-time operating system, RTOS），又稱**即时操作系统**，它會按照排序執行、管理系統資源，並為開發應用程式提供一致的基礎。

实时操作系统与一般的[操作系统](https://zh.wikipedia.org/wiki/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F "操作系统")相比，最大的特色就是「[实时性](https://zh.wikipedia.org/wiki/%E5%AE%9E%E6%97%B6%E8%AE%A1%E7%AE%97 "实时计算")」[[1]](https://zh.wikipedia.org/wiki/%E5%AE%9E%E6%97%B6%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F#cite_note-1)，如果有一个任务需要执行，实时操作系统会马上（在较短时间内）执行该任务，不会有较长的延时。这种特性保证了各个任务的及时执行。

设计实时操作系统的首要目标不是高的[吞吐量](https://zh.wikipedia.org/wiki/%E5%90%9E%E5%90%90%E9%87%8F "吞吐量")，而是保证任务在特定时间内完成，因此衡量一个实时操作系统坚固性的重要指标，是系统从接收一个任务，到完成该任务所需的时间，其时间的变化称为[抖动](https://zh.wikipedia.org/wiki/%E5%AE%9E%E6%97%B6%E8%AE%A1%E7%AE%97 "实时计算")。可以依抖动將实时操作系统分為兩種：硬实时操作系统及软实时操作系统，硬实时操作系统比软实时操作系统有更少的抖动：

* 硬实时操作系统**必须**使任务在确定的时间内完成。
* 软实时操作系统能让**绝大多数**任务在确定时间内完成。[[2]](https://zh.wikipedia.org/wiki/%E5%AE%9E%E6%97%B6%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F#cite_note-2)

实时操作系统与一般的操作系统有着不同的[调度](https://zh.wikipedia.org/wiki/%E6%8E%92%E7%A8%8B "排程")算法。普通的操作系统的调度器对于线程优先级等方面的处理更加灵活；而实时操作系统追求最小的[中断延时](https://zh.wikipedia.org/w/index.php?title=%E4%B8%AD%E6%96%AD%E5%BB%B6%E6%97%B6&action=edit&redlink=1)和[线程切换延时](https://zh.wikipedia.org/wiki/%E4%B8%8A%E4%B8%8B%E6%96%87%E4%BA%A4%E6%8F%9B "上下文交換")。[[3]](https://zh.wikipedia.org/wiki/%E5%AE%9E%E6%97%B6%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F#cite_note-3)

通常都會有最基礎的[內核](https://zh.wikipedia.org/wiki/%E5%86%85%E6%A0%B8 "内核")，以及外加上去的模組，像是[檔案系統](https://zh.wikipedia.org/wiki/%E6%AA%94%E6%A1%88%E7%B3%BB%E7%B5%B1 "檔案系統")、[網路協定堆疊](https://zh.wikipedia.org/wiki/%E7%B6%B2%E8%B7%AF%E5%8D%94%E5%AE%9A%E5%A0%86%E7%96%8A "網路協定堆疊")和應用、裝置驅動程式等模組。

RTOS的內核通常會有：[排程器](https://zh.wikipedia.org/wiki/%E6%8E%92%E7%A8%8B%E5%99%A8 "排程器")、[物件](https://zh.wikipedia.org/wiki/%E7%89%A9%E4%BB%B6_(%E9%9B%BB%E8%85%A6%E7%A7%91%E5%AD%B8)) "物件 (電腦科學)")、[服务](https://zh.wikipedia.org/wiki/%E6%9C%8D%E5%8A%A1 "服务")

## 设计理念

通常，实时操作系统分为两大类:

* 事件驱动型。当一个高优先级的任务需要执行时，系统会自动[切换](https://zh.wikipedia.org/wiki/%E4%B8%8A%E4%B8%8B%E6%96%87%E4%BA%A4%E6%8F%9B "上下文交換")到这个任务。这种根据优先级调度任务的方式称为[抢占式任务处理](https://zh.wikipedia.org/wiki/%E6%8A%A2%E5%8D%A0%E5%BC%8F%E4%BB%BB%E5%8A%A1%E5%A4%84%E7%90%86 "抢占式任务处理")。
* 时间触发型。每个任务在各自设定好的的时间间隔内重复、轮流调度。

时间触发型设计往往比较严格地调度任务，具有更好的[多任务处理](https://zh.wikipedia.org/wiki/%E5%A4%9A%E4%BB%BB%E5%8A%A1%E5%A4%84%E7%90%86 "多任务处理")能力。多个任务被不停地轮流调度，在宏观上，就相当于一个[CPU](https://zh.wikipedia.org/wiki/CPU "CPU")同时执行多个任务。

在过去，CPU在切换任务时往往需要多个[机器周期](https://zh.wikipedia.org/wiki/%E6%9C%BA%E5%99%A8%E5%91%A8%E6%9C%9F "机器周期")，在这段时间内，CPU不能处理其他任何任务。例如，一个20 MHz的[摩托罗拉68000](https://zh.wikipedia.org/wiki/%E6%91%A9%E6%89%98%E7%BD%97%E6%8B%8968000 "摩托罗拉68000")处理器（1980年代后期），在切换任务时需要花费20微秒。（相比之下，一个100 MHz的[ARM架构](https://zh.wikipedia.org/wiki/ARM%E6%9E%B6%E6%9E%84 "ARM架构")的处理器（2008年之后的）只需要3微秒。）[[4]](https://zh.wikipedia.org/wiki/%E5%AE%9E%E6%97%B6%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F#cite_note-4)[[5]](https://zh.wikipedia.org/wiki/%E5%AE%9E%E6%97%B6%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F#cite_note-5)因此，早期的实时操作系统通过减少任务切换次数来避免消耗过多CPU时间。

## 任务调度

在典型的设计中[[來源請求]](https://zh.wikipedia.org/wiki/Wikipedia:%E5%88%97%E6%98%8E%E6%9D%A5%E6%BA%90 "Wikipedia:列明来源")，一个任务有以下三种状态：

1. 正在运行（Running，正在CPU中执行）
2. 待命（Ready，等待执行）
3. 阻塞（Blocked，任务暂停，等待一个事件的发生，例如接收一组数据）

由于CPU在某个时间只能执行一个任务，大部分任务，在大部分时间，处于阻塞或待命状态。可能会有大量项目在待命列表里等待执行，这取决于系统所需的任务数量以及调度器的类型。

通常情况下，对于简单的时间触发式调度器来说，待命任务列表的数据结构的设计要尽可能缩短最坏情况下，程序在调度器关键部分的执行时间，以防止其他任务一直在待命列表中，无法及时执行。因此，在这种调度器中，应尽可能避免抢占式任务，甚至应该关闭调度器之外的所有中断。当然，待命任务列表的数据结构也应根据这个系统需要的最大任务数量做进一步的优化。

如果待命任务列表中的任务较多，[双向链表](https://zh.wikipedia.org/wiki/%E5%8F%8C%E5%90%91%E9%93%BE%E8%A1%A8 "双向链表")是一个比较好的选择。如果待命任务列表通常包含少量任务，但偶尔会出现较多任务，任务应该根据优先级排序。这样一来，要寻找最高优先级的任务，就不必要在整个列表中一个一个地寻找。而插入任务需要从列表中的第一个任务开始，向后寻找，直到找到比要插入的任务优先级低的任务，然后插入到该任务之前；如果没有找到优先级更低的任务，就插入到任务列表末尾。

在寻找任务列表，准备插入任务的过程中，应该注意避免抢占。长的关键部分应分为多个小的部分分别执行。如果在寻找任务列表，要插入低优先级任务的时候，一个中断发生使高优先级任务进入待命状态，高优先级任务应该在低优先级任务被插入之前立刻被插入列表和执行。

在更先进的系统中，实时任务和许多非实时任务共享运算资源，这时候待命任务列表会变得很长。在这种系统中，待命任务列表可能不适合用链表的结构。

### 排程算法

一些实时操作系统中常用的算法：

* 合作式调度
* [抢占式调度](https://zh.wikipedia.org/wiki/%E6%8A%A2%E5%8D%A0%E5%BC%8F%E5%A4%9A%E4%BB%BB%E5%8A%A1%E5%A4%84%E7%90%86 "抢占式多任务处理")
  
  * [Rate-monotonic scheduling](https://zh.wikipedia.org/w/index.php?title=Rate-monotonic_scheduling&action=edit&redlink=1 "Rate-monotonic scheduling（页面不存在）")
  * [Round-robin scheduling](https://zh.wikipedia.org/wiki/Round-robin_scheduling "Round-robin scheduling")
  * [Fixed priority pre-emptive scheduling](https://zh.wikipedia.org/w/index.php?title=Fixed_priority_pre-emptive_scheduling&action=edit&redlink=1 "Fixed priority pre-emptive scheduling（页面不存在）"), an implementation of[preemptive time slicing](https://zh.wikipedia.org/w/index.php?title=Preemption_(computing)&action=edit&redlink=1 "Preemption (computing)（页面不存在）")
  * Fixed-Priority Scheduling with Deferred Preemption
  * Fixed-Priority Non-preemptive Scheduling
  * Critical section preemptive scheduling
  * Static time scheduling
* [Earliest Deadline First](https://zh.wikipedia.org/w/index.php?title=Earliest_deadline_first_scheduling&action=edit&redlink=1 "Earliest deadline first scheduling（页面不存在）") approach
* [Stochastic](https://zh.wikipedia.org/w/index.php?title=Stochastic&action=edit&redlink=1 "Stochastic（页面不存在）")[digraph](https://zh.wikipedia.org/w/index.php?title=Directed_graph&action=edit&redlink=1 "Directed graph（页面不存在）")s with[multi-threaded](https://zh.wikipedia.org/wiki/Thread_(computer_science)) "Thread (computer science)")[graph traversal](https://zh.wikipedia.org/w/index.php?title=Tree_traversal&action=edit&redlink=1 "Tree traversal（页面不存在）")

---










