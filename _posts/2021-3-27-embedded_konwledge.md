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
