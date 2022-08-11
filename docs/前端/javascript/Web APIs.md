# JavaScript中级篇

**Web APIs**

> `javascript`包括`js`的语法部分和`Web APIs`的`DOM`和`BOM`部分
>
> `API`就是预先封装好的接口（函数），可以直接使用，不用关心内部原理。

## DOM

> DOM（Document Object Model） 文档对象模型

DOM文件树

![img](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/20210728143112521.gif)

### 获取元素

```javascript
1. 通过id得到元素
<div id="date">2022-8-7</div>
    <script>
        //页面加载是从上往下，因此script要写在div标签下面
        // getElementById返回的是一个element对象,参数是字符串
        var timer = document.getElementById('date');
        console.log(timer);// <div id="date">2022-8-7</div>
        console.log(typeof timer);// object
        //console.dir 打印我们返回的元素对象，能更好的查看里面的属性和方法
        console.dir(timer);
    </script>
2. 通过标签名获取
<ul>
        <li>知否知否应是绿肥红瘦1</li>
        <li>知否知否应是绿肥红瘦2</li>
        <li>知否知否应是绿肥红瘦3</li>
        <li>知否知否应是绿肥红瘦4</li>
        <li>知否知否应是绿肥红瘦5</li>
    </ul>
    <ol id="ols">
        <li>生僻字1</li>
        <li>生僻字2</li>
        <li>生僻字3</li>
        <li>生僻字4</li>
        <li>生僻字5</li>
    </ol>
    <script>
        var lis = document.getElementsByTagName('li');
        console.log(lis);//  [li, li, li, li, li]
        // 返回的是获取元素对象的集合，是一个伪数组
        console.log(lis[0]);
        for (var i = 0; i < lis.length; i++) {
            console.log(lis[i]);
        }
        //若找不到这个标签，返回一个空的伪数组。
        //element.getElementByTagName中的父元素必须是一个确定的元素。
        var ols = document.getElementsByTagName('ol');
        console.log(ols);// [ol]
        // console.log(ols.getElementsByTagName('li'));//会报错
        //正确写法
        console.log(ols[0].getElementsByTagName('li'));//[li, li, li, li, li]
        //常见的写法 给ol添加id属性
        var ol = document.getElementById('ols');
        console.log(ol.getElementsByTagName('li'));//[li, li, li, li, li]
</script>
3. H5新增获取元素方式 
    <div class="box">盒子</div>
    <div class="box">盒子</div>
    <div id="nav">
        <ul>
            <li>首页</li>
            <li>产品</li>
        </ul>
    </div>
    <script>
        //getElementsByClassName通过类名进行选择
       var boxs = document.getElementsByClassName('box');
       console.log(boxs);// [div.box, div.box]
       //querySelector(选择器 必须加) 返回指定选择器的第一个元素对象
       var firstBox = document.querySelector('.box');
       console.log(firstBox);//<div class="box">盒子</div>
       var nav = document.querySelector('#nav');
       console.log(nav); 
       var li = document.querySelector('li');
       console.log(li);
        //querySelectorAll(选择器) 返回指定选择器的所有元素对象
        var boxs = document.querySelectorAll('.box');
        console.log(boxs);// [div.box, div.box]
    </script>
4. 获取特殊标签 html body
		//获取body标签
        var body = document.body;
        console.log(body);
        //获取HTML标签
        var html = document.documentElement;
        console.log(html);
```

### 事件基础

```javascript
// 事件 触发响应的一种机制
// 事件三要素 
事件源 被触发的对象
事件类型 如何触发事件
事件处理程序 通过一个函数赋值的方式完成触发
	<button id="btn">才疏学浅的小熊</button>
    </div>
    <script>
        //点击一个按钮，弹出对话框
        var btn = document.getElementById('btn');
        //鼠标点击
        btn.onclick = function(){
            alert('欢迎来到我的博客');
        }
    </script>
// 执行事件的步骤
1.获取事件源
2.绑定事件
3.添加事件处理程序
<div>123</div>
    <script>
        //点击div控制台输出我被选中了
        var divs = document.querySelector('div');
        divs.onclick = function() {
            console.log('我被选中了');
        }
    </script>
```

### 操作元素

```javascript
// 改变元素的内容
innerText innerHtml
<button>点击显示时间</button>
    <div>显示时间</div>
    <script>
        var btn = document.querySelector('button');
        var divs = document.querySelector('div');
        btn.onclick = function() {
            divs.innerHtml = getTime();//getTime()显示当前时间，在日期对象那里有封装过
        }
    </script>//点击button，div里面的内容发生变化，显示当前的时间
//innerText innerHtml区别
		// innnerText不识别HTML标签 
        var divs = document.querySelector('div');
        divs.innerText = '<strong>你好</strong>';// <strong>你好</strong>
        //innerHtml识别HTML标签 W3C标准
        divs.innerHTML = '<strong>你好</strong>';// **你好**
        // 这两个属性可以读写 innerText不保留换行和空格 innerHTML保留空格和换行
//修改元素属性 src href title alt
	<button id="pic1">pic1</button>
    <button id="pic2">pic2</button>
    <img src="pic1.png" alt="" title="图片一">
    <script>
        var pic1 = document.getElementById('pic1');
        var pic2 = document.getElementById('pic2');
        var img = document.querySelector('img');
        // 注册事件
        pic2.onclick = function() {
            img.src = "pic2.png";
            img.title = "图片二";
        }
        pic1.onclick = function() {
            img.src = "pic1.png";
            img.title = "图片一";
        }
	</script>
//案例 分时显示不同的图片，同时显示不同的问候语
上午打开页面，显示上午好，显示上午的图片
下午打开页面，显示下午好，显示下午的图片
晚上打开页面，显示晚上好，显示晚上的图片
<img src="pic1.png" alt="">
    <div>上午好</div>
    <script>
        var img = document.querySelector('img');
        var div = document.querySelector('div');
        //得到当前的时间
        var date = new Date();
        var hour = date.getHours();
        if (hour < 12) {
            img.src = 'pic1.png';
            div.innerHTML = '上午好';
        } else if (hour < 19) {
            img.src = 'pic2.png';
            div.innerHTML = '下午好';
        } else {
            img.src = 'pic3.png';
            div.innerHTML = '晚上好';
        }
</script>
//表单元素的属性操作 type value disabled
    <button>按钮</button>
    <input type="text" value="请输入内容">
    <script>
        var btn = document.querySelector('button');
        var input = document.querySelector('input');
        //注册事件
        btn.onclick = function () {
            //表单里面的文字内容通过value实现
            input.value = '我点击了按钮';
            //被禁用，按钮不能再点击
            // btn.disabled = 'true'; 
            this.disabled = 'true';
            //this指向的是该事件函数的调用者    
        }
    </script>
// 仿京东显示密码
    <div class="box">
        <label for="">
            <img src="images/close.png" alt="" id="eye">
        </label>
        <input type="password" name="" id="pwd">
    </div>
    <script>
        var img = document.getElementById('eye');
        var pass = document.getElementById('pwd');
        var flag = 0;
        img.onclick = function() {
            if (!flag){
            pass.type = 'text';
            img.src = 'images/open.png';
            flag = 1;
        } else {
            pass.type = 'password';
            img.src = 'images/close.png';
            flag = 0;
        }
    }
    </script>
//通过style来修改元素的样式属性 样式比较少，使用比较方便
// 显示隐藏文本框内容 
    <style>
        input {
            color: #999;
        }
    </style>
</head>
<body>
    <input type="text" value="手机">
    <!-- <input type="text" placeholder="手机"> -->
    <script>
        var text = document.querySelector('input');
        // //获得焦点
        // text.onfocus = function() {
        //     this.placeholder = ' ';
        //     this.style.color = '#333';
        // }
        // //失去焦点
        // text.onblur = function() {
        //     this.style.color = '#999'
        //     this.placeholder = '手机';
        // }
        text.onfocus = function() {
            if (this.value === '手机') {
                this.style.color = '#333';
                this.value = ' ';
            }
            
        }
        text.onblur = function() {
            if (this.value === '') {
                this.style.color = '#999';
                this.value = '手机';
            }
        }
    </script>
// 使用className修改样式属性 element.className
当前元素的类名改成className
    <style>
        .pre {
            background-color: #333;
            font-size: 35px;
            width: 100px;
            height: 100px;
        }
        .change {
            background-color: purple;
            font-size: 25px;
            margin-top: 100px;
            
        }
    </style>
</head>
<body>
    <div class="pre">文字</div>
    <script>
        var div = document.querySelector('div');
        div.onclick = function() {
            // 通过修改元素的类名来更改元素的样式，适合样式多的情况
            //如果想要保留原来的类名，可以这样写 多类名选择器
            this.className = 'pre change';
            // this.className = 'change';
        }
    </script>
//密码框格式提示错误信息
    <style>
        div {
            width: 600px;
            margin: 100px auto;
        }
        .message {
            display: inline-block;
            font-size: 12px;
            color: #999;
            padding-left: 20px;
            background: url(images/mess.png) no-repeat left center;
        }
    .change {//密码错误
        background-image: url(images/wrong.png);
        color: red;
    }
    .right {//密码正确
        color: green;
        background-image: url(images/right.png);
    }
    </style>
</head>
<body>
    <div class="register">
        <input type="password" class="ipt">
        <p class="message">请输入6~16位密码</p>
    </div>
    <script>
        var pic = document.querySelector('.message');
        var input = document.querySelector('.ipt');
        input.onblur = function() {
          if (this.value != '') {//防止我们什么也不输入，出现报错的情况
            if (this.value.length < 6 || this.value.length > 16){
            pic.className = 'message change';
            pic.innerHTML = '你输入的位数不对';
            } else {
                pic.className = 'message right';
                pic.innerHTML = '你输入的密码正确';
            }
          }
        }
    </script>
```

**排他思想**

如果有同一组元素，我们想让其中一种元素实现某种样式，这时候就要用到循环的排他思想。

1. 所有元素去除样式
2. 给当前的元素添加样式

按钮点击案例

```javascript
<body>
    <button>按钮1</button>
    <button>按钮2</button>
    <button>按钮3</button>
    <button>按钮4</button>
    <button>按钮5</button>
    <button>按钮6</button>
    <script>
        var btn = document.querySelectorAll('button');
        // console.log(btn);
        for (var i = 0; i < btn.length; i++) {
            btn[i].onclick = function() {
                //当我点击某个按钮时，先去掉所有的按钮背景颜色
                for (var i = 0; i < btn.length; i++) {
                    btn[i].style.backgroundColor = '';
                }
                //给当前的按钮设置背景颜色
                this.style.backgroundColor = 'pink';
            }
        }
    </script>
</body>
```

**获取自定义属性值**

```javascript
//获取元素的自定义属性值
element.getAttribute('属性') 

<div myclass="1"></div>
    <script>
        var div = document.querySelector('div');
        console.log(div.getAttribute('myclass'));// 1
    </script>

```

**设置属性值**

```javascript
// 设置自定义属性值
element.setAttribute('属性','值')

    <div myclass="1"></div>
    <script>
        var div = document.querySelector('div');
        div.setAttribute('myclass','3');
        console.log(div.getAttribute('myclass'));// 3
    </script>
```

**移除属性**

```javascript
element.removeAttribute('属性')

    <div myclass="1"></div>
    <script>
        var div = document.querySelector('div');
        div.setAttribute('myclass','3');
        console.log(div.getAttribute('myclass'));// 3
        div.removeAttribute('myclass');
        console.log(div.getAttribute('myclass'));// null
    </script>
```

**H5自定义属性**

```javascript
//之所以要自定义属性，因为有些数据可以保存在页面上不用保存在数据库中。
//有些自定义属性容易引起歧义，不确定是自定义属性还是内置属性
H5标准data-属性开头作为属性名
//获取h5自定义属性(新增)
element.dataset.属性
dataset是一个集合，里面存放了所有以dataset开头的属性。
    <div getTime="20" data-index="2" data-list-name="andy"></div>
    <script>
        var div = document.querySelector('div');
        // console.log(div.getTime);
        console.log(div.getAttribute('getTime'));
        div.setAttribute('data-time', 20);
        console.log(div.getAttribute('data-index'));
        console.log(div.getAttribute('data-list-name'));
        // h5新增的获取自定义属性的方法 它只能获取data-开头的
        // dataset 是一个集合里面存放了所有以data开头的自定义属性
        console.log(div.dataset);
        console.log(div.dataset.index);
        console.log(div.dataset['index']);
        // 如果自定义属性里面有多个-链接的单词，我们获取的时候采取 驼峰命名法
        console.log(div.dataset.listName);
        console.log(div.dataset['listName']);
    </script>
```



**tab栏切换**

```javascript

```

### 节点操作

为了能更加方便的获取元素，让元素之间的逻辑性更强。我们可以采用节点的方式获得元素。

**获取父节点和子节点**

```javascript
// 父子节点 element.parentNode
// 得到的是离element最近的父节点，找不到就返回null
// 子节点 parentNode.childNode
// 得到的是所有节点，包括元素节点 文本节点
// 如果只想得到元素节点，需要进行特殊处理，不提倡使用。
// parentNode.children 得到所有的子元素节点
```

**获取第一个子节点和最后一个子节点**

```javascript
// parentNode.firstChild 得到的是第一个子节点，不一定是元素节点。
// parentNode.firstElementChild 得到第一个子元素节点 伪数组
// parentNode.lastElementChild 得到最后一个子元素节点
// 但是这个方法存在兼容性问题。
// 我们更推荐用伪数组的方法得到。 parentNode.children[0] 得到第一个元素节点  parentNode.children[parentNode.children.length - 1] 得到最后一个元素节点
```

**案例 下拉菜单**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        
        li {
            list-style-type: none;
        }
        
        a {
            text-decoration: none;
            font-size: 14px;
        }
        
        .nav {
            margin: 100px;
        }
        
        .nav>li {
            position: relative;
            float: left;
            width: 80px;
            height: 41px;
            text-align: center;
        }
        
        .nav li a {
            display: block;
            width: 100%;
            height: 100%;
            line-height: 41px;
            color: #333;
        }
        
        .nav>li>a:hover {
            background-color: #eee;
        }
        
        .nav ul {
            display: none;
            position: absolute;
            top: 41px;
            left: 0;
            width: 100%;
            border-left: 1px solid #FECC5B;
            border-right: 1px solid #FECC5B;
        }
        
        .nav ul li {
            border-bottom: 1px solid #FECC5B;
        }
        
        .nav ul li a:hover {
            background-color: #FFF5DA;
        }
    </style>
</head>

<body>
    <ul class="nav">
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
    </ul>
    <script>
        // 1. 获取元素
        var nav = document.querySelector('.nav');
        var lis = nav.children;
        for (var i = 0; i < lis.length; i++) {
            lis[i].onmouseover = function() {
                this.children[1].style.display = 'block';
            }
            lis[i].onmouseout = function() {
                this.children[1].style.display = 'none';
            }
        }
    </script>
</body>
</html>
```

**获取兄弟节点**（不常用）

```javascript
// nextSibling得到的是下一个兄弟节点，包括文本节点
// previousSibling 得到的是上一个兄弟节点，包括文本节点
// nextelementSibling 得到下一个兄弟元素节点
// previouselementSibling 得到上一个兄弟元素节点
```

**创建节点**

```javascript
// 动态创建元素节点
document.createElement('元素节点')
```

**添加节点**

```javascript
父节点.appendChild(child) append是追加元素，类似于数组的push
父节点.insertBefore(child,指定元素) 添加到指定元素的前面。
    <ul>
        <li>123</li>
    </ul>
    <script>
        // 创建新的元素节点
        var li = document.createElement('li');
        //添加到ul里面
        var ul = document.querySelector('ul');
        ul.appendChild(li);// 添加到第一个li的后面
        var lis = document.createElement('li');
        ul.insertBefore(lis, ul.children[0]);
    </script>
```

案例 简单发布留言案例

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        
        body {
            padding: 100px;
        }
        
        textarea {
            width: 200px;
            height: 100px;
            border: 1px solid pink;
            outline: none;
            resize: none;
        }
        
        ul {
            margin-top: 50px;
        }
        
        li {
            width: 300px;
            padding: 5px;
            background-color: rgb(245, 209, 243);
            color: red;
            font-size: 14px;
            margin: 15px 0;
        }
    </style>
</head>

<body>
    <textarea name="" id=""></textarea>
    <button>发布</button>
    <ul>
    </ul>
    <script>
        // 1. 获取元素
        var btn = document.querySelector('button');
        var text = document.querySelector('textarea');
        var ul = document.querySelector('ul');
        //注册事件
        btn.onclick = function() {
            if (text.value == '') {
                alert('你没有输入内容');
                return false;
            } else {
                var li = document.createElement('li');
                li.innerHTML = text.value;
                //添加节点
                ul.insertBefore(li, ul.children[0]);
            }
        }
    </script>
</body>
</html>
```

**删除节点**

```javascript
父节点.removeChild(删除的节点)，返回删除的节点
    <button>删除</button>
    <ul>
        <li>熊大</li>
        <li>熊二</li>
        <li>光头强</li>
    </ul>
    <script>
        //获取元素
        var ul = document.querySelector('ul');
        // ul.removeChild(ul.children[0]);
        var btn = document.querySelector('button');
        btn.onclick = function() {
            if (ul.children.length == 0) {
                this.disabled = true;//当ul里面没有元素时，就禁用删除按钮
            } else {
                ul.removeChild(ul.children[0]);
            }
        }
    </script>
```

**删除留言案例**

```javascript
        // 1. 获取元素
        var btn = document.querySelector('button');
        var text = document.querySelector('textarea');
        var ul = document.querySelector('ul');
        // 2. 注册事件
        btn.onclick = function() {
            if (text.value == '') {
                alert('您没有输入内容');
                return false;
            } else {
                // console.log(text.value);
                // (1) 创建元素
                var li = document.createElement('li');
                // 先有li 才能赋值
                li.innerHTML = text.value + "<a href='javascript:;'>删除</a>";//阻止链接跳转可以用javascript:void(0);或者javascript:;
                // (2) 添加元素
                // ul.appendChild(li);
                ul.insertBefore(li, ul.children[0]);
                // (3) 删除元素 删除的是当前链接的li  它的父亲
                // var as = document.querySelectorAll('a');
                // for (var i = 0; i < as.length; i++) {
                //     as[i].onclick = function() {
                //         ul.removeChild(this.parentNode);
                //     }
                // }
                var a = document.querySelector('a');
                a.onclick = function() {
                    ul.removeChild(a.parentNode);
                }
            }
        }
```

**克隆节点**

```javascript
// node.cloneNode()// 浅拷贝 只拷贝节点node，不拷贝节点中的内容
// node.cloneNode(true) 深拷贝，拷贝节点node和节点中的内容
```

**动态生成表格**

```javascript

```

**三种创建元素的方式对比**

```javascript
// innerHTML document.creatElement() document.write()
// 1.document.write()是直接将内容写进页面的内容流 文档流执行完毕后，他会导致页面重绘。
// 2.innerHTML是将内容写进一个DOM节点中，不会页面重绘。创建多个元素若使用数组的方式拼接，则效率更高
// 3.document.creatElement()创建多个元素的效率较低，但结构更清晰。
```

数组方式创建多个元素

```javascript
    <button>点击</button>
    <p>abc</p>
    <div class="inner"></div>
    <div class="create"></div>
    <script>
        // 2. innerHTML 创建元素
        var inner = document.querySelector('.inner');
        // for (var i = 0; i <= 100; i++) {
        //     inner.innerHTML += '<a href="#">百度</a>'
        // }
        var arr = [];
        for (var i = 0; i <= 100; i++) {
            arr.push('<a href="#">百度</a>');
        }
        inner.innerHTML = arr.join('');
    </script>
```

### 事件高级

**绑定事件的两种方法**

传统方式：

* 利用on开头的事件onclick
* `<button onclick='alert('nihao)'></button>`

* `btn.onclik = function(){}`
* 传统方式一个元素只能注册一个事件

方法监听注册方式

* `addEventListener()方法`
* 这种方式可以给一个元素注册多个事件
* 该方法接收三个参数 type listener useCapture

```javascript
// type 事件类型字符串 比如click mouseover 不加on
// listener 事件处理函数 事件发生后会调用该监听函数
// useCapture 可选参数 是一个布尔值 默认false 
    <button>方法监听注册事件</button>
    <script>
       var btn = document.querySelector('button');
    //    btn.onclick = function() {
    //     alert('传统方式');
    //    }
        btn.addEventListener('click', function() {//事件类型要加引号
            alert('你好');
        })
        btn.addEventListener('click', function() {//事件类型要加引号
            alert('第二次');
        })
    </script>
```

**删除事件**

传统方式

* `onclick = null`

方法监听事件方式

* `removeEventListener(type,listener,useCapture)`

```javascript
    <div>1</div>
    <div>2</div>
    <script>
       var div = document.querySelectorAll('div');
       //传统方式
       div[0].onclick = function() {
        alert(11);
        this.onclick = null;
       }
       //方法监听事件
       div[1].addEventListener('click', fn)// 注意这里的监听事件只写函数，不加括号
       function fn() {
        alert(11);
        div[1].removeEventListener('click',fn);
       }
    </script>
```

**DOM事件流**

事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程就是DOM事件流。

<img src="https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220810214631443.png" alt="image-20220810214631443" style="zoom: 67%;" />

JS代码只能执行捕获和冒泡其中一个阶段。

`onclick` 只能得到冒泡阶段

`addEventListener()`第三个参数如果是``true`，表示在事件捕获阶段调用事件处理程序，如果是默认，则在事件冒泡阶段调用事件处理程序。

在实际开发中，我们更关心事件冒泡。



>  为什么我给父元素绑定一个事件，它的子元素也能调用这个事件？

**事件对象**

```javascript
    <div>1</div>
    <script>
        var div = document.querySelector('div');
        //事件对象 是 我们事件的一系列相关数据的集合 跟事件相关的 比如鼠标点击里面就包含了鼠标的相关信息，鼠标坐标啊，如果是键盘事件里面就包含的键盘事件的信息 比如 判断用户按下了那个键
        // div.onclick = function(e) {// 这里的e就是事件对象 写在函数里面的参数 不需要传递实参
        //     console.log(e);
        // }
        div.addEventListener('click', function(e){
            console.log(e);
        })
    </script>
</body>
// 事件对象常见的属性和方法
target 触发事件的元素对象 点击了谁谁就是target
注意它和this的区别，this返回的是绑定事件的元素对象
    <ul>
        <li>abc</li>
        <li>abc</li>
        <li>abc</li>
    </ul>
//js代码
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
                // 我们给ul 绑定了事件  那么this 就指向ul  
                console.log(this);
                // e.target 指向我们点击的那个对象 谁触发了这个事件 我们点击的是li e.target 指向的就是li
                console.log(e.target);

            })
type 返回事件类型 不加on
preventDefault() 阻止默认事件 让链接不能跳转 提交按钮不能提交
stopPropagation() 阻止冒泡

```





## BOM



## **ES6新特性**



## **正则表达式**