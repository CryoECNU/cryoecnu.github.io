---
layout: post
title: 下一代空间建模环境（SME）
date: 2021-02-12
categories: blog
description: 
tags: [SME]
header-img: img/top.png    #这篇文章标题背景图片
---

## 啥玩意是空间建模环境（SME）

SME是建立集成生态经济模型的有效工具。

<center>
<p><img src="/img/Eco-Eco.gif" align="center"></p>
</center>

实现的具体方法是采用模块化建模方法，将模型结构分解为界面友好、图标化的独立模块集合，并通过公共的模型代码转换器，实现模型代码公用性。

SME的最大优点就是模块化。
SME的架构主要分为三大部分：

1. 单元模型开发
2. 代码转换
3. 代码空间分配

<center>
<p><img src="/img/WeCom20210212-233436@2x.png" align="center"></p>
</center>

简单而言：

建模人员利用STELLA等可视化系统动力学建模软件，构建单个单元格上的模型和接口；然后SME的代码转换功能可以将建模人员建立的单元格模型转成编程语言；然后再将单元格代码分发到所有网格上。

<center>
<p><img src="/img/HabsAndStella.gif" align="center"></p>
</center>

## 下一代SME？

这个SME的概念和整体框架设计都是相对比较好而且也比较有前瞻性的，尽管在整个建模中依然存在比较困难的环节（比如行为设定等），但已经极大简化了一般建模人员的工作量。理想状态下，一般建模工作只是需要在STELLA中构建单元格模型。复杂些的应用则还需要修改或增加新的函数去实现所需功能。

总体来说，对于人-地耦合建模，SME有独特的优势。

然而，二十多年过去了，也再没有更新过。目前的新CPU架构、新编译器、新JAVA等等，都已经不再能满足SME的使用了。当然，并不是完全不可以用，美国还是有些机构依然在使用SME构建的模型，但是他们是基本上脱离了最关键的建模人员-单元模型这一环节。

可能需要在原有SME的框架上，对其进行升级改造。一方面可能是测试比较新的编译器；另一方面可能是移植很多功能到Python平台上去，估计能极大的简化模型内置转换器和分发的代码实现。

这个想法跟SME的主要作者沟通过，基本上只是技术层面的工作，所以，能找到一两个计算机专业的、再有经费支持上一年半载的应该就差不多。

## 相关书籍

《Landscape simulation modeling: a spatially explicit, dynamic approach》: [<span style="color:red">**Link!**</span>](https://link.springer.com/book/10.1007/b97268)

有中文译本，翻译质量是很好了的。
《景观模拟模型：空间显式的动态方法》：[<span style="color:red">**Link!**</span>](https://baike.baidu.com/item/%E6%99%AF%E8%A7%82%E6%A8%A1%E6%8B%9F%E6%A8%A1%E5%9E%8B%EF%BC%9A%E7%A9%BA%E9%97%B4%E6%98%BE%E5%BC%8F%E7%9A%84%E5%8A%A8%E6%80%81%E6%96%B9%E6%B3%95)

《Systems Science and Modeling for Ecological Economics》：[<span style="color:red">**Link!**</span>](https://www.elsevier.com/books/systems-science-and-modeling-for-ecological-economics/voinov/978-0-12-372583-7)

也有中文译本，尚未读过，不好评判。《生态经济学中的系统分析与模拟》：[<span style="color:red">**Link!**</span>](http://www.hep.com.cn/book/details?uuid=80eeb3ac-1460-1000-bc2a-3fafc67de19c)