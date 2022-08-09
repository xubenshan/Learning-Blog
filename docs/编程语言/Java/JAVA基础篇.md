# JAVA基础篇

## JDK的安装和卸载（记录踩坑过程）

由于之前我下载过jdk，之后因为不用的缘故，将它卸载了。由于当时水平不高，没有正确的卸载，导致卸载的时候有残留。如今重新下载JDK的时候会出现双击exe文件，电脑没有反应。从发现原因到成功安装，花费了我近一天的时间。特此记录一下，避免有些朋友也出现这种问题，也能指导以后的自己能够正确的卸载JDK。

以下教程适合之前安装过JDK，卸载后又重新安装但是打不开安装程序的小伙伴。可以打开或者第一次安装可以自行选择看。

* YourUninstallerPortable卸载JDK

首先建议大家用YourUninstallerPortable这个软件去卸载东西。[YourUninstaller下载地址](https://wwc.lanzouj.com/ifsfn030z3cj)

<img src="https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220809105807538.png" alt="image-20220809105807538" style="zoom:50%;" />

我用过`geek`，也用过系统自带的卸载程序，但是显示没有`JDK`的残留文件了，仍然是打不开`exe`安装文件的。

打开`YourUninstallerPortable`，找到所有有关`JDK`的程序，右键`uninstall`，根据提示进行就可以了。

没发现这个软件之前，我按照网上的教程将系统变量里面的`JDK`相关的东西，还有注册表里面的残留文件，`C:\Users\86186\AppData\LocalLow\Oracle\Java`残留的`Java.exe`等文件全部删除，`cmd`指令输出`Java`，显示不是内部命令或外部命令，仍然是打不开`exe`安装程序。

如果不放心的话，卸载完成后大家可以去我上面说的这些地方看一看有没有残留。

* 安装JDK

我安装的是`JDK8_221`。双击`exe`安装程序，然后根据提示下一步就可以。安装完成后去自己的安装目录看以下是不是有`JDK`和`jDR`两个文件夹。

链接：https://pan.baidu.com/s/1LF9XWfGogMDlVU_kzFfbtA 
提取码：gdbv

![image-20220809111203628](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220809111203628.png)

> 不用单独下载jre，下载jdk的时候就自动下载了。

* 配置环境变量

右键此电脑，打开属性，点击高级系统设置。

![image-20220809111407390](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220809111407390.png)

打开环境变量，在系统变量下面点击新建。

![image-20220809111519316](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220809111519316.png)

变量名输入`CLASSPATH`，变量值输入`.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar`。点击确定。

![image-20220809111658951](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220809111658951.png)

新建，变量名输入`JAVA_HOME`，变量值输入JDK的安装目录，如果你没有更改安装目录，默认是`C:\ProgramFiles\Java\jdk1.8.0_221`。

![image-20220809111937513](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220809111937513.png)

在系统变量中找到Path，点击编辑，添加两条记录，`%JAVA_HOME%\bin` 和`%JAVA_HOME%\jre\bin`。

<img src="https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220809112759422.png" alt="image-20220809112759422" style="zoom:50%;" />

`win+R`输入`cmd`，打开之后输入`java`，`java -version`，`javac`。查看配置是否成功。

![image-20220809113237665](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220809113237665.png)

若显示正确信息，则证明配置成功。

* 更新JDK

如果只是单纯的想要更新JDK，没有必要删除所有的东西。我们可以用官方给的卸载工具将旧版本的JDK卸载掉。卸载后环境变量还会存在，只需安装新版本的JDK即可。[JAVA 卸载工具](https://www.java.com/zh-CN/download/uninstalltool.jsp)

![image-20220809113633829](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220809113633829.png)



