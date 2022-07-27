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

![image-20220726162218270](C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20220726162218270.png)

检查`docsify`是否安装成功

`docsify -v`  显示版本号则安装成功

## 初始化

在E盘新建github文件夹，进入github文件夹里面，右键打开`git bash`。

* 初始化

  `docsify init ./docs`

* 启动服务

  ` docsify serve ./docs`

![image-20220726162947582](C:\Users\86186\AppData\Roaming\Typora\typora-user-images\image-20220726162947582.png)

打开`http://localhost:3000`网址。

# **推送到远程仓库**

更新本地代码，执行`git push -u origin origin/master`。

![image-20220727071526338](C:/Users/86186/AppData/Roaming/Typora/typora-user-images/image-20220727071526338.png)

若出现上述情况，说明网络有问题。等网络畅通的时候再执行即可。出现`Everything up-to-date`证明更新成功。