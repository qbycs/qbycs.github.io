---
type: page
title: 群体遗传学常用软件合集
tags: 群体遗传学
mathjax: true
key: gather-of-genetic-population-softwares
---


本文仅仅是为了记载我利用SSR数据进行群体遗传学分析的过程中所接触和使用的软件，以及少量相关的大名鼎鼎的软件，如果你刚开始群体遗传（仅在使用SSR数据时）学的研究，我想这些软件多数都可能对你有用，不妨一观。

<!--more-->


## 1. 数据获取

### 1.1 数据整理

- PeakScanner 可以处理SSR毛细管电泳的原始测量fsa格式数据
- Genemapper 功能同上，但可以处理部分低质量数据，同时可以批量导出峰形图，该软件收费

### 1.2 格式转换

- [PGDSpider]( http://www.cmpg.unibe.ch/software/PGDSpider/ ) 专门的**格式转换软件**，可以在主要的系统发育格式之间转换，**支持格式众多**
- [GenAlex]( https://biology-assets.anu.edu.au/GenAlEx/Welcome.html ) 群体遗传学Excel插件，兼顾格式转换功能
- DataFormater 针对主流的群体遗传学软件所需的格式进行转化，基于python语言开发

## 2. 群体遗传学参数统计

- [GenAlex]( https://biology-assets.anu.edu.au/GenAlEx/Welcome.html ) 对常用的群体遗传学参数进行估计
- [Popgene]( https://sites.ualberta.ca/~fyeh/popgene.html ) 常用的群体遗传学参数估计软件
- [Arlequin]( http://cmpg.unibe.ch/software/arlequin35/ ) 群体遗传结构分析软件，可实现AMOVA分析
- [PowerMarker]( https://brcwebportal.cos.ncsu.edu/powermarker/ ) 可用于计算微卫星位点的多态性，比如PIC参数，其他功能请见软件和官网
- [MicroChecker]( http://www.nrp.ac.uk/nrp-strategic-alliances/elsa/software/microchecker/ ) 基于哈温平衡计算微卫星位点中是否存在哑等位基因

## 3. 数据分析

### 3.1 地理遗传格局

- IBD 可在[GenAlex]( https://biology-assets.anu.edu.au/GenAlEx/Welcome.html )中完成

### 3.2 相似性分析

- PCoA 可在[GenAlex]( https://biology-assets.anu.edu.au/GenAlEx/Welcome.html )中完成
- NMDS 可在R语言Vega包中完成

### 3.3 种群历史动态

- 矢配分析 可在[DNAsp]( http://www.ub.edu/dnasp/ )中完成
- 奠基者效应 可在[DNAsp]( http://www.ub.edu/dnasp/ )中完成

### 3.4 遗传聚类分析

- [Structure]( https://web.stanford.edu/group/pritchardlab/structure.html ) 基于哈温平衡和等位基因频率进行个体的非先验祖先种群估计，使用较多，但使用前需要注意是否符合模式假设，和其配套的还有结果总结软件[CLUMMP]( http://www.stanford.edu/group/rosenberglab/clumpp.html )和可视化软件[DISTRUCT]( https://web.stanford.edu/group/rosenberglab/distruct.html )，以及ΔK值的[在线计算工具]( http://taylor0.biology.ucla.edu/struct_harvest/ )。
- [BAPS]( http://www.helsinki.fi/bsg/software/BAPS/ )  同上，但是对居群间样品规模大小差异不敏感
- [Instruct]( http://cbsuapps.tc.cornell.edu/InStruct.html )  Structure的扩展，不再依赖哈温平衡的假设
- [Admixture]( https://bioinformaticshome.com/tools/descriptions/ADMIXTURE.html )  和Structure类似，假设哈温平衡，能够处理大量的SNPs数据，在基因组时代使用较多
- [DAPC]( https://grunwaldlab.github.io/Population_Genetics_in_R/DAPC.html ) 基于PCA和判别分析的遗传聚类分析软件，不需要理论假设，速度很快
- Geneland、sNMF、Structurama、TESS等

### 3.5 基因流

- [IMa]( https://bio.cst.temple.edu/~hey/software ) 基于溯祖理论的历史基因流和分化时间估算的系列（IM，IMa，IMa2，IMa2p，IMa3）软件，使用广泛
- [BayesASS]( http://www.rannala.org/software/ ) 评估基因流的软件之一，暂时无法定向分析基因流
- TreeMix 利用二代测序的大量SNPs数据推断种群间历史基因流。







​       