---
layout:     post
title:      Qt5如何实现用户点击QTreeWidget中的某一确定item ,程序跳转到别的窗口部件执行操作.
subtitle:   
date:       2019-11-13
author:     HB
header-img: img/post-bg-qtproblem.jpg
catalog: true
tags:
    - RaspberryPi
---

##  qt5如何实现用户点击QTreeWidget中的某一确定item ,程序跳转到别的窗口部件执行操作.

### 预期功能:

   - 双击肺癌选项,患者信息窗口只显示肺癌病人




#### 实现这个功能的关键:

   - 信号与槽函数
   - 如何取出item中的数据并匹配



**关键代码:**
```c++

   connect( ui->treeWidget,SIGNAL(itemDoubleClicked(QTreeWidgetItem *, int )),this,SLOT( on_basicTreeWidget_clicked( QTreeWidgetItem *, int )));

   void  MainWindow::on_basicTreeWidget_clicked(QTreeWidgetItem *item, int column)

   {

       QTreeWidget *treewigdet = ui->treeWidget;

       QList<QTreeWidgetItem *> canceritem;

       canceritem=treewigdet->findItems("肺癌",Qt::MatchFlags( Qt::MatchContains|Qt::MatchRecursive),0);

       if (item == canceritem[0])

       {

           //要执行的操作

       }

    }
````

**代码分析:**

   在connect 函数中,itemDoubleClicked函数为QTreeWidge Class中内部定义的一个函数.当用户双击item时,这个函数发送信号被on_basicTreeWidget_clicked函数接收.


   在findItems函数中的第二个参数Qt::MatchContains|Qt::MatchRecursive为了保证树中的子节点也可以被搜索到。

```c++   
   QList<QTreeWidgetItem *> QTreeWidget::findItems(const QString &text, Qt::MatchFlags flags, int column = 0) const

   Returns a list of items that match the given text, using the given flags, in the given column.

```
