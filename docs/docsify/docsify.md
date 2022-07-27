# **安装docsify**

## 安装docsify脚手架

默认已经安装`git`和`node`。

`win+R`运行命令行，输入`npm i docsify-cli -g`。若安装速度很慢，可以使用`npm`的淘宝镜像。

* 安装`cnpm`

`npm install -g cnpm --registry=https://registry.npm.taobao.org`

* 将`cnpm`设置为淘宝镜像

`npm config set registry https://registry.npm.taobao.org`

* 查看`cnpm`是否安装成功

`cnpm config get registry `

输入`cnpm i docsify-cli -g`，

![image-20220727102139553](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/202207271021617.png)

检查`docsify`是否安装成功

`docsify -v`  显示版本号则安装成功

## 初始化

在E盘新建github文件夹，进入github文件夹里面，右键打开`git bash`。

* 初始化

  `docsify init ./docs`

* 启动服务

  ` docsify serve ./docs`

![image-20220726162947582](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/202207271020075.png)

打开`http://localhost:3000`网址。

# **推送到远程仓库**

## 关联远程仓库

## 本地代码修改后更新到远程仓库

* `git add .`

* `git commit -m "提示信息"`

* `git push origin master`

  