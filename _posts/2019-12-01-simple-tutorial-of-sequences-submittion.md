---
type: page
title: Excel遇上R，轻松完成序列提交
tags: 系统发育
key: simple-tutorial-of-sequences-submittion
---

本文是对如何向NCBI上传序列的详细介绍，不过本文完成时间较早，和最新的NCBI网页上传流程略有差别，不过应该影响不大！

<!--more-->


## 1. 序列及信息、注释文件准备

### 1.1 序列文件准备

将所有的序列集中在一个txt文件中，格式参照BankIt提供的模板。为使准备流程更为简单，可将原始的.fasta格式序列文件，序列编号（>Seq1, >Seq2, >Seq3…）,采集名称、采集号，序列名称在excel里进行编辑后，再粘贴到txt文件中。

- 序列标题以>Seq1, >Seq2, >Seq3…开始。
- 物种名称要求特定格式： [organism=Ficus abelii]，此字段在提交后会被自动识别为物种名，且会在名称文件中消失，如为使名称中出现物种名，再次添加即可。
- 标题内部内容以空格隔开，不支持非ASCII

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/1.png){:.shadow}

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/2.png){:.shadow}

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/3.png){:.shadow}

### 1.2    资源文件准备

资源文件包括采集人、采集日期、国家、生境、经纬度等信息。格式参照BankIt提供的模板。此步亦可略过。

BankIt模板和整理形式如下：

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/4.png){:.shadow}

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/5.png){:.shadow}

### 1.3    注释文件准备

将序列的分区、功能、产物等信息写到一个五列的txt文本中，格式如下图。  

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/6.png){:.shadow} 

- 注释文件内部内容tab键隔开；
- 如果分段片段不是全长，请加上“<”、“>”， “<”表示5’端缺失，“>”表示3’端缺失；
- 如果有编码序列被注释cds，则需要同时注释gene，codon_start，transl_table，product等信息；
- 其他详细说明参见BankIt提供的模板。

关于准备以上文件，需要对于序列该如何分段注释需要对上传序列的结构较为熟悉，如ITS和G3pdh的序列结构：  

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/7.png){:.shadow}

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/8.png){:.shadow}

了解结构后，具体各分区的起始终止位置可以参考NCBI中近缘类群已经上传注释的序列。然而，当一次性上传序列较多时，上述文件的准备是一个相当繁重的工作，如果再考虑到每个序列的不同的长度、分区的起始终止的位置由于插入缺失而不同，这个工作甚至会让人抓狂。但是，考虑到系统发育工作的特性，一次上传工作，通常为几十到几百个样品，几个到十几个DNA片段。如果能以片段为单位来批量生成上述文件，似乎可以达到一个可接受的程度。现在介绍大致流程：

1. 下载几条该类群的近缘类群已经注释的序列，同自己的序列同时比对，就可以获得片段不同分区的起始终止位置。比对完整后，可以将每个分区单独粘贴至Excel中，去换掉比对造成的gap字符“-”，即可使用公式获得片段总长、各分区的起始终止位置。参考图如下：

   ![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/9.png){:.shadow}
2. 上述步骤获取到全长和起始终止位置后，插入统一的注释文字内容后，即可获得如下文件：

   ![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/10.png){:.shadow}

3. 转化为Tab分割的文本文件：

   ![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/11.png){:.shadow}

4. 此时根据上述文件可以手工排版为NCBI要求的五列格式，但是此部依然是相对易错且繁琐的工作，本文在此尝试提供一个相对快捷的方式，使用R语言脚本实现注释文件的自动生成。但需要在原本的注释文件上加一行说明数据，即在上述的Excel文件中加上首行，说明每列文本在最终5列txt文本中应被放置的列数，然后存为txt格式，执行R代码后（要求对R语言初步了解），即生成所需注释文件。数据准备和预期结果见下图：

   ![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/12.png){:.shadow}

   ![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/13.png){:.shadow}

5. R脚本如下：（使用过程你需要适当修改一下关于文件读取和写入相关的路径参数）

   ```
   a<-read.table("original.txt",sep = "\t",stringsAsFactors = F) #读取原始注释数据,序列注释文件请命名为original.txt
   anno<-a[1,]
   a<-a[-1,]
   b<-nrow(a)
   c<-ncol(a)
   e<-d<-c()
   for(i in 2:c) # 生成注释位置和换行说明矩阵
     {
     if(anno[i]==1) 
       {d<-paste(d,i,"\t")
       e<-paste(e,3,"\t")}
     else
       if(anno[i]==4)
       {d<-paste(d,i,"\t")
       e<-paste(e,2,"\t")}
     }
   base0<-rbind(d,e)
   write.table(base0,"temp.txt",sep="\t",quote = F,row.names = F,col.names = F)
   char<-read.table("temp.txt")
   lieshu<-ncol(char)
   feature<-1:5
   base<-c("qbycs","qbycs","qbycs","qbycs","qbycs")
   for(l in 1:b) #根据说明矩阵将原始注释数据逐行写入注释文件
    {
     base[1]<-a[l,1]
     feature<-rbind(feature,base)
     base<-c("qbycs","qbycs","qbycs","qbycs","qbycs")
     for(k in 1:lieshu)
       {
       if(char[2,k]==3){leng<-1:3}  else  {leng<-4:5}
       base[leng]<-a[l,char[1,k]:(char[1,k]+char[2,k]-1)]
       feature<-rbind(feature,base)
       base<-c("qbycs","qbycs","qbycs","qbycs","qbycs")
       }
       feature<-feature[-1,]
       feature[feature=="qbycs"]<-""
       write.table(feature,"feature.txt",sep="\t",quote = F,row.names = F,col.names = F,append = TRUE) # 结果文件命名为feature.txt
       feature<-1:5
         }
   ```

## 2.  提交流程

提交流程相关教程较多，大同小异，此处简写。此外，提交可以多次中断，系统会自动记录信息，下次登录继续提交。简要流程如下：

1. 打开BankIt网站，登陆账户，准备提交数据。若没有账号，需先注册。  

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/14.png){:.shadow}

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/15.png){:.shadow}

2. 开始一个新的提交，输入个人信息。  

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/16.png){:.shadow}

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/17.png){:.shadow}

3. 输入参考信息，如序列作者；参考文献作者、题目、是否发表等等。

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/18.png){:.shadow}

4. 输入测序类型、序列是否为双向测序。（示例为桑格尔测序，单向测序）  

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/19.png){:.shadow}

5. 输入序列公布日期，序列类型等。同时，开始上传序列数据，建议以文本形式上传。若文件中出现非ANSII编码内容，则会报错。  

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/20.png){:.shadow}

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/21.png){:.shadow}

6. 输入所提交序列的研究目的。  

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/22.png){:.shadow}

7. 输入提交类别。  

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/23.png){:.shadow}

8. 上传序列的采集信息。此步亦可省略。  

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/24.png){:.shadow}

9. 上传序列注释文件。根据可能的报错修改注释文件。 

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/25.png){:.shadow}

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/26.png){:.shadow}

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/30.png){:.shadow}

10. 确认上传。如果为二次上传（resubmission），此时需要输入初次上传的上传号。

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/27.png){:.shadow}

11.   上传完成，注册邮箱会收到提交完成的邮件。如果没有错误，NCBI大约会在1-3个工作日邮件通知你序列号。一般来说，NCBI工作人员仅作格式审查，对于注释内容是否合适翔实通常不做要求。

![](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2019-12-01-simple-tutorial-of-sequences-submittion/28.png){:.shadow} 