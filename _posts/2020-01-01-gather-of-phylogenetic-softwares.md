---
type: page
title: 系统发育常见软件与在线工具合集
tags: 系统发育
mathjax: true
key: gather-of-phylogenetic-softwares
---


本篇文章是为了记录本人在系统发育实验和数据分析过程中，所使用过的以及部分未使用但如雷贯耳的软件的集合。当然，相对于整个系统发育软件之汪洋大海，此处不过一滴水！

<!--more-->

## 1. 数据获取

### 1.1 测序数据整理

- [DNAstar]( https://www.dnastar.com/ ) DNAstar是一个序列编辑和分析的全功能包，其子包Seqman能比对和手动调整Sanger测序文件，操作简单，但默认不解析少量低质量测序结果的测序文件
- [Chromas]( https://technelysium.com.au/wp/chromas/ ) 功能和Seqman类似，不支持测序结果反向互补查看，但没有Seqman的低质量限制，可做为Seqman的补充

### 1.2 序列比对

- [Mega]( https://www.megasoftware.net/ ) 全能型系统发育工具，比对和编辑序列较方便，比对算法集成ClustralX和Muscle方法
- [Mafft]( https://mafft.cbrc.jp/alignment/software/ ) 快速而准确的序列比对工具，在序列比对方面比Mega效果更好

### 1.3 比对后处理

- [PhyDE]( http://www.phyde.de/ ) 序列编辑软件，可以多开，方便多个比对结果之间进行比较
- [FastGap]( https://www.aubot.dk/FastGap_home.htm ) 可以对比对后的**序列的gap进行重编码**，提高序列信息使用效率
- [Gblocks]( http://www.phylogeny.fr/one_task.cgi?task_type=gblocks ) 在线工具，**选择序列保守区**，使得后续系统发育分析免受变异过大的比对区域的不良影响
- [DAMBE]( http://dambe.bio.uottawa.ca/Include/software.aspx ) 一个低调但全能的系统发育软件，定位与Mega类似，包括**饱和度检测**功能点
- [DNAsp]( http://www.ub.edu/dnasp/ ) 序列分析软件，计算各种序列多样性数据，如核苷酸多样性、序列信息位点含量、单倍型等

## 2. 格式转换

- [DAMBE]( http://dambe.bio.uottawa.ca/Include/software.aspx ) 少有的集成有格式转换模块的综合性软件
- [PGDSpider]( http://www.cmpg.unibe.ch/software/PGDSpider/ ) 专门的格式转换软件，可以在**众多系统发育和群体遗传学的文件格式**之间转换
- [EasyCodeML]( https://github.com/BioEasy/EasyCodeML ) 进化选择压力检测软件，但是也集成了部分常见格式的转换功能

## 3. 模型选择

- Modeltest/[MrModeltest]( https://github.com/nylander/MrModeltest2 )---ModelGUI 最常使用的DNA突变模型选择软件组合，依附于PAUP，直接生成适用于MrBayes和Garli的对应模型命令模块
- [jmodeltest]( https://en.bio-soft.net/tree/MODELTEST.html ) 模型选择软件，优势是可选择的模型很多，缺点是运算速度很慢
- [Moderfinder]( http://www.iqtree.org/ ) 较新的模型选择软件，速度很快，集成于iqtree里面
- [PartitionFinder]( http://www.robertlanfear.com/partitionfinder/ ) 较新的模型和数据分区选择软件

## 4. 发育树构建

### 4.1 最大简约法法

- [PAUP]( https://paup.phylosolutions.com/ ) 老牌著名系统发育软件，支持UPGMA，MP，ML等方法。
- [Mega]( https://www.megasoftware.net/ ) 支持最大简约法
- [DAMBE]( http://dambe.bio.uottawa.ca/Include/software.aspx )  支持最大简约法
- [Phylip]( http://evolution.genetics.washington.edu/phylip.html ) 老牌系统发育软件，可覆盖系统发育构建的几乎全部流程

### 4.2 最大似然法

- [PAUP]( https://paup.phylosolutions.com/ ) 老牌著名系统发育软件，支持UPGMA，MP，ML等方法。

- [Phylip]( http://evolution.genetics.washington.edu/phylip.html ) 老牌系统发育软件，可覆盖系统发育构建的几乎全部流程

- [Garli]( https://molevol.mbl.edu/index.php/Garli_wiki ) 基于遗传算法的构建ML树的软件

- [RAxML]( http://www.exelixis-lab.org/software.html ) 现在较为常用的ML树构建软件，速度很快，从RAxML开始，由于peusolikelihood和快速自展的引入，最大似然法的运算速度得到极大改善，一改最大似然法计算强度大的印象

- [ExaML]( http://www.exelixis-lab.org/software.html ) RAxML的扩展，支持并行运算，速度较快，适用于基因组数据

- [iqtree]( http://www.iqtree.org/ ) 集成了模型选择和发育树评估的建树软件，使用起来方便，在[Zhou et al.]( https://doi.org/10.1093/molbev/msx302 )对各种快速似然发育树构建方法（RAxML，[PhyML]( http://www.atgc-montpellier.fr/phyml/ )，[Fasttree]( http://www.microbesonline.org/fasttree/ )，iqtree）的评价中，iqtree综合表现最好

  | Programs | Optimality Criterion | Starting Tree | Topological Moves | Supported Models(DNA) |Supported Models(AA) |  Partitioned Analysis |
  | -------- | -------------------- | ------------- | ----------------- | ---------------- | -------------------- |-------------------- |
  |RAxML v8.2.0 (ExaML v3.0.17) |ML| Parsimony/random/custom| SPR| Common and custom models| JC69, K80, HKY85, GTR| Y|
  | PhyML v20160530 | ML   | Parsimony/random/custom | Interleaved NNI and SPR | Common and custom models | Common and custom models | Y|
  |IQ-TREE v1.4.2| ML| BIONJ and multiple parsimony/random/custom |NNI and stochastic perturbation| Common and custom models |Common and custom models| Y|
  |FastTree v2.1.9| ML| Heuristic NJ |NNI and SPR (ME) followed by NNI (ML)| JTT, WAG, LG |JC69, GTR| N |

  > 图表参考自该[论文]( https://academic.oup.com/mbe/article/35/2/486/4644721 )

### 4.3 贝叶斯法

- [MrBayes]( http://nbisweden.github.io/MrBayes/ ) 贝叶斯方法的主要软件，但相对于支持快速自展的ML方法，速度较慢

- BEAST 一个基于贝叶斯方法构建发育树、物种树、时间树以及时空动态的平台型软件，分为两个版本[BEAST1]( http://beast.community/ )和[BEAST2]( http://www.beast2.org/ )。

- [ExaBayes]( https://cme.h-its.org/exelixis/web/software/exabayes/ ) 针对于大数据集的贝叶斯构树软件

  | Program | Brief description                                            |
  | ------- | ------------------------------------------------------------ |
  | BEAST   | Implements a vast number of models. Examples are the simultaneous estimation of the tree topology and divergence times, phylodynamics, phylogeography, and species tree estimation under the MSC model. |
  |MrBayes| Implements a large number of models for analysis of nucleotide, amino acid and morphological data. Estimates species phylogenies and species divergence times.|
  |RevBayes| Similar to MrBayes, but with its own programming language to set up complex hierarchical Bayesian models.|
  |MCMCTree| Estimates divergence times on a fixed phylogenetic tree.|
  |Phycas |Estimates phylogenetic trees based on nucleotide data. This allows for multifurcating trees, helping to reduce spuriously high posterior probabilities for phylogenies.|
  |PhyloBayes| Reconstructs phylogenetic trees using infinite mixture models to account for among-site and among-lineage heterogeneity in nucleotide or amino acid compositions, which may be important for inferring deep phylogenies.|
  |BPP| Implements species tree estimation and species delimitation under the MSC model using multi-loci genomic sequence data.|
  |Migrate |Estimates population sizes and migration rates under the population-subdivision model based on molecular data.|
  |IMa2 |Estimates divergence times, population sizes and migration rates under the isolation-with-migration model using multi-loci DNA sequence data and a fixed phylogenetic tree for populations.|
  |Structure| Estimates population structure from multi-loci genotype data.|
  |BAMM |Estimates clade diversification rates on phylogenies.|
  |Tracer |A program for MCMC diagnostics and summaries.|
  |AWTY | A package for MCMC diagnostics for Bayesian phylogenetic inference.|
  
  > 图标参考自此[论文]( https://www.nature.com/articles/s41559-017-0280-x )

## 5. 系统发育网络构建

- [TCS]( http://w3.ualg.pt/~rcastil/SOFTWARE_WINDOWS/TCS1.21/docs/TCS1.21.html ) 简单的构建系统发育网络的软件，官方的下载链接可能已经失效
- [Network]( http://www.fluxus-engineering.com/sharenet.htm ) 同上
- [SplitsTree]( https://en.bio-soft.net/tree/SplitsTree.html ) 支持多种算法（距离法，NJ法等）的发育网络构建软件
- [Phylonet]( https://bioinfocs.rice.edu/phylonet ) 利用最大似然算法推断系统发育网络，能够区分杂交事件和不完全谱系分选
- [JML]( https://github.com/simjoly/jml ) 同样宣称可以区分杂交和不完全谱系分选的发育网络构建软件
- [Dendroscope]( http://dendroscope.org/ )

  |                                  | SplitsTree                   | Network    | Arlequin                  | TCS                   | T-Rex                 | SpectroNet        | CombineTrees |
  | -------------------------------- | ---------------------------- | ---------- | ------------------------- | --------------------- | --------------------- | ----------------- | ------------ |
  | Input  format                    | Nexus                        | Unique     | Unique, can import Phylip | Nexus                 | Phylip                | Nexus             | Nexus        |
  | Data types                       | Characters, distances, trees | Characters | Characters                | Characters, distances | Characters, distances | Characters, trees | Trees        |
  | **Network method**               |                              |            |                           |                       |                       |                   |              |
  | *Character-display networks*     |                              |            |                           |                       |                       |                   |              |
  | Median network                   | *                            |            |                           |                       |                       | *                 |              |
  | Qusai-median network             |                              | *          |                           |                       |                       | *                 |              |
  | Reduced-median network           |                              |            |                           |                       |                       |                   |              |
  | Greedily reduced-median netword  |                              |            |                           |                       |                       |                   |              |
  | Local buneman graph              |                              |            |                           |                       |                       |                   |              |
  | Quartet window annlysis          |                              |            |                           |                       |                       |                   |              |
  | Pruned median network            |                              |            |                           |                       |                       |                   |              |
  | Pruned quasi-median network      | *                            |            |                           |                       |                       |                   |              |
  | Parsimony splits                 | *                            |            |                           |                       |                       |                   |              |
  | Splits decomposition             | *                            |            |                           |                       |                       |                   |              |
  | Neighobor-net                    | *                            |            |                           |                       |                       |                   |              |
  | *Parsimony networks*             |                              |            |                           |                       |                       |                   |              |
  | Netting                          |                              |            |                           |                       |                       |                   |              |
  | Union of maximum-parsimony trees |                              |            |                           |                       |                       |                   | *            |
  | Minimum-spanning netword         | *                            |            | *                         |                       |                       |                   |              |
  | Median-joining                   | *                            | *          |                           |                       |                       |                   |              |
  | Statistical-parsimony            |                              |            |                           | *                     |                       |                   |              |
  | *Other networks*                 |                              |            |                           |                       |                       |                   |              |
  | Pyramids                         |                              |            |                           |                       |                       |                   |              |
  | Statistical geometry             |                              |            |                           |                       |                       |                   |              |
  | Concordance tree                 |                              |            |                           |                       |                       |                   |              |
  | Netview                          |                              |            |                           |                       |                       |                   |              |
  | Reticulogram                     |                              |            |                           |                       | *                     |                   |              |
  | *Tree-display networks*          |                              |            |                           |                       |                       |                   |              |
  | Consensus network                | *                            |            |                           |                       |                       | *                 |              |
  | Super-network                    | *                            |            |                           |                       |                       |                   |              |
  | Filtered super-network           | *                            |            |                           |                       |                       |                   |              |
  
  > 该表参考自书籍 *Morrison, D. A. (2011). An introduction to phylogenetic networks. RJR productions.* 

## 6. 物种树构建

- BEAST 

- [BPP]( http://abacus.gene.ucl.ac.uk/software/ ) BEAST和BPP软件推算物种树的时候同时计算每个基因的基因树及其和每个物种树的组合概率，称为一步法，一般较为准确，但是运算量很大，难以适用于基因组时代的大量数据

- [ASTRAL]( https://github.com/smirarab/ASTRAL ) 该软件需先计算出每个基因的基因树，然后再根据基因树利用溯祖原理推断出物种树，称为两步法，速度很快

- [STEM-hy]( https://www.asc.ohio-state.edu/kubatko.2//software/STEM/ )

- [MP-EST]( http://faculty.franklin.uga.edu/lliu/mp-est )

- NJst

  |Program| Analytical framework| Input| Output|
  |---|---|---|---|
  |GMYC| Best-fit tree branching models (coalescent vs Yule)| Ultrametric gene tree |Transition point from species to populations, and estimate of species number|
  |Brownie| Maximum likelihood or gene tree parsimony| Gene trees |Species tree of delimited species and group membership|
  |SpedeSTEM |Maximum likelihood and/or information theory| Sequence alignments and group membership| Species tree of delimited species|
  |BP&P | Bayesian and/or reversible-jump MCMC| Sequence alignments, group membership, and guide tree |Posterior probability distribution of species delimitation models, coalescent times, and population sizes|

  ![]( https://oup.silverchair-cdn.com/oup/backfile/Content_public/Journal/mbe/35/2/10.1093_molbev_msx302/4/m_msx302f1.png?Expires=1580765501&Signature=A8DefAUQ4MmV0oK0RzLYrROYNzWTHJDZ~uUSEh4I4ornI9IBdp4VtuNyinkmyCyi1E-1ZT1c9PIhWrEG4iiq5I1eFtkWYBz7Le-U2CKjM8P9KjhpvwennYBZCvtcu3aD~oDMRuzfjLuQ3c9Qg4Strl62TZulecbI-8HkdsxNkDkuoebxDGoG8Gr19~gZG28OD17gXP~GnRcJHBf6NJCVDhofXM4dQnFtlPYayFt1DfROrVACQ0PSbinekb--bMqKZyPA4-xlMEgLnPQBeUK15TxS5PLHfCqDXia~10plQx08avakUHum-zW8dsSk5~lB3a3fRc8LhGg-3hRyM29HHw__&Key-Pair-Id=APKAIE5G5CRDK6RD3PGA )

> 图表参考自此论文[论文]( https://www.sciencedirect.com/science/article/pii/S0169534712001000 )

## 7. 发育树注释

- 祖先状态重建
  - [Mesquite]( http://www.mesquiteproject.org/ ) 功能相当全面的系统发育软件，包括其他软件少有的发育树编辑功能。对于祖先状态重建，该软件支持MP和ML方法
  - [BayesTraits]( http://www.evolution.rdg.ac.uk/BayesTraitsV3/BayesTraitsV3.html ) 支持贝叶斯方法进行状态重建，这里状态包括形态性状和地理分布数据
  
- 祖先地理重建
  - [RASP]( http://mnh.scu.edu.cn/soft/blog/RASP/ ) 常见的祖先地理重建软件，操作简便，支持多种模型和参数设置
  - [BayesTraits]( http://www.evolution.rdg.ac.uk/BayesTraitsV3/BayesTraitsV3.html ) 支持贝叶斯方法进行状态重建，这里状态包括形态性状和地理分布数据
  
- 时间树
  
  - BEAST 最常用的时间树构建软件，基于贝叶斯算法，速度较慢
  - [MCMCtree]( http://abacus.gene.ucl.ac.uk/software/MCMCtree.Tutorials.pdf ) [PAML]( http://abacus.gene.ucl.ac.uk/software/paml.html )软件的子包，常用的时间树构建软件，在基因组时代使用较多
  - [r8s]( http://ginger.ucdavis.edu/r8s ) 基于最大似然法的时间树构建软件，计算相对时间，善于应对没有化石校准点的状况，貌似官方下载链接已失效
  
  | Program      | Method               | Brief description                                            |
  | ------------ | -------------------- | ------------------------------------------------------------ |
  | Beast        | Bayesian             | Comprehensive suite of models. Particularly strong for the analysis of serially sampled DNA sequences. Includes models of morphological traits |
  | DPPDiv       | Bayesian             | Dirichlet relaxed clock model. Fossilized birth–death process prior to calibrate time trees |
  | MCMCTree     | Bayesian             | Comprehensive suite of models of rate variation. Fast approximate likelihood method that allows the estimation of time trees using genome alignments |
  | MrBayes      | Bayesian             | Large suite of models for morphological and molecular evolutionary analysis. Comprehensive suite of models of rate variation |
  | Multidivtime | Bayesian             | The first Bayesian clock dating program. Introduced the geometric Brownian model and the approximate likelihood method |
  | PhyloBayes   | Bayesian             | Broad suite of models. Uses data augmentation to speed up likelihood calculation and can be efficiently used in parallel computing environments (MPI enabled) |
  | r8s          | Penalized likelihood | Very fast (uses Poisson densities on inferred mutations to approximate the likelihood). Suitable for the analysis of large phylogenies. Suitable for estimating relative ages (by fixing the age of the root to 1). Does not deal with fossil and branch length uncertainty correctly |
  | TreePL       | Penalized likelihood | Similar to r8s                                               |
  
  > 图标参考自此[论文]( https://www.nature.com/articles/nrg.2015.8 )。

##  8. 发育树评估

- [Consel]( http://stat.sys.i.kyoto-u.ac.jp/prog/consel/ ) 一个年代相当久远的发育树评估软件，但是功能相对全面，现在还少见可以替代的软件
- [Bucky]( http://www.stat.wisc.edu/~ane/bucky/ ) 多基因树中，可以评估发育树中某个拓扑结构受到多少个基因数据的支持，而不是仅仅只看总体的支持率

## 9. 发育树可视化

- [Figtree]( http://tree.bio.ed.ac.uk/software/figtree/ ) 常见又好用的发育树可视化软件，当额外的形态性状或者地理分布注释数据不多的时候，很好用

- [Tree graph]( http://treegraph.bioinfweb.info/ ) 发育树可视化软件，特色之一是可以手动画发育树，自定义拓扑结构和枝长

- [iTol]( http://itol.embl.de/ ) 发育树可视化在线工具，可以注释多种多样的数据

- [EvolView]( https://www.evolgenius.info/evolview/ ) 类似iTOL的在线工具，但是是由国人创造的

- [ggtree]( https://bioconductor.org/packages/release/bioc/html/ggtree.html ) Y叔开发的发育树可视化R包，在最新的版本中ggtree被拆分成了树文件读取解析的[treeio]( http://www.bioconductor.org/packages/release/bioc/html/treeio.html )和专注于可视化的ggtree，如果你熟悉R语言，那么也不失于一个好选择


## 10. 在线工具

- [CIPRES]( http://www.phylo.org/ ) 系统发育在线工具， 支持大量主要的系统发育和群体遗传性软件（ [RAxML](http://sco.h-its.org/exelixis/software.html); [MrBayes](http://mrbayes.sourceforge.net/); [BEAST](http://beast.bio.ed.ac.uk/); [BEAST2](http://www.beast2.org/); [GARLI](https://www.nescent.org/wg_garli/Main_Page); [MAFFT](http://mafft.cbrc.jp/alignment/software/); [ExaBayes](https://sco.h-its.org/exelixis/web/software/exabayes/); [DPPDIV](http://phylo.bio.ku.edu/content/tracy-heath-dppdiv); [FastTree,](http://meta.microbesonline.org/fasttree/) [jModelTest2](http://code.google.com/p/jmodeltest2/), [ModelTest-NG](https://www.biorxiv.org/content/10.1101/612903v1), [PAUP](https://people.sc.fsu.edu/~dswofford/paup_test/), [ParallelStructure](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0070651), [PartitionFinder2](http://www.robertlanfear.com/partitionfinder/), [IQ Tree](http://www.iqtree.org/), [Bali-Phy](http://www.bali-phy.org/), and [Migrate-N](http://popgen.sc.fsu.edu/Migrate/Migrate-n.html).  ），并且这些软件都被配置以支持并行计算

- [MABL]( http://www.phylogeny.fr/phylogeny.cgi ) 小众的系统发育在线工具

- [GBlocks]( http://www.phylogeny.fr/one_task.cgi?task_type=gblocks&tab_index=1 ) 保守区选择在线工具

- [FindModel]( https://www.hiv.lanl.gov/content/sequence/findmodel/findmodel.html ) 碱基突变模型选择工具

- [bPTP]( https://species.h-its.org/ ) 物种划分在线工具，基于泊松树过程处理发育树，推断出一棵树上合理的物种数量

- [GMYC]( https://species.h-its.org/gmyc/ ) 和上一个功能类似，只是基于广义混合Yule溯祖过程

- [RAxML BlackBox]( https://raxml-ng.vital-it.ch/#/ ) 一个RXaML在线工具

- [IQ-TREE]( http://iqtree.cibiv.univie.ac.at/ ) 软件官方提供的在线工具

- [HIV Database Tools]( https://www.hiv.lanl.gov/content/sequence/HIV/HIVTools.html ) 在线工具合集，主要针对于HIV数据，但是也有一些通用的工具

- [iTol]( http://itol.embl.de/ ) 发育树可视化在线工具，可以注释多种多样的数据

- [EvolView]( https://www.evolgenius.info/evolview/ ) 类似iTOL的在线工具，但是是由国人创造的

- [VizioMetrics]( http://viziometrics.org/ ) 这不是一个数据分析工具，他可以根据**图表标题**搜索其SCI文章出处

## 11. 软件合集

- [PhyloSuite]( https://dongzhang0725.github.io/dongzhang0725.github.io/installation/ ) 虽然它只是一个软件，而不是一个合集，但却是迄今最全面的系统发育流程整合软件，从序列下载、比对、模型选择到发育树构建均可以完成，主要是还可以设置批处理流程，设置好后一键运行，系统发育分析再也不用在软件间繁琐地跳来跳去了。
- [ExPASy]( https://www.expasy.org/resources ) Bioinformatics Resource Portal
- [Phylogeny Programs pages](  http://evolution.genetics.washington.edu/phylip/software.html#methods  )  系统发育软件集合
- [生物软件网]( http://www.bio-soft.net/tree.html ) 

