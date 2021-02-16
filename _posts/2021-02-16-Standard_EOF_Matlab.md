---
layout: post
title: Matlab做EOF分析
date: 2021-02-16
categories: blog
description: 
tags: [Software, EOF, Matlab]
header-img: img/top.png    #这篇文章标题背景图片
---

## 用MATLAB做EOF分析

以之前NCL中的例子为基础 => [点击这里](https://cryoecnu.github.io/blog/2021/02/14/Standard_EOF/)

原数据文件做了计算，只留下这个例子计算实际用到的数据：<a href="/zips/slp05.nc"><span style="color:blue">下载</span></a>

原NCL脚本也做了简化修改：<a href="/zips/eof_1.ncl"><span style="color:blue">下载</span></a>

NCL结果：

<center>
<p><img src="/img/eof_test.000001_20210216.png" align="center"></p>
</center>

<center>
<p><img src="/img/eof_test.000002_20210216.png" align="center"></p>
</center>

这些计算结果用来比对MATLAB计算的结果，进一步确保MATLAB的计算程序是对的。

-----

编写了一个计算EOF的函数：<span style="color:red">EOF_CALCULATE.m</span>，基本上就是把NCL的计算翻译过来了。输入变量是一个3D的场数据，两个1D的经纬度数据。

```Matlab
clc; close all; clear;

filename = 'slp05.nc';

lat = ncread(filename,'lat'); lat = double(lat);
lon = ncread(filename,'lon'); lon = double(lon);
data = ncread(filename,'slp');
time = 1979:2003;

[eof0, pc, percent_variance] = EOF_CALCULATE( data, lat, lon );

figure1=figure;

plot_eof(lat, lon, eof0(:,:,1))

figure2=figure;

ttt = pc(:,1);

bar(time(ttt>0), ttt(ttt>0),'r');
hold on
bar(time(ttt<0), ttt(ttt<0),'b');

ylim([-0.15, 0.15]);

xlim([1978.5,2003.5]);

xticks(1979:5:2003);
title(['Variance=',num2str(round(percent_variance(1),1)),'%']);

ax = gca;
ax.TitleHorizontalAlignment = 'right';

saveas(figure1,'eof_matlab1_20210216.png');
saveas(figure2,'eof_matlab2_20210216.png');

function plot_eof(lat, lon, eof0)

axesm('eqdcylin', ...
    'maplatlimit',[25,80], ...
    'maplonlimit',[-70, 40],...
    'meridianlabel','on', 'parallellabel','on',...
    'mlinelocation',-180:30:180, 'plinelocation',-90:30:90,...
    'labelrotation','on');

contourfm(lat, lon, eof0',-0.05:0.01:0.05);

colormap jet

contourcbar

caxis([-0.05 0.05])

% clabelm(C,h)

axis off;
framem on;
gridm on;
load coastlines coastlat coastlon
plotm(coastlat,coastlon,'k')

tightmap
end
```
Matlab 计算的结果：

<center>
<p><img src="/img/eof_matlab1_20210216.png" align="center"></p>
</center>

<center>
<p><img src="/img/eof_matlab2_20210216.png" align="center"></p>
</center>

与NCL比较结果显示，应该是重现了NCL的EOF计算过程，不管是空间模态、时间序列、或者是解释方差。

-------

## 相关参考资料

[<span style="color:red">**EOF in IDL**</span>](http://www.idlcoyote.com/code_tips/eof_analysis.html), 不光是解释如何用IDL做EOF分析，也很仔细地解释了计算过程。

Daniel Wilks 的 [<span style="color:red">**Statistical Methods in the Atmospheric Sciences**</span>](https://www.elsevier.com/books/statistical-methods-in-the-atmospheric-sciences/wilks/978-0-12-815823-4)，最新版应该是2019年的第四版。

Daniel Wilks 的第三版有中文译本：[<span style="color:red">**大气科学中的统计方法**</span>](https://item.jd.com/12403725.html).