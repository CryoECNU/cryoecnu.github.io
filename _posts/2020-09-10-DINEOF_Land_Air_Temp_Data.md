---
layout: post
title: Reconstructed global monthly land air temperature dataset (1880–2017)
date: 2020-09-10
categories: blog
description: 
tags: [Climate, Reference, Global, Temperature, EOF, DINEOF]
header-img: img/top.png    #这篇文章标题背景图片
---

**Kang Wang**, Gary D. Clow
(**2020**),
Reconstructed global monthly land air temperature dataset (1880–2017).
**Geoscience Data Journal**:4-12.
[DOI:10.1002/gdj3.84](https://doi.org/10.1002/gdj3.84)

地表气温是理解全球快速环境变化的基本气候变量。 1950年代之前的稀疏网络覆盖可能是全球气候变化评估不确定性的重要来源。
正是认识到空间覆盖的重要性，越来越多的台站被不断添加到全球气候监测网络中。
一个挑战是如何更好地利用新台站观测所引入的新的信息来增进我们对全球气候状况和变化的理解和评估，尤其是对于20世纪中叶之前的这一段时期。
在我们这项研究中，一种基于EOF方法的数据插值技术（DINEOF）被用于从全球历史气候学网络（GHCNm第4版）1880-2017年地面逐月气温的重建。
最终重建的气温数据集覆盖了大约全球陆地表面积的95％，在1880-1900年间将空间覆盖率提高了约80％，自1950年代以来空间覆盖率提高了10-20％。
验证测试表明，重建数据的平均绝对误差小于0.82°C。
与CMIP5输出的比较表明，重建的数据集大大减少了稀疏空间覆盖（尤其是在1950年代之前）引起的全球数据集中的偏差。

<center>
<p><img src="/img/gdj384-fig-0005-m.jpg" align="center"></p>
</center>

**【后记】**
在2017年做GRL那篇工作[<span style="color:red">**【GRL2017】**</span>](https://cryoecnu.github.io/blog/2017/10/30/Continuously_Amplified_Warming_Alaskan_Arctic/)的时候，一个重要的问题是网格资料的原始输入台站数据空间分布不均。后来发现，DINEOF最初用于遥感或者其他空间数据的缺失值插补，我们就想，这个技术是否能够用在时间插补上面。所以就尝试了对全球地面台站的历史资料进行了重建和比对，结果还可以。通过这样的时间插补，能够最大程度的减小早期台站分布不均一的问题，即便很多数据产品采用了各种各样的空间插值方法，我们在这里也列举了CRU的例子。

没曾想，这个小文章第一次的被引用是被Nature Geoscience文章引用的：
Christopher Kadow, David Matthew Hall, Uwe Ulbrich (**2020**), Artificial intelligence reconstructs missing climate information, **Nature Geoscience**: 408-413. [DOI: 10.1038/s41561-020-0582-5](https://doi.org/10.1038/s41561-020-0582-5)