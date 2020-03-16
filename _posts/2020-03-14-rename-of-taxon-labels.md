---
type: page
title: 系统发育树分类群重命名
tags: 系统发育
mathjax: true
key: rename-of-taxon-labels
---

在系统发育分析的过程中，由于对序列的命名和在文章中需要呈现的名字不一致，或者根据系统发育结果需要对序列重新命名时，就会遇到需要对发育树中分类群的名字进行更改的情况。如果需要更改的数量较多，就会相当麻烦。本文会提供一些技巧应对几种情况下的重命名需求。

<!--more-->

## 1. 在Figtree中重命名

[Figtree](http://tree.bio.ed.ac.uk/software/figtree/)是发育树可视化最常用的软件之一，幸运的是该软件提供了批量重命名方法，具体步骤如下：

1. 准备批量重命名的配置文本文件，文本内容为两列，左侧为原始名字，右侧为想要改成的名字，两列之间用tab键隔开。首行为说明文字，内容和形式固定。

   | annotation     | rename            |
   | -------------- | ----------------- |
   | pumilaITS      | Ficus pumila      |
   | sarmentosaITS  | Ficus sarmentosa  |
   | pubigeraITS    | Ficus pubigera    |
   | pedunculosaITS | Ficus pedunculosa |

2. 打开Figtree软件，点击File>Import annotations，选择上述配置文件。操作完后，实际上已经替换，但还未立即显示。

   ![](https://github.com/qbycs/qbycs.github.io/blob/master/image/blog/2020-03-14-rename-of-taxon-labels/figtree.jpg?raw=true)

3. 在Figtree软件中，点选Tip Labels>Display>rename，即可显示重命名效果。此处rename和上述准备文件中的第二列首行保持一致，也可自行修改。但遗憾的是，此重命名效果仅限制在Figtree软件内部，无法通过另存导出修改名字后的树文件为其他软件所用。

   ![](https://github.com/qbycs/qbycs.github.io/blob/master/image/blog/2020-03-14-rename-of-taxon-labels/rename.jpg?raw=true)

## 2. 在iTOl中重命名

iTOL作为Web平台的发育树可视化方法，具有相当丰富的调整和注释功能，同时也可批量重命名。此处不提供iTOL的使用方法（默认已经入门iTOL的使用方法），仅贴上重命名的配置文件，配置好后直接拖入界面即可。

```
LABELS
#use this template to change the leaf labels, or define/change the internal node names (displayed in mouseover popups)

#lines starting with a hash are comments and ignored during parsing

#=================================================================#
#                    MANDATORY SETTINGS                           #
#=================================================================#
#select the separator which is used to delimit the data below (TAB,SPACE or COMMA).This separator must be used throughout this file (except in the SEPARATOR line, which uses space).

SEPARATOR TAB
#SEPARATOR SPACE
#SEPARATOR COMMA

#Internal tree nodes can be specified using IDs directly, or using the 'last common ancestor' method described in iTOL help pages
#=================================================================#
#       Actual data follows after the "DATA" keyword              #
#=================================================================#
DATA
#NODE_ID,LABEL

#Examples
#define a name for an internal node
#9031|9606,Metazoa

#change the label for leaf node 9606
#9606,Homo sapiens

pumilaITS	Ficus pumila
sarmentosaITS	Ficus sarmentosa
pubigeraITS	Ficus pubigera
pedunculosaITS	Ficus pedunculosa
```

## 3. 其他软件的一些重命名需求

重命名的功能无非就是批量的执行替换功能，如果有软件可以根据替换列表批量完成不同内容的替换，则也可完成多个分类群的重命名。前提是需要该文件为txt格式，比如Mesquite、RASP等软件的结果保存文件。下面推荐一个小软件，可以实现以上功能。

水淼软件：[点此下载]( https://github.com/qbycs/qbycs.github.io/blob/master/softwarerepositories/shuimiao.zip )

![](https://github.com/qbycs/qbycs.github.io/blob/master/image/blog/2020-03-14-rename-of-taxon-labels/shuimiao.jpg?raw=true)

1. 点选替换tab
2. 准备需要替换的分类群名字列表，不同的名字字符串之间使用$|$隔开
3. 准备要替换为的名字列表，不同的名字字符串之间同样使用$|$隔开
4. 粘贴进需要替换处理的文本
5. 点击预览一篇
6. 复制预览结果，粘贴使用