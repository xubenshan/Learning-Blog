# latex排版笔记

## 前言

很早就听说latex写论文排版非常好，寒假偶然看到ElegantBook，感觉latex的排版非常漂亮。下定决心学一下。怕以后自己忘记，决定用Typora做一下笔记。

## Texstudio及Texlive软件安装





## 常用的快捷键

`ctrl+E`快速生成环境

`win+R`打开命令行，输入`texdoc 宏包名称`可以查看宏包的使用

`ctrl+shift+M`快速生成$...$，用来嵌入公式。

## Latex基本知识

### 各类文件

`cls`文件

`tex`文件

`sty`文件

### 导言区

```latex
\document{article}
中间就是导言区
\begin{document}
\end{document}
```





## Latex常用操作

### 页面设置

`\usepackage{geometry}`导入宏包

### 字体设置

```
{\CJKfontspec{华文中宋}   }
```



### 图片插入

导入宏包`usepackage{graphicx}`

### 文本颜色

```latex
\textcolor{颜色}{文本}
```



### 超链接

导入宏包`usepackage{hyperref}`

命令

```latex
\href{链接}{显示的文字}
```

### 参考文献

### 公式插入

### 插入目录

### 插入代码

```latex
\usepackage{listings}
\lstset{
	columns=fixed,       
	numbers=left,                                        % 在左侧显示行号
	numberstyle=\tiny\color{gray},                       % 设定行号格式
	frame=none,                                          % 不显示背景边框
	backgroundcolor=\color[RGB]{245,245,244},            % 设定背景颜色
	keywordstyle=\color[RGB]{40,40,255},                 % 设定关键字颜色
	numberstyle=\footnotesize\color{darkgray},           
	commentstyle=\it\color[RGB]{0,96,96},                % 设置代码注释的格式
	stringstyle=\rmfamily\slshape\color[RGB]{128,0,0},   % 设置字符串格式
	showstringspaces=false,                              % 不显示字符串中的空格
	language=c++,                                        % 设置语言
}


\begin{lstlisting}

\end{lstlisting}
```

### 插入pdf

> 这个操作常用于封面制作。latex自制封面的话会很麻烦，另外尽管网上有很多现成的latex封面，将代码移植到本地可能会出现各种各样的问题。最简单的方法就是导出pdf，将pdf文件插入到自己写的文章里面。

```latex
%导入宏包
\usepackage{pdfpages}

%调用
\includepdf[pages={1}]{cover.pdf}%注意要将pdf文件放在main.tex同一目录下
```



## 好看的盒子样式

比较好的教程：[点击这里](https://liam.page/2016/07/22/using-the-tcolorbox-package-to-create-a-new-theorem-environment/)

> 如果全篇都是黑白样式，显得会很单调。给一些特定内容加上好看的盒子可以看起来条理清晰，重点突出。

### 文本框底纹填充效果

```latex
%setting文件下的代码
\usepackage{lipsum} % 该宏包会生成一段本文，只是为了演示用，正式使用不需要引用。
\usepackage[dvipsnames,svgnames]{xcolor}
\usepackage[strict]{changepage} % 提供一个 adjustwidth 环境
\usepackage{framed} % 实现方框效果
\definecolor{redshade}{rgb}{1.00,0.90,0.90} % 定义一个新颜色名字叫redshade，rgb为1,0.9,0.9。若是{RGB}，后面就是{256*1,256*0.9,256*0.9}
% ------------------******-------------------
% 注意行末需要把空格注释掉，不然画出来的方框会有空白竖线
\newenvironment{formal}{%定义了一个新环境formal
\def\FrameCommand{%定义文本框的外观
\hspace{1pt}%
{\color{LightCoral}\vrule width 2pt}%2pt宽度的竖线，颜色是LightCoral
{\color{redshade}\vrule width 4pt}%4pt宽度的横线，颜色是redshade
\colorbox{redshade%文本框颜色为redshade
}%
\MakeFramed{\advance\hsize-\width\FrameRestore}% 这个命令用于在内容周围创建一个带框的框架。
\noindent\hspace{-4.55pt}% 这用于取消第一个段落的缩进
\begin{adjustwidth}{}{7pt}%这个环境用于调整带框的框架的宽度，左边距设置为 7pt。
\vspace{2pt}\vspace{2pt}%这些命令在带框的框架内的内容之前和之后添加垂直空间。
}
{%
\vspace{2pt}\end{adjustwidth}\endMakeFramed%结束
}
% ------------------******-------------------
%main文件下的代码
\begin{formal}
\lipsum[4]
\end{formal}
```
效果如下：

<img src="C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20240217114455631.png" alt="image-20240217114455631" style="zoom:67%;" />

推荐几个配色比较舒服的盒子。

```latex
\definecolor{brownshade}{rgb}{0.99,0.97,0.93} % 莫兰迪棕色，竖线颜色设为 BurlyWood
\definecolor{greenshade}{rgb}{0.90,0.99,0.91} % 绿色文本框，竖线颜色设为 Green
\definecolor{redshade}{rgb}{1.00,0.90,0.90}% 红色文本框，竖线颜色设为 LightCoral
```

效果如图：

<img src="C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20240217114953106.png" alt="image-20240217114953106" style="zoom: 50%;" />

也可以自己找喜欢的颜色DIY，推荐个查找颜色英文名字及RGB的网站：[点击这里](https://www.rgbku.com/chaxun.html)

再给一个自定义的全封闭的文本框盒子代码，适合用在题目解析，颜色尽量浅一些，显得不会很乱。下一小节有tcolorbox提供的代码。

```latex
\usepackage{ctex}%写中文一定要加这个宏包
\usepackage{mdframed}%创建一个新的带有自定义样式的框
% 定义浅蓝色
\definecolor{myblue}{RGB}{178, 215, 228}
% 定义浅灰色
\definecolor{mygray}{RGB}{249, 249, 249}
% 定义一个新的mdframed环境，名字叫mybox
\newmdenv[
linewidth=2pt, % 设置边框线宽度
linecolor=myblue, % 设置边框颜色
backgroundcolor=mygray, % 设置背景颜色
roundcorner=5pt, % 设置边框圆角
innerleftmargin=10pt, % 设置左内边距
innerrightmargin=10pt, % 设置右内边距
innertopmargin=10pt, % 设置上内边距
innerbottommargin=10pt % 设置下内边距
]{mybox}


%main文件下的代码
\begin{mybox}
首先看出这道题和书上知识没有任何关系，考的就是你的政治素养。abc四个选项读下来没有任何问题，d选项犹豫了一下也选上了，我觉得说国家具有很多高素质人才和劳动者是完全可以的，出题人不太会在这个地方扣东西。
\end{mybox}
```

效果如下：

![image-20240217122718516](C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20240217122718516.png)

### tcolorbox 宏包提供的样式

> 这种盒子看起来更美观，适合用在特定的内容，比如数学定理，各种例题。

```latex
%setting文件下的代码
\usepackage{ctex}%写中文一定要添加这个宏包
\usepackage{lipsum} % 该宏包会生成一段本文，只是为了演示用，正式使用不需要引用。
\usepackage[dvipsnames,svgnames]{xcolor}
\usepackage{tcolorbox}%注意上面两行顺序不能颠倒，xcolor必须在tcolorbox前面

%main文件下的代码	
	\begin{tcolorbox}
		[colback = Emerald!10, colframe = cyan!40!black, title = 这是个例题]%colback是盒子内部颜色，colframe是盒子边框颜色，title是边框说明
		%cyan!40!black意思是40%cyan和60%black。Emarald!10意思是透明度为10%的Emarald，数字越小，颜色越浅
		\lipsum[3]%盒子里面的内容
	\end{tcolorbox}
```
效果如下：

<img src="C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20240217121300962.png" alt="image-20240217121300962" style="zoom:67%;" />

更多的盒子配色


```latex
\begin{tcolorbox}[title=\textbf{Note},colback=SeaGreen!10!CornflowerBlue!10,colframe=RoyalPurple!55!Aquamarine!100!]
这道题材料有点长，但是最后一句话有个这表明，所以不得不读一下，读完发现中心思想就是不去描绘未来的具体细节，因为现在没有可以解决这些问题的材料。d就显而易见了。
\end{tcolorbox}
```

![image-20240217123429211](C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20240217123429211.png)

```latex
\begin{tcolorbox}
[title = \textbf{Proposition}, colback=Salmon!20, colframe=Salmon!90!Black]
这道题我在考场是犹豫了下的，因为枫桥经验这个点见到的不是很多，脑子没什么影响。但好在我隐隐约约记得在模拟卷做过，枫桥经验就是把风险矛盾在基层就化解掉，然后选了b。这说明考前多做些模拟卷还是有用的。
\end{tcolorbox}
```

![image-20240217123919526](C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20240217123919526.png)

上述盒子配色参考知乎文章[点击这里](https://zhuanlan.zhihu.com/p/336171630)

在上一节提到了自定义全封闭文本框盒子，这里提供一个tcolorbox自带的文本框盒子。

```latex
\begin{tcolorbox}[colback=JungleGreen!10!Cerulean!15,colframe=CornflowerBlue!60!Black]
	首先看出这道题和书上知识没有任何关系，考的就是你的政治素养。abc四个选项读下来没有任何问题，d选项犹豫了一下也选上了，我觉得说国家具有很多高素质人才和劳动者是完全可以的，出题人不太会在这个地方扣东西。
\end{tcolorbox}
```

![image-20240217123200521](C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20240217123200521.png)

### 加入图标的自定义盒子样式

> 该样式可以用来写一些注意事项，类似评注。

简单的图标我们可以使用`pifont`宏包来实现，提供了一些特殊的带有圈圈或者叉叉等符号的字符。用`\ding{number}`来调用该宏包。

每个数字都代表不同的符号，具体如下：

![image-20240217133802296](C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20240217133802296.png)

> 图片不太清晰，凑合看吧。pifont宏包在texdoc里面没有找到。

详细代码如下：

```latex
\documentclass{article}
\usepackage{ctex}%写中文必须用
\usepackage[dvipsnames,svgnames]{xcolor}
\RequirePackage[many]{tcolorbox}%自定义盒子必须写上面两行
% uespackage和RequirePackage几乎没有区别，但自定义文档时最好还是用RequirePackage
\usepackage{pifont}%这个宏包提供了一些特殊符号，如代码中使用的箭头符号 \ding{43}
\usepackage{geometry}%设置页面页边距，页眉页脚要用
\geometry{%
	left=1cm,%左
	right=1cm,%右
	top=1.5cm,%上
	bottom=1.5cm,%下
	bindingoffset=0cm%装订线偏移量，没啥用
	}%这样设置，note盒子才会铺满整个页面，不会显得很突兀。
	
	%全局设置盒子，在需要自定义多个盒子的时候可以使用
	\tcbset{
		colframe=magenta,
		colback=magenta!12!white,
		boxed title style={colback=magenta},%设置标题框的背景颜色为 magenta。
		breakable, %允许框在页面底部自动断开，以适应页面边界。
		enhanced, %启用高级功能，允许更复杂的框样式和效果。
		sharp corners,%设置框的角落为尖锐。
		boxsep=1pt,%设置框的内边距为 1pt。
		attach boxed title to top left={yshift=-\tcboxedtitleheight,  yshifttext=-.75\baselineskip},
		boxed title style={boxsep=1pt,sharp corners},%将标题框连接到框的左上角，通过 yshift 和 yshifttext 参数微调位置。
		fonttitle=\itshape,%图标文字的字体
		drop lifted shadow%添加阴影
	}
\definecolor{bbe}{RGB}{236, 0, 140}
	\newtcolorbox{note}[1][]{
	title={\scalebox{1.75}{\raisebox{-.25ex}{\ding{43}}}~Note},% 这个选项设置了框的标题，使用了 \scalebox 命令来调整图标的大小，并使用了 \raisebox 命令来调整图标的位置。ding{43} 是 pifont 宏包中的一个符号，表示一个带有角标的箭头。然后标题文本是 "Note"，标题和图标之间用空格分隔。
	colframe=violet!12!white,%盒子边缘的颜色
	colback=violet!12!white,%盒子内部的颜色，不包括图标和Note文字占据的部分
	coltitle=bbe,%图标和Note文字的颜色
	fontupper=\itshape,%字体为斜体
	boxed title style={colback=violet!12!white},%图标和Note文字占据部分的颜色
	%尽量让colframe,colback,boxed title style颜色保持一致
	boxed title style={boxsep=1ex,sharp corners},%%这个选项设置了标题框的内边距为 1ex，并且使标题框的角落变得尖锐。
	overlay unbroken and first={
		\node[below right,font=\normalsize,color=red,text width=.8\linewidth]
		at (title.north east) {#1};%这个选项用于在框的标题部分添加一个额外的节点，用于显示额外的信息。具体来说，它在标题的右上角添加了一个节点，用于显示传递给 note 环境的参数。这个参数是通过 #1 引用的，表示传递给 note 环境的可选参数。
	}
}


\begin{document}
\begin{note}
 从这个题中我们可以看出真题的出题风格，可以看到这四个选项是完全不同的，这种帽子题出题人不会设置两个迷惑选项的。在模拟卷中，可能就会设置一个迷惑选项，解放和增强社会活力（全面深化改革的关键所在。）
\end{note}
\end{document}
```

![image-20240217134012697](C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20240217134012697.png)

在这里简单画个图来说明一下`colframe`,`colback`,`boxed title style`具体控制的是哪里，这里容易混淆。

<img src="C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20240217135732580.png" alt="image-20240217135732580" style="zoom:50%;" />



## 选择题排版环境

### 计数器

```latex
\newcounter{defin}[section]%定义一个计数器，名字叫defin。遇到下一个section就重新计数 
\setcounter{defin}{0} %从0开始计数 
\renewcommand{\thedefin}{\arabic{defin}}%重新定义计数器表示方式。编号为阿拉伯数字。
```

### 新建环境

```latex
\newenvironment{definition}{\par\refstepcounter{defin}%新建环境，名字是definition，\par是换行， %\refstepcounter{defin}使用defin计数器 
{\noindent\bfseries{定义}\thesection.\thedefin\hspace{0.2em}}\kaishu}{\par}%\noindent首行不缩进， 定义用粗体，数字以节.计数器呈现，隔0.2字符显示内容，用楷书，接换行。
main文件下的代码 
\begin{definition} 
这是定理这是定理这是定理这是定理这是定理这是定理这是定理 
\end{definition}
```

### 实用的环境

* 例题环境

> 这个东西很实用，可以用来对各种题目进行排版
>
> ```latex
> %新建计数器 \newcounter{examm}[subsection] 
> \setcounter{examm}{0} 
> \renewcommand{\theexamm}{\arabic{examm}} 
> %新建环境 
> \newenvironment{example}{\par\vspace{5pt}%跟下一个example之间的距离 
> \refstepcounter{examm}\noindent{\songjian 例\textbf{\theexamm}\;}}{\par}%\textbf是加粗意思 
> %选项ABCD设计 
> \RequirePackage{sty/choices}%在主文件下新建sty文件夹，将choices宏包放入。
> \RequirePackage{setspace} \newenvironment{xgsj}{\par\hangafter 1\hangindent 2em}{\par} \newenvironment{choice}{\begin{xgsj}\begin{choices}}{\end{choices}\end{xgsj}}
> ```
>
> choices宏包下载链接：[点这里](https://wwlb.lanzout.com/iVDW81kde00j) 

**注**：选项ABCD设计用在ElegantBook盒子里面会错乱。原因未知。


* 解析环境

```latex
%原始版本
\newenvironment{solution}{ {\par\noindent\textbf{\color{black}解 \hspace{0.5em}}} }{\par}
```

一般我们要把解析过程用盒子包装起来，这样看起来显眼。可以参考上一节的好看的盒子样式。这里给

出我用的代码.

```latex
\RequirePackage[many]{tcolorbox}%一般我们要用很多盒子，要加这句话。
\newtcolorbox{solution}[1][]{ no shadow, top=2ex, leftrule=1.4pt, title={Solution}, 
colframe=green!79!blue, 
colback=green!12!white, 
boxed title style={colback=green!79!blue}, 
overlay unbroken and first={ \node[below right,font=\small,color=magenta,text width=.8\linewidth] at (title.north east) {#1}; }
```

![image-20240220182320697](C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20240220182320697.png)

## 实用模板

> 在学习latex的开始，我没有按照正常顺序来学，而是直接去找模板，然后自己修改，遇到不懂的去网上搜。慢慢的我就对latex的基本架构，基本语法了解清楚了。我相信大家学习latex的主要目的就是为了让自己的文章排版美观，而不是拘泥于latex语言本身，或者想要自己去开发一个模板。所以一个实用的模板是非常重要的。会节省我们的时间，让自己专注于文章内容，而不是形式。
>
> 下面就是我在学习过程中收集的比较好的模板，实用性很高。当然有些模板我是修改了一些细节，比如加入好看的盒子，修改字体等等。为了实用性，我将这些模板分为了四大类型，讲义类，习题类，试卷类以及论文类。下面分别介绍。

### 讲义类型

#### ElegantBook模板

#### bbe模板

### 习题集类型

#### 简洁模板

> 我用在分专题整理数学题，政治真题，大唐杯真题上面。

由于篇幅有限，我把完整代码放到了ubuntu上面。[点击这里](https://paste.ubuntu.com/p/2TtD8yJ2RQ/)

该模板在overleaf和Texstudio上面可以正常编译。效果如下：

![image-20240220183255722](C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20240220183255722.png)

#### litesolution模板

> 这个模板设计很清新，适合写试题解答，还可以一键隐藏解析。我用来写大唐杯真题解析。
>

下载地址：[点击这里](https://ctan.org/pkg/litesolution)

![image-20240222131144142](C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20240222131144142.png)

### 论文类型





### 试卷类型

#### 竖版试卷类型

参考模板[点击下载](https://www.ctan.org/pkg/LiteSolution)

#### 横板试卷类型

参考模板[点击这里](https://www.zhihu.com/question/402111484/answer/3302539544)

### 封面设计

> 在这里列出一些比较好看简洁或花哨的封面，方便以后的学

* ```latex
  % !TEX program = xelatex
  % 简洁书籍 封面模板
  % 作者信息：无垠的广袤
  % 个人主页：http://blog.sina.com.cn/h2457528767
  % 邮箱：lijinlei0907@163.com
  % 创作不易，转载请注明出处，谢谢合作！
  \documentclass{article}
  \usepackage{amsmath}
  \usepackage{ctex}
  \usepackage{tikz}
  \usetikzlibrary{intersections,decorations.text,shadings,3d,positioning,patterns}
  \definecolor{c1}{RGB}{62,97,127}
  \definecolor{c2}{RGB}{104,182,182}
  \definecolor{c3}{RGB}{107,190,190}
  \definecolor{c4}{RGB}{100,172,174}
  \definecolor{c5}{RGB}{95,162,162}
  \definecolor{c6}{RGB}{235,242,252}
  \usepackage{hyperref}
  \newcommand{\zhongsong}{\CJKfontspec{STZhongsong}}%华文中宋
  \newcommand{\xinwei}{\CJKfontspec{STXinwei}}%华文新魏
  \usepackage{lmodern}
  \begin{document}
  	\thispagestyle{empty}
  	\begin{tikzpicture}[remember picture,overlay,font=\sffamily\bfseries]
  		\fill[opacity=0.2,c6!50](current page.south east)rectangle (current page.north west);%遮住页码
  		%===================网格线==============================
  %		\draw[help lines,step=0.8cm,opacity=0.4,color=c1](current page.south east)grid(current page.north west);
  		%=================右上方弧线图像========================
  		\draw[ultra thick,c4,name path=big arc] ([xshift=-2mm]current page.north) arc(150:285:11)
  		coordinate[pos=0.225] (x0);
  		\begin{scope}
  			\clip ([xshift=-2mm]current page.north) arc(150:285:11) --(current page.north east);
  			\fill[c4!50,opacity=0.25] ([xshift=4.55cm]x0) circle (4.55);
  			\fill[c4!50,opacity=0.25] ([xshift=3.4cm]x0) circle (3.4);
  			\fill[c4!50,opacity=0.25] ([xshift=2.25cm]x0) circle (2.25);
  			\draw[ultra thick,c4!50] (x0) arc(-90:30:6.5);
  			\draw[ultra thick,c4] (x0) arc(90:-30:8.75);
  			\draw[ultra thick,c4!50,name path=arc1] (x0) arc(90:-90:4.675);
  			\draw[ultra thick,c4!50] (x0) arc(90:-90:2.875);
  			\path[name intersections={of=big arc and arc1,by=x1}];
  			\draw[ultra thick,c4,name path=arc2] (x1) arc(135:-20:4.75);
  			\draw[ultra thick,c4!50] (x1) arc(135:-20:8.75);
  			\path[name intersections={of=big arc and arc2,by={aux,x2}}];
  			\draw[ultra thick,c4!50] (x2) arc(180:50:2.25);
  		\end{scope}
  		%================日期==================================
  		\path[decoration={text along path,text color=c4,
  			raise = -2.8ex,
  			text = {|\sffamily\bfseries|10/05/2024},
  			text align = center
  		},
  		decorate
  		] ([xshift=-2mm]current page.north) arc(150:245:11);
  		
  		%===================坐标轴==============================
  		\node[opacity=0.5,color=c1] at([xshift=4cm,yshift=-4cm]current page.north
  		west){\tikz{\draw[-stealth](-0.3,0)--(0,0)node[below left]{$O$}--(3.6,0)node[below=2pt]{$x$};
  				\draw[-stealth,color=c1](0,-0.42)--(0,2)node[left]{$y$};
  				\draw(0,1.3)node[left]{$A$}..controls(1.4,0.6)and(2.2,2.4)..(2.8,1.7)node[right]{$B$}
  				--(2.8,0)node[below]{$C$};\node at(0.65,1.4){$f(x)$};}};
  		%=================标题信息=========================
  		\node[text=c1,anchor=west,scale=5,inner sep=0pt,font=\zhongsong] at
  		([xshift=-9.2cm,yshift=-1.25cm]current page.center) {考研政治八讲};
  		\node[text=c1,anchor=west,scale=2.5,inner sep=0pt,font=\zhongsong] at
  		([xshift=-4.2cm,yshift=-1.65cm]current page.center) {};
  		\node[text=c1,anchor=west,scale=3,inner sep=0pt,font=\zhongsong] at
  		([xshift=-9.20cm,yshift=-3.75cm]current page.center) {\fontencoding{T1}\fontfamily{ptm}\bfseries\selectfont 站在命题人视角的真题分析};
  		\node[text=c1,anchor=west,scale=1.5,inner sep=0pt,font=\zhongsong] at
  %		([xshift=-4.8cm,yshift=-3.65cm]current page.center) {\fontencoding{T1}\fontfamily{ptm}\bfseries\selectfont ()};
  		%\node [text=c1,scale=3,font=\heiti] at (-0.5,-12.8){\fontencoding{T1}\fontfamily{ptm}\bfseries\selectfont Notes};
  		%\node [text=c1,scale=1.5,font=\heiti] at (3,-12.98){\fontencoding{T1}\fontfamily{ptm}\bfseries\selectfont (First Edition)};
  		
  		\draw[ultra thick,c1!50]([xshift=1.5cm,yshift=-5cm]current page.west)--([xshift=-5cm,yshift=-5cm]current page.east);
  		
  		\node[text=c1,anchor=west,scale=2.5,inner sep=0pt,font=\heiti] at
  		([xshift=-8.2cm,yshift=-6cm]current page.center) {才疏学浅的小熊 \;~编};
  		
  		\node[opacity=0.5,scale=1.8,color=c1!80] at ([xshift=0.75cm,yshift=-8.0cm]current page.center) {$i\hbar \partial_t \psi(\boldsymbol{r},t) = H\psi(\boldsymbol{r},t)$};
  		\node[opacity=0.5,scale=1.8,color=c1!80] at ([xshift=4.80cm,yshift=-9.5cm]current page.center) {$= \left[-\frac{\hbar^2}{2m}\nabla^2+U(\boldsymbol{r})\right]\psi(\boldsymbol{r},t)$};
  		
  		%==============出版社信息=============================
  		\node[text=c1,scale=1.8,font=\xinwei] at ([yshift=2cm]current page.south){\href{http://blog.sina.com.cn/h2457528767}{小熊的网站：xubenshan.top}};
  	\end{tikzpicture}
  	
  \end{document}
  % 创作不易，转载请注明出处，谢谢合作！
  ```

<img src="https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/fenmian.jpg" alt="fenmian" style="zoom: 25%;" />

* beautybook模板里面的封面（标准A4大小）

<img src="https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/cover1.jpg" alt="cover1" style="zoom: 25%;" />






















