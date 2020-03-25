---
layout:     post
title:      如何确定QTableView中数据来自那个视图
subtitle:   
date:       2019-11-15
author:     HB
header-img: img/post-bg-qtques.jpg
catalog: true
tags:
    - QT
---
## 如何确定QTableView中数据来自那个视图
### 问题描述:

  #### 在我的MySQL数据库中我创建了三个视图,通过如下代码指定和加载要使用的视图到QTableView中去.
```c++
        QSqlTableModel *model_b;

        QSqlTableModel *model_d;

        QSqlTableModel *model_lungCancer;

        MainWindow::MainWindow(QWidget *parent) :


        QMainWindow(parent),


        ui(new Ui::MainWindow)


    {


        ui->setupUi(this);


        this->resize(1000,750);


        initMainWindow();


        model_b = new QSqlTableModel(this);


        model_b->setTable("basic_inf");指定要访问的视图名


        model_b->select();//加载视图数据


        model_d = new QSqlTableModel(this);


        model_d->setTable("details_inf");


        model_d->select();


        ui->basicTableView->setModel(model_b);


        onTableSelectChange(0);


    }

```
  ####  然后在我的QTableView中如何判断传进来的是哪一个视图呢?

#### 尝试的解决办法

  - 因为QAbstractItemModel是QSqlTableModel的父类,

```c++

        const QAbstractItemModel *model;//定义model
        model = ui->basicTableView->currentIndex().model();

        QModelIndex index;

        index = model->index(r,1);//这里的model是上文中定义的model,但其类型为QSqlTableModel

        ui->nameLabel->setText(model->data(index).toString());

```
- 运行程序发现程序崩溃,查看model()函数

> const QAbstractItemModel *QModelIndex::model() const

####    Returns a pointer to the model containing the item that this index refers to. A const pointer to the model is returned because calls to non-const functions of the model might invalidate the model index and possibly crash your application.


  #### 从提示来看我们应该是调用了model 的non_const 函数,导致程序崩溃.但不明白应该如何修改,或者这个思路错了.


#### 解决办法

```c++

    void  MainWindow::on_basicTreeWidget_clicked(QTreeWidgetItem *item, int column)

    {

       QTreeWidget *treewidget = ui->treeWidget;

       QList<QTreeWidgetItem*> canceritem;

       canceritem = treewidget->findItems("肺癌",Qt::MatchFlags(Qt::MatchContains|Qt::MatchRecursive),0);

       if(item == canceritem[0])

       {

           model->setTable("lungcancer_inf");

           model->select();

           ui->basicTableView->setModel(model);

       }

    }
```

####   使用这个思路即不去通过onTableSelectChange()函数来获取当前的model来自哪个视图,而是通过将变量 QSqlTableModel *model 中的model指针再次赋值使视图信息被更新.从而不需要去改变onTableSelectChange()函数实现这个功能,并且程序易于更新和维护.
