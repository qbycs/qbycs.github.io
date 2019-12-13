---
type: page
title: 利用LaTex编辑数学公式
tags: 电脑知识
key: formula-based-on-LaTex
---

在Typora中轻松数学编辑公式。

<!--more-->




公式的编辑是一个相对困难的事情。首先可以想到的是Word，对于一些简单的公式和函数，你的确可以使用word中的公式编辑器。但是，对于一些复杂的公式，Word的编辑功能就显得相对不足了。此时你可以有以下解决办法：

- 在Word使用公式编辑器插件增强Word的公式编辑功能；
- 使用[WPS]( https://www.wps.cn/ )，WPS中的公式编辑功能相对完善一些；
- 使用专门的公式编辑器软件，比如[MathType]( http://www.mathtype.cn/ )，不过这些通常是收费的；
- 使用LaTex来编辑公式，LaTex是一种基于Tex的排版系统，能以极其出色的效果排版书籍，特别是对于数学公式的支持非常好。当然整个Latex排版系统学习曲线非常陡峭 ，但如果我们仅仅是来学习其中的公式编辑功能，则是相对简单的。

其实，以上铺垫也仅仅是想切入LaTex来编辑公式而已。

## 1. 软件工具

支持LaTex公式编辑器的软件和网页在线工具（比如[这里]( https://www.codecogs.com/eqnedit.php )和[这里]( http://latex.codecogs.com/eqneditor/editor.php )）众多，在这里特别推荐[Typora]( https://www.typora.io/ )这个Markdown编辑器，在其中编辑公式是一个相当舒服的事情。

## 2. 编辑方式

我们先来看一个简单的例子，在Typora中输入一下内容：

```
$$
                                  f(x)=(x+1)^2=x^2+2x+1
$$
```

则可以得到：

$$
f(x)=(x+1)^2=x^2+2x+1
$$

可见，在两对$符号之间的内容会被自动渲染为公式。一个相对复杂的公式如下：

```
$$
f(x)=a_0+\displaystyle\sum_{n=1}^\infty{\Big (a_n \cos{n\pi x \over L}+b_n\sin {n\pi x \over L}\Big )}
$$
```

$$
f(x)=a_0+\displaystyle\sum_{n=1}^\infty{\Big (a_n \cos{n\pi x \over L}+b_n\sin {n\pi x \over L}\Big )}
$$

文中行内的公式可以如下写作：

```
假如$x^2-1=0$，那么$x=\pm1$。
```

则可看到一下语句：

>  假如$x^2-1=0$，那么$x=\pm1$。

所以，在Typora中利用LaTex编辑公式主要有以下逻辑：

- 独行公式应该为位于两对$之间，而且两对之间的内容只会被渲染成一个公式，多余空格都不会被渲染；
- 行内公式和函数，应该仅处于一对$之间；
- 公式从左到右渲染，每个诸如^ _等上下标特殊字符后默认只处理一个字符，多余的字符就不在有特殊效果。如果想要多个字符有特殊效果，需要位于一对大括号之间；
- 大部分特殊字符和效果都使用\符号来实现，具体可参考第3部分内容；

剩下的就应该交给练习和百度了。

## 3. 特殊符号总结

![](https://raw.githubusercontent.com/qbycs/qbycs.github.io/master/image/blog/2019-12-07-formula-based-on-LaTex/symbol1.jpg)

![](https://raw.githubusercontent.com/qbycs/qbycs.github.io/master/image/blog/2019-12-07-formula-based-on-LaTex/symbol2.jpg)

![](https://raw.githubusercontent.com/qbycs/qbycs.github.io/master/image/blog/2019-12-07-formula-based-on-LaTex/symbol3.jpg)

![](https://raw.githubusercontent.com/qbycs/qbycs.github.io/master/image/blog/2019-12-07-formula-based-on-LaTex/symbol4.jpg)

> 图片来源见此[博客]( https://blog.csdn.net/caiandyong/article/details/53351737 )。



## 4. 符号大小

可以使用\big, \Big, \bigg, \Bigg来控制括号的大小，如：

```
\Bigg ( \bigg [ \Big \{ \big \langle \left | \| x \| \right | \big \rangle \Big \} \bigg ] \Bigg )
```

结果如下：

$$
\Bigg ( \bigg [ \Big \{ \big \langle \left | \| x \| \right | \big \rangle \Big \} \bigg ] \Bigg )
$$

> 此部分内容参考自此[博客]( https://blog.csdn.net/miao0967020148/article/details/78712811 )。

## 5. 一些特殊效果

![](https://raw.githubusercontent.com/qbycs/qbycs.github.io/master/image/blog/2019-12-07-formula-based-on-LaTex/specialeffect.jpg)

## 6. 转入到Word中

当然，写好以后转入到Word中还是一个刚需，我们可以借助网络工具，具体步骤如下：

- 将写好的LaTex公式粘贴到网站[Engenharia Livre]( http://engenharialivre.com/latex-para-word/?# )中，网页会自动渲染出公式；
- 在公式右键，选择Mostrar Formulas Como>Codigo MathML，复制弹框内容；
- 将弹框内容以文本方式粘贴到Word 2016中即可。

![](https://raw.githubusercontent.com/qbycs/qbycs.github.io/master/image/blog/2019-12-07-formula-based-on-LaTex/Latextoword.jpg)