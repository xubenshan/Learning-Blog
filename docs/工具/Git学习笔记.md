# **Git学习笔记**

> 我学习Git的原因就是为了很方便的将本地代码上传到远程仓库，比如`gitee`，`GitHub`。

## **版本控制**

> 学习Git前一定要了解什么是版本控制。

所谓的版本控制其实就是一种管理文件，工程历史记录的一种技术。这种技术可以很方便的查看更改历史记录，恢复到以前的版本。版本控制常用于管理多人协同开发项目中。

常见的版本控制工具：

* Git
* SVN
* CVS
* VSS
* TFS
* Visual studio Online

版本控制的分类

* 本地版本控制

记录文件每次的更新，对每个版本做一个快照。

* 集中版本控制

所有的版本数据都存储在一个中央服务器上，用户从服务器上同步更新或上传自己的修改。

所有的数据都在一个服务器上，用户本地只有自己以前同步的版本，只有联网才能看到之前的版本。另外如果这个服务器损坏，就会丢失所有的数据，需要定期备份。SVN是集中版本控制的典型。

* 分布式版本控制

每个用户的电脑都是一个服务器，所有的版本信息都同步到本地的每个用户，这样就可以在本地查看所有的版本历史，离线在本地提交，只需联网的时候push到相应的服务器或其他用户那里。每个用户保存的都是所有的版本数据，因此不用担心出现因为服务器损坏，或者网络问题，而不能工作的情况。Git是分布式版本控制的典型。

## **Git简介**

> Git就是一个分布式版本控制工具。

Git是由Linux之父Linus开发的。是目前世界上最先进的分布式版本控制系统。

Git是开源的，免费的，最初的Git是为辅助Linux内核开发的，来代替Bitkeeper来管理和维护代码。

## **Git的安装**
### Windows下Git的安装
[Git下载官网](https://git-scm.com/downloads)

在Git官网下载可能会非常慢，还会出现打不开网页的现象。小伙伴们可以去淘宝镜像下载：http://npm.taobao.org/mirrors/git-for-windows/  ，下载对应版本即可。

安装的过程中只要无脑下一步即可。

安装完成之后，在开始菜单中会有Git项。如下图：

<img src="https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220731165152676.png" alt="image-20220731165152676" style="zoom: 80%;" />

简单说一下，`Git Bash`是类似`linux`的命令行；`Git CMD`是类似`window cmd`的命令行；`Git GUI`是图形化界面。

在日常使用中，我们一般只用`Git Bash`。

我自己下载的是`2.36.1`版本。通过`win+R`，打开运行，输入`cmd`。然后输入`git --version`，就可以查看对应的版本信息了。

![image-20220731165743893](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220731165743893.png)

## **Git的环境配置**

```bash
git config --system --list查看系统配置

git config --global --list查看本地配置
```

使用Git前我们需要设置用户名和密码。

* `git config --global user.name "用户名"`

* `git config --global user.email "邮箱"`

设置完成后输入`git config --global --list`，就可以查看用户名和邮箱是否设置成功。

![image-20220731182535086](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220731182535086.png)

另外Git在安装过程中会自动的将环境添加到系统变量的path路径下。不用额外进行添加。

![image-20220731182135209](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220731182135209.png)

## **Git基本理论**



## **Git项目搭建**

在工作盘新建一个名为`test`文件夹，进入文件夹内部，右键打开`git bash`。

输入`git init`，将这个文件夹初始化成`git`管理的文件夹。

![image-20220731182959388](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220731182959388.png)

我们会看到文件夹内部多了一个`.git`文件夹。

输入`touch test.txt`，在工作目录下创建了一个test文本。

![image-20220731195654748](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220731195654748.png)

`git add test.txt`，将test文件添加到index暂存区；

`git commit -m "add test.txt"` 将test文件提交到本地仓库；

![image-20220731205156110](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220731205156110.png)

至此，我们已经将创建的文件存储在本地仓库了，我们可以通过pull命令将本地仓库同步到远程仓库中。下面看具体的做法。

### 使用Github

首先你要有一个Github账户。没有注册的小伙伴们可以先去注册一下。注册完成后点击右上角的加号，新建仓库 `New repository` 。

<img src="https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220731200551687.png" alt="image-20220731200551687" style="zoom:67%;" />

然后输入仓库名称，仓库描述，是否公开，最后创建仓库。

<img src="https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220731204108694.png" alt="image-20220731204108694" style="zoom:67%;" />


github仓库就创建完成了，接下来我们要让远程仓库和本地仓库关联起来。

在test文件夹下运行命令 `git remote add origin git@github.com:xubenshan/test.git`。注意要将`xubenshan/test`换成你自己的用户名。否则你关联的就是我的远程库，你是无法将本地库推送上去的。

![image-20220731204824909](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220731204824909.png)

出现`unsafe repository`这种情况的话，运行git给你的解决方案即可。`git config --global --add safe.directory F:/test`。

再次运行 `git remote add origin git@github.com:xubenshan/test.git`。这样就将本地库同远程库关联起来了。

在GitHub官方文档里面，关联完成后，还要将当前分支`master`改成`main`。`master`可能跟黑人有关。对于我们来说改不改其实问题不大。我们就不改了，这样命令会少一些。

执行命令`git push -u origin master`。这样就可以将本地仓库上传到远程库里面了。其中`origin`是远程库的名字，`master`是本地仓库的当前分支。

需要注意的是第一次执行这个命令的时候需要加`-u`。Git会把本地的`master`分支内容推送到远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。直接执行`git push origin master`。

![Snipaste_2022-07-31_21-31-53](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/Snipaste_2022-07-31_21-31-53.jpg)

刷新`github`界面就能看到我们上传的test文件了·。

### 使用gitee

先注册登录码云，完善个人的信息。

设置本机绑定ssh公钥，实现免密码登录。

```bash
# 进入用户目录下的.ssh目录 C:\Users\86186\\.ssh
# 生成ssh公钥
ssh-keygen -t tsa
```



![Snipaste_2022-07-31_21-50-51](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/Snipaste_2022-07-31_21-50-51.jpg)

生成完之后打开`id_rsa.pub`文件，将公钥粘贴到gitee里面。

![image-20220731215659358](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220731215659358.png)

添加成功！

创建仓库，和GitHub类似，这里就不再重复了。

然后我们在本地库使用命令`git remote add`把它和远程库关联起来。

`git remote add origin git@gitee.com:xu-benshan/test.git`。

之后的操作就和GitHub如出一辙了。`git push -u origin master`。

### Git问题汇总

在push的过程中，出现`error: failed to push some refs to 'gitee.com:xu-benshan/test.git`。解决方案参考[博客](https://blog.csdn.net/m0_43599959/article/details/108934056?ops_request_misc=&request_id=&biz_id=102&utm_term=failed%20to%20push%20some%20refs%20to%20%27g&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-108934056.142^v35^pc_rank_34&spm=1018.2226.3001.4187)

`error: failed to push some refs to 'github.com:xubenshan/test.git`

另一种原因：执行了`git branch -M main`，将`master`分支重命名为`main`。pull的时候要将`master`改成`main`。

`git push -u origin main`

## **Git操作**

### 版本管理

### 分支管理

### 标签管理

### 自定义Git

## **使用vscode操作Git**

