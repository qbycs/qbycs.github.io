---

type: page
title: 遗传聚类软件BAPS教程
tags: 群体遗传学
key: tutorial-of-BAPS
---

介绍使用BAPS推断群体遗传结构的具体方法。BAPS与STRUCTURE类似，都是基于哈温平衡假设和贝叶斯推断来估算个体的遗传聚类（K）归属。该软件支持多种数据类型，如SSR数据，二元数据以及连锁或者不连锁的gene序列等。相对于STRUCTURE，BAPS运行速度更快且对于居群间的样本量差异不敏感，可作为STRUCTURE遗传聚类分析的补充分析。

<!--more-->

##  1. 数据和软件准备

BAPS有自己的数据格式，参考以下（以最常用的SSR数据为例，其他数据的格式请参考[官方示例数据](http://www.helsinki.fi/bsg/software/BAPS/ExerciseDatasets.zip)）：

```
199	153	165	267	214	205	-9	139	274	128	198	188	249	219	191	246	258	232	1
195	153	169	283	214	205	-9	139	274	128	198	188	249	219	191	246	288	226	1
199	153	169	275	214	205	-9	139	284	128	198	188	249	219	193	246	258	226	1
199	153	169	283	214	205	-9	141	284	128	198	188	249	219	189	234	258	232	1
199	153	169	283	214	205	186	139	274	128	198	188	249	219	193	246	270	226	1
199	155	203	283	216	205	186	139	282	128	198	188	249	219	193	234	286	232	1
203	153	173	273	220	205	184	137	278	126	196	188	259	229	205	246	256	228	2
205	131	175	281	220	205	184	143	288	126	196	188	263	229	199	242	269	228	2
199	131	169	281	220	205	-9	143	278	126	190	188	261	231	199	230	254	228	2
201	133	171	281	220	205	-9	143	288	126	198	188	261	233	205	242	254	240	2
203	153	175	273	220	205	-9	143	278	128	196	188	261	227	205	242	269	228	2
205	131	173	281	220	205	-9	137	288	128	198	188	263	231	199	246	256	228	2
197	151	167	267	218	209	184	151	286	122	196	182	245	223	195	246	256	248	3
197	145	167	275	218	209	184	131	286	128	198	182	253	223	179	252	266	236	3
197	143	167	281	216	209	184	137	286	124	196	184	245	227	195	246	254	236	3
197	143	167	289	216	209	200	137	286	122	196	184	247	223	195	252	252	236	3
```

格式说明：

1.  直接以SSR数据开始，二倍体或多倍体数据以多行显示，行数和倍性一致，缺失数据使用-9代替
2.  居群来源信息（居群信号）位于最后一列
3.  使用tab制表符分隔数据，保存为txt文本格式即可。

BAPS软件可以在[此处](http://www.helsinki.fi/bsg/software/BAPS/)下载。

## 2. 分析过程

打开软件，界面如下：

![begin](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-11-12-tutorial-of-BAPS/begin.png){:.shadow} 

### 1. 数据预处理

如果你关注的是最为常用的个体非先验遗传归类推断，数据预处理需要使用第一个功能（Clustering of individuals），然后选择BAPS-format，导入数据文件。

![specify data format](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-11-12-tutorial-of-BAPS/specify-data-format.png){:.shadow} 

同时还可指定居群的名字和具体居群的行数索引，根据提示导入对应文件，格式参考示例数据。

![add-name-and-index](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-11-12-tutorial-of-BAPS/add-name-and-index.png){:.shadow} 

然后保存预处理文件，方便后续使用其他参数重复分析。

![save-proprocessed-data](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-11-12-tutorial-of-BAPS/save-proprocessed-data.png){:.shadow} 

### 2. Mixture分析

之后会提示输入可能的居群数上限（对应 STRUCTURE 中的最大K值），BAPS允许输入多个上限，软件会针对多个上限均进行mixture预分析。建议输入多个上限，且每个上限可重复多次，最大上限的指定原则和STRUCTURE中一致。

![input-maximum-K](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-11-12-tutorial-of-BAPS/input-maximum-K.png){:.shadow} 

然后保存mixture结果。

![save-mixture-result](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-11-12-tutorial-of-BAPS/save-mixture-result.png){:.shadow} 

### 3. Admixture分析

选择Population admixture analysis的Admixture based on mixture clustering功能，根据提示输入上一步的mixture结果文件，导入成功后依次需要填写minimum size of a population、number of iterations、number of reference individuals from each population、number of  iteration for reference individuals四个参数的具体数值。

- minimum size of a population，聚类的最小个体数量，如果某个推断出的聚类所含的个体数小于这个数值，其所包含的个体会排除在结果之外，被认为是异常值
- number of iterations，迭代次数，用于估算等位基因频率，运行时间允许的情况下，越大越好，推荐大于100
- number of reference individuals from each population、number of  iteration for reference individuals，参考个体数量和迭代参数，前者推荐为200，后者可以较小，一般为5---20之间

![input-minimum-size](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-11-12-tutorial-of-BAPS/input-minimum-size.png){:.shadow} 

![input-iteration](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-11-12-tutorial-of-BAPS/input-iteration.png){:.shadow} 

![input-number-reference-individuals](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-11-12-tutorial-of-BAPS/input-number-reference-individuals.png){:.shadow} 

![input-interation-of-referecne-individuals](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-11-12-tutorial-of-BAPS/input-interation-of-referecne-individuals.png){:.shadow} 

输入四个参数后即可等待运行完成，完成后弹出聚类结果窗口和最佳聚类K值。

![running](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-11-12-tutorial-of-BAPS/running.png){:.shadow} 

![result](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-11-12-tutorial-of-BAPS/result.jpg){:.shadow} 

## 3. 结果可视化

可以保存当前运行结果供后续查看，同时也可以保存聚类结果为图片，软件自身也支持更改聚类颜色。在运行文件夹内有结果文件，其内有每个体遗传聚类比例的log文件，该文件可使用[Distruct](https://web.stanford.edu/group/rosenberglab/distruct.html)软件进行更为细致的美化。

