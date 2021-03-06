---
layout: post
title: 使用Excel随机分配固定人数到不同组里
categories: Excel
description: 
keywords: Excel
---

如果我们有手动制作的表，并且需要给学生分配学科，那么如何使用Excel来给学生随机分配呢？  

**目录**

* TOC
{:toc}


## 1. 新建一列随机数
在表格右侧新建公式=RAND()，这是一个从0-1的随机数。  
从第一个学生拉到最后一个学生。  

## 2. 新建分组公式
继续在右侧再新建一列并填写公式。


公式：
```
=ROUNDUP(RANK(D2,$D$2:$D$23)/10,0)
```
![Excel随机分配固定组](/blog/images/posts/2020/20200811_Excel_Randomly_Assign_Groups.png)

从图中可以看出，D2就是我们第一个学生随机数值的行列数，而D23则是我们最后一个学生的行列。
为什么我们不用D2:D23呢，因为那样在下拉过程中，会导致行列变动，所以使用$固定。
在公式中的10，代表的是分组中每个组内成员的数量。  
我们有22个学生，分成2个组，也就是说每组11人。如果我们分成10人一组，那么我们就会产生第三组。  

注：图中第一个学生分组其实是2，但是因为显示原因导致显示是空白。

这个公式中的RANK函数实际上是Office 2007及以前版本，目前其实使用的是RANK.AVG   
也就是：
```
=ROUNDUP(RANK.AVG(D2,$D$2:$D$23)/10,0)
```

## 3. 将整个表复制成数值
将表复制成数值，因为RAND这个函数每次操作都会发生新的变化，所以建议直接复制成数值。

## 非固定分组
我们也可以没有规定的分组
```
=CHOOSE(RANDBETWEEN(1,3),"A","B","C")
```
这代表分成3组，且名字为A/B/C

## 参考文献
1. [ExcelJet](https://exceljet.net/formula/randomly-assign-people-to-groups)
2. <https://www.extendoffice.com/documents/excel/5895-excel-create-random-groups.html#group2>