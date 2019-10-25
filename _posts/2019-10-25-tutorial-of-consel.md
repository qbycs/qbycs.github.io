---
type: page
title: Consel教程
tags: 系统发育
key: tutorial-of-consel
---

## 1. 简介

​	系统发育是一种历史教程，任何基于分子数据集得到的发育树都是对真实系统发生的推测。一个合理地假设，总是应该接收来自各种证据的检验。

​	系统发育假设检验（phylogenetic hypothesis testing）是用**统计学方法检验两个或多个不同发育树的差异是否有统计学上的显著性**。系统发育检验需要数据集、模型、两棵以上的发育树。已有有大量的检验方法，主要包括频率检验或者贝叶斯检验。一般来说，检验方法包括Approximately unbiased test，Approximate Bayesian posterior probability test，bootstrap probability test，Kishino-Hasegawa test，weighted Kishino-Hasegawa test，Shimodaira-Hasegawa test和weighted Shimodaira-Hasegawa test等。常用的为**Approximately unbiased test (AU)和Kishino-Hasegawa test (KH)**。
<!--more-->

> 黄原. (2012). 分子系统发生学. 科学出版社. pp 381-393.

​	多个软件都可以用于执行这种检验，如 PAUP，TREE-PUZZLE等。此处，我们介绍consel 01j.

> Shimodaira, H., & Hasegawa, M. (2001). CONSEL: for assessing the confidence of phylogenetic tree selection. *Bioinformatics*, *17*(12), 1246-1247.

## 2. 数据准备

​	输入文件是一个包含**各位点对数似然值** (per site log-likelihood)的文本，该文本可以直接来自与常用的系统发育软件。此处以RXaML-master 8.2.0 为例。

​	此处与常用的快速自展分析(-f a)不同，计算各位点对数似然值需要在 -f G (g)进行，同时仍需要fas文件和一个包含不同拓扑结构的文本文件。

​	具体命令如下：

```
raxmlHPC -s consel.fas -m GTRGAMMA -f G -z trees.txt -n puzzle
```

​	注：计算per site log-likelihood时，RXaML并不支持GTRCAT模型，仅GTRGAMMA被支持。

​	包含不同拓扑结构的文本通过 -z参数输入，具体格式如下：

``` 
((1,(2,3)),4,(5,6));
(1,4,((2,3),(5,6)));
(1,((2,3),4),(5,6));
(1,(4,5),((2,3),6));
((1,(2,3)),(4,5),6);
(1,((2,3),(4,5)),6);
```

​	RXaML运行结束后会直接生成一个puzzle格式的文件，其中记录了per site log-likelihood.

## 3. 系统发育检验

​	系统发育检测在consel中完成。

### 3.1 consel的安装和运行

​	consel的安装和运行基本和RXaML-master一致，该软件并没有运行界面。将下载好的consel安装包解压后放置C盘桌面。然后打开cmd，输入cd+consel文件夹所在路径。注意路径应直接转到bin文件夹下。

``` 
C:\Users\zz> cd C:\Users\zz\Desktop\consel 01j\bin

C:\Users\zz\Desktop\consel 01j\bin>
```

​	此处已设置好运行环境，将puzzle文件拷入到 ...\bin\ 下后即可开始运算。

### 3.2 系统发育检测

#### 3.2.1 读取puzzle文件

```
C:\Users\zz\Desktop\consel 01j\bin> seqmt --puzzle consel.puzzle

# $Id: seqmt.c,v 1.5 2007/03/24 00:57:18 shimo Exp $
# reading consel.puzzle
# M:5 N:1906
# writing consel.mt
```

#### 3.2.2 生成rmt文件

```
C:\Users\zz\Desktop\consel 01j\bin>makermt --puzzle consel.puzzle
# $Id: makermt.c,v 1.15 2007/03/24 00:57:22 shimo Exp $
# seed:0 (MT19937 generator)
# K:10
# R:0.5 0.6 0.7 0.8 0.9 1 1.1 1.2 1.3 1.4
# B:10000 10000 10000 10000 10000 10000 10000 10000 10000 10000
# reading consel.puzzle
# M:5 N:1906
# writing consel.vt
# writing consel.rmt
# start generating total 100000 replicates for 5 items..........
# time elapsed for bootstrap t=9.658 sec
# exit normally
```

​	此步骤可能较慢，需耐心等待。

#### 3.2.3 进行系统发育检验 

​	结果记录在.pv文件中。

```
C:\Users\zz\Desktop\consel 01j\bin> consel consel.rmt
# $Id: consel.c,v 1.19 2004/11/11 08:14:09 shimo Exp $
# reading consel.rmt..........
# K:10
# R:0.5 0.599685 0.699895 0.79958 0.89979 1 1.09969 1.1999 1.29958 1.39979
# B:10000 10000 10000 10000 10000 10000 10000 10000 10000 10000
# M:5
# generate the identity association
# CM:5
# MC-TEST STARTS
# centering the replicates
# calculating kh-pvalue.....
# calculating mc-pvalue.....
# calculating the variances.....
# calculating weighted kh-pvalue.....
# calculating weighted mc-pvalue.....
# MC-TEST DONE
# calculate replicates of the statistics..........
# BP-TEST STARTS - DONE
# AU-TEST STARTS
# sorting the replicates..........
# calculating approximately unbiased p-values by MLE (fast) fitting.....
# time elapsed for AU test is t=0.015 sec
# ALPHA:0.05 0.1 0.5 0.9 0.95
# calculating confidence intervals.....
# AU-TEST DONE
# writing consel.pv
# writing consel.ci
# exit normally

```

#### 3.2.4 结果可视化

```
C:\Users\zz\Desktop\consel 01j\bin>catpv consel.pv

# reading consel.pv
# rank item    obs     au     np |     bp     pp     kh     sh    wkh    wsh |
#    1    1  -12.7  0.957  0.911 |  0.911  1.000  0.910  0.982  0.910  0.995 |
#    2    4   12.7  0.114  0.064 |  0.065 3e-006  0.090  0.452  0.090  0.272 |
#    3    5   21.6  0.035  0.021 |  0.022 4e-010  0.043  0.292  0.043  0.113 |
#    4    3   27.7  0.003  0.003 |  0.003 9e-013  0.021  0.200  0.021  0.056 |
#    5    2  203.6 7e-007 5e-006 |      0 4e-089      0      0      0      0 |
```

​	此结果即为文献中展示的结果。

### 4. 结果解读

​	结果的解释涉及到对p值的理解，我也不懂......

​	开个玩笑，不懂当然是不懂，然而我还是尝试去理解一下。每个p值代表当前数据集对某一拓扑结构在该种test下的支持程度，p值越高，当前拓扑结构的可靠性就越大。**如果p值<0.05，则说明该拓扑结构被显著拒绝。**(当然严格来说，p值>0.05时，一般不认为不同高低的p值对应不同的支持程度。)

​	有关p值的解释和讨论见于下述链接：

​	https://www.zhihu.com/question/21195469

​	https://en.wikipedia.org/wiki/P-value

