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

**事件委托**

事件委托，又称为事件代理

事件委托的原理：不要给每个子节点单独设置事件监听器，而是将事件监听器绑定在父节点上面，通过冒泡原理影响设置每个子节点。

事件委托的作用：只操作了一次DOM，提高程序的性能。

```javascript
    <ul>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
    </ul>
    <script>
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
            // 排他思想
            for (var i = 0; i < this.children.length; i++) {
                this.children[i].style.background = '';
            }
            //e.target 返回触发事件的对象
            e.target.style.background = 'pink';
        })
    </script>
```

**两个鼠标事件**

* 禁止选中文字 `selectstart`
* 禁止右键菜单 `contextmenu`

```javascript
    我不能被复制和选中
    <script>
        //禁止选中文字
        document.addEventListener('selectstart', function(e) {
            e.preventDefault() // 阻止默认事件       
        })
        //禁止右键菜单
        document.addEventListener('contextmenu', function(e) {
            e.preventDefault()        
        })
    </script>
```

**鼠标事件对象** `MouseEvent`

| 鼠标事件对象 | 说明                                  |
| ------------ | ------------------------------------- |
| e.clientX    | 返回鼠标相对于浏览器可视化窗口的x坐标 |
| e.clientY    | 返回鼠标相对于浏览器可视化窗口的Y坐标 |
| **e.pageX**  | 返回鼠标相对于文档页面的x坐标         |
| **e.pageY**  | 返回鼠标相对于文档页面的Y坐标         |
| e.screenX    | 返回鼠标相对于电脑屏幕的x坐标         |
| e.screenY    | 返回鼠标相对于电脑屏幕的Y坐标         |

```javascript
    <script>
        // 鼠标事件对象 MouseEvent
        document.addEventListener('click', function(e) {
            // 1. client 鼠标在可视区的x和y坐标
            console.log(e.clientX);
            console.log(e.clientY);
            console.log('---------------------');

            // 2. page 鼠标在页面文档的x和y坐标
            console.log(e.pageX);
            console.log(e.pageY);
            console.log('---------------------');

            // 3. screen 鼠标在电脑屏幕的x和y坐标
            console.log(e.screenX);
            console.log(e.screenY);

        })
    </script>
```

```javascript
// 跟随鼠标移动的图片 给整个页面绑定鼠标移动事件，利用e.pageX,e.pageY得到鼠标的实时坐标，将坐标赋给图片的left,top即可。
    <img src="images/angel.gif" alt="">
    <script>
        var pic = document.querySelector('img');
        document.addEventListener('mousemove', function(e) {
            // 1. mousemove只要我们鼠标移动1px 就会触发这个事件
            // console.log(1);
            // 2.核心原理： 每次鼠标移动，我们都会获得最新的鼠标坐标， 把这个x和y坐标做为图片的top和left 值就可以移动图片
            var x = e.pageX;
            var y = e.pageY;
            console.log('x坐标是' + x, 'y坐标是' + y);
            //3 . 千万不要忘记给left 和top 添加px 单位
            pic.style.left = x - 50 + 'px';
            pic.style.top = y - 40 + 'px';
        });
    </script>
```

**键盘事件对象**

| 键盘事件   | 触发条件                                                  |
| ---------- | --------------------------------------------------------- |
| onkeyup    | 某个键盘按键松开时触发                                    |
| onkeydown  | 某个键盘按键按下时触发                                    |
| onkeypress | 某个键盘按键按下时触发 但是不识别功能键 CTRL 方向键 shift |

```javascript
// 三个事件的执行顺序  keydown -- keypress -- keyup
        document.addEventListener('keyup', function() {
            console.log('我弹起了');
        })
        document.addEventListener('keydown', function() {
            console.log('我按下了down');
        })
        document.addEventListener('keypress', function() {
            console.log('我按下了press');
        })
```

判断用户按下哪个键 `e.key`

```javascript
// 注意我们不再使用keyCode属性了。
        document.addEventListener('keyup', function(e) {
            console.log(e.key);
        })
```

**案例 模拟京东按键输入内容**

当我们按下s键，光标就定位到搜索框

```javascript
    <input type="text">
    <script>
        var input = document.querySelector('input');
        document.addEventListener('keyup', function(e) { //不要用down press 会将s填入光标中
            // console.log(e.key);
            if (e.key === 's') {
                input.focus();// 获得光标
            }
        })
    </script>
```

**案例 模拟京东快递单号查询案例**

当我们在文本框中输入内容时，文本框上面自动显示大字号的内容。

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
        
        .search {
            position: relative;
            width: 178px;
            margin: 100px;
        }
        
        .con {
            display: none;
            position: absolute;
            top: -40px;
            width: 171px;
            border: 1px solid rgba(0, 0, 0, .2);
            box-shadow: 0 2px 4px rgba(0, 0, 0, .2);
            padding: 5px 0;
            font-size: 18px;
            line-height: 20px;
            color: #333;
        }
        
        .con::before {
            content: '';
            width: 0;
            height: 0;
            position: absolute;
            top: 28px;
            left: 18px;
            border: 8px solid #000;
            border-style: solid dashed dashed;
            border-color: #fff transparent transparent;
        }
    </style>
</head>

<body>
    <div class="search">
        <div class="con">123</div>
        <input type="text" placeholder="请输入您的快递单号" class="jd">
    </div>
    <script>
        // 快递单号输入内容时， 上面的大号字体盒子（con）显示(这里面的字号更大）
        // 表单检测用户输入： 给表单添加键盘事件
        // 同时把快递单号里面的值（value）获取过来赋值给 con盒子（innerText）做为内容
        // 如果快递单号里面内容为空，则隐藏大号字体盒子(con)盒子
        var con = document.querySelector('.con');
        var jd_input = document.querySelector('.jd');
        document.addEventListener('keyup', function(e) {
            if (e.key == 's') {
                console.log(e.key);
                jd_input.focus();
            }
        })
        jd_input.addEventListener('keyup', function() {// 不能用keydown 放大的文本框内容总是比输入的内容少一个
                // console.log('输入内容啦');
                if (this.value == '') {
                    con.style.display = 'none';
                } else {
                    con.style.display = 'block';
                    con.innerText = this.value;
                }
            })
            // 当我们失去焦点，就隐藏这个con盒子
        jd_input.addEventListener('blur', function() {
                con.style.display = 'none';
            })
            // 当我们获得焦点，就显示这个con盒子
        jd_input.addEventListener('focus', function() {
            if (this.value !== '') {
                con.style.display = 'block';
            }
        })
    </script>
</body>
```



## BOM

> 浏览器对象模型 核心对象是`Window`

### BOM概述

`DOM`和`BOM`的对比

* `DOM`是把文档当作对象来看待，主要是操作页面元素 ，标准是`W3C` ，兼容性较好
* `BOM`是把浏览器当作对象来对待，学习的是浏览器窗口交互的一些对象 ，兼容性差

`BOM`的构成

`window`对象是浏览器的顶级对象，具有双重角色。

1. 它是`js`访问浏览器窗口的一个借口
2. 它是一个全局对象，定义在全局作用域的函数，变量自动变成`window`对象下的方法和属性。

> window有一个属性叫做name,因此前面变量部分说过不建议将变量命名成name。

  ### 常用事件

**窗口加载事件**

`window.onload = function()`

`window.addEventListener('load',function(){})`

当文档内容完全加载完成后才会触发这个事件。我们就可以利用这个事件，将js代码写在页面元素的上面。

> DOMContentLoaded事件当DOM元素加载完成后就会触发。页面图片比较多，可以使用这个事件。

**调整窗口大小事件**

`window.onresize  = function()`

`window.addEventListener('resize', function(){})`

窗口大小发生变化就会触发这个事件。

经常利用这个事件完成响应式布局。 `window.innerWidth` 屏幕宽度

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <script>
        window.addEventListener('load', function() {
            var div = document.querySelector('div');
            window.addEventListener('resize', function() {
                console.log(window.innerWidth);

              //  console.log('变化了');
                if (window.innerWidth <= 800) {
                    div.style.display = 'none';
                } else {
                    div.style.display = 'block';
                }

            })
        })
    </script>
    <div></div>
</body>
</html>
```



### 定时器

**setTimeout()**

`window.setTimeout(调用函数，延迟的毫秒数)`

>里面的调用函数可以只写函数名，也可以直接写函数。
>
>window可写可省略

```javascript
        function callback() {
            console.log('爆炸了');
        }
        var timer1 = setTimeout(callback, 3000);
        var timer2 = setTimeout(callback, 5000);
		var timer3 = setTimeout(function(){
            console.log('爆炸了');
        }, 7000);
// 我们要给定时器起个名字，区分不同的定时器。
```

> 回调函数
>
> 定时器里面的函数又叫回调函数。回头去调用。
>
> onclick 里面的函数也是回调函数

**案例 5秒自动关闭广告**

```javascript
    <img src="images/ad.jpg" alt="" class="ad">
    <script>
        var ad = document.querySelector('.ad');
        setTimeout(function() {
            ad.style.display = 'none';
        }, 5000);
    </script>
```

**停止`setTimeout`定时器**

`clearTimeout(定时器的名字)`

```javascript
    <button>点击停止定时器</button>
    <script>
        var btn = document.querySelector('button');
        var timer = setTimeout(function() {
            console.log('爆炸了');

        }, 5000);
        btn.addEventListener('click', function() {
            clearTimeout(timer);
        })
    </script>
```

**setInterval()**

该方法可以重复调用一个函数，每隔一段时间就去调用这个函数。

```javascript
        setInterval(function() {
            console.log('继续输出');

        }, 1000);
```

**案例 倒计时**

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            margin: 200px;
        }
        
        span {
            display: inline-block;
            width: 40px;
            height: 40px;
            background-color: #333;
            font-size: 20px;
            color: #fff;
            text-align: center;
            line-height: 40px;
        }
    </style>
</head>

<body>
    <div>
        <span class="hour">1</span>
        <span class="minute">2</span>
        <span class="second">3</span>
    </div>
    <script>
        // 1. 获取元素 
        var hour = document.querySelector('.hour'); // 小时的黑色盒子
        var minute = document.querySelector('.minute'); // 分钟的黑色盒子
        var second = document.querySelector('.second'); // 秒数的黑色盒子
        var inputTime = +new Date('2019-5-1 18:00:00'); // 返回的是用户输入时间总的毫秒数
        countDown(); // 我们先调用一次这个函数，防止第一次刷新页面有空白 
        // 2. 开启定时器
        setInterval(countDown, 1000);

        function countDown() {
            var nowTime = +new Date(); // 返回的是当前时间总的毫秒数
            var times = (inputTime - nowTime) / 1000; // times是剩余时间总的秒数 
            var h = parseInt(times / 60 / 60 % 24); //时
            h = h < 10 ? '0' + h : h;
            hour.innerHTML = h; // 把剩余的小时给 小时黑色盒子
            var m = parseInt(times / 60 % 60); // 分
            m = m < 10 ? '0' + m : m;
            minute.innerHTML = m;
            var s = parseInt(times % 60); // 当前的秒
            s = s < 10 ? '0' + s : s;
            second.innerHTML = s;
        }
    </script>
</body>
</html
```

停止`setInterval`定时器

`clearInterval(定时器的名字)`

```javascript
    <button class="begin">开启定时器</button>
    <button class="stop">停止定时器</button>
    <script>
        var begin = document.querySelector('.begin');
        var stop = document.querySelector('.stop');
        var timer = null; // 全局变量  null是一个空对象
        begin.addEventListener('click', function() {
            timer = setInterval(function() {
                console.log('ni hao ma');

            }, 1000);
        })
        stop.addEventListener('click', function() {
            clearInterval(timer);
        })
    </script>
```

**发送短信案例**

点击按钮后，该按钮60秒内不能再次点击，防止重复发短信。

```javascript
    手机号码： <input type="number"> <button>发送</button>
    <script>
        var btn = document.querySelector('button');
        btn.addEventListener('click', function(){
            var time = 5;
            btn.disabled = true;
            var timer = setInterval(function(){
                if (time == 0) {
                    clearInterval(timer);// 清除定时器
                    btn.disabled = false;
                    btn.innerHTML = '发送';
                } else {
                    btn.innerHTML = '还剩' + time + '秒才能重新发送';
                    time--;
                    }
            }, 1000)
        })
    </script>
```

**this指向**

一般情况下谁调用对象，`this`就指向这个调用者。

1. 全局作用域下或普通函数中`this`指向全局对象`window`
2. 方法调用谁调用`this`指向谁
3. 构造函数`this`指向实例化的对象

### JS执行队列

`js`是单线程，同一时间只能做一件事。所有的任务都需要排队。

HTML5提出允许`js`创建多个线程，出现了同步和异步。

**同步**

程序的执行顺序和任务的排列顺序相同。

**异步**

同时做多个任务

```javascript
        console.log(1);

        setTimeout(function() {

            console.log(3);

        }, 1000);

        console.log(2); //  1 2 3
```

**同步任务**

同步任务放到执行栈中。

**异步任务**

`js`的异步是通过回调函数实现的。

执行过程

* 先执行同步任务
* 异步任务放入任务队列（消息队列）中
* 执行栈中的同步任务执行完毕后，系统按照顺序依读取任务队列中的异步任务，异步任务进入执行栈，开始执行。

```javascript
        console.log(1);

        setTimeout(function() {

            console.log(3);

        }, 0);

        console.log(2); // 1 2 3
```



**js的执行机制**

>  多个异步任务该如何执行。 这就涉及到了js的执行机制。

执行机制原理图

<img src="https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220813102535117.png" alt="image-20220813102535117" style="zoom: 67%;" />

```javascript
        console.log(1);
        document.onclick = function() {
            console.log('click');
        }
        console.log(2);
        setTimeout(function() {
            console.log(3)
        }, 3000) // 1 2 3 最后点击鼠标，打印出click，若三秒内点击，则先打印出click，最后输出3.
```

执行过程分析：

首先执行栈将click和定时器交给异步进程处理，先执行同步任务，打印出1 2 。同步任务执行完毕后去任务队列看还有没有异步任务，3秒后异步进程处理将定时器推入任务队列中，然后进入主线程执行该任务。当点击鼠标后，onclick事件推入任务队列，主线程查看任务队列有没有异步任务，然后进入主线程执行该任务。

总之遇到多个异步任务，谁先进入任务队列，谁先执行。

### 常用对象

`location`对象

获取和设置窗口的`URL`。

> URL 统一资源定位符   它包含的信息指出文件的位置以及浏览器怎么处理它。

<img src="https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220813104357059.png" alt="image-20220813104357059" style="zoom:50%;" />

**`location`常用属性**

 `location.href`   获取整个URL或设置URL

`location.search` 返回参数

案例 5秒之后跳转页面

```javascript
    <div></div>
    <script>
        var div = document.querySelector('div');
        var time = 5;
        
        function fn() {
            div.innerHTML = '还剩' + time + '秒自动跳转页面';
            time--;
            if (time == 0){
            location.href = 'http://xubenshan.top';
            }
        }
        fn();// 在定时器前面先调用这个回调函数，防止刷新页面有空白。
        setInterval(fn, 1000);
    </script>
```

案例 获取URL参数数据

```javascript
location.search = '?uname=xubenshan'
得到login页面的登录信息，将它变成用户名xubenshan，同时还要保留uname。我们可以用substr将？去掉，用split将uname和xubenshan分隔开。
login页面
    <form action="index.html">
        用户名： <input type="text" name="uname">
        <input type="submit" value="登录">
    </form>
index页面
    <div></div>
    <script>
        console.log(location.search); // ?uname=xubenshan
        // 1.先去掉？  substr('起始的位置'，截取几个字符);
        var params = location.search.substr(1); 
        console.log(params); // uname=xubenshan
        // 2. 利用=把字符串分割为数组 split('=');
        var arr = params.split('=');
        console.log(arr); // ["uname", "xubenshan"]
        var div = document.querySelector('div');
        // 3.把数据写入div中
        div.innerHTML = arr[1] + '欢迎您';
    </script>
```

**`location`常用方法**

`location.assign(URL)` 跳转页面

`location.replace() ` 替换页面

`location.reload()` 重新加载页面  里面参数为`true`相对于强制刷新。

```javascript
    <button>点击</button>
    <div></div>
    <script>
        var btn = document.querySelector('button');
        btn.addEventListener('click', function() {
            // 记录浏览历史，所以可以实现后退功能
            // location.assign('http://www.xubenshan.top');
            // 不记录浏览历史，所以不可以实现后退功能
            // location.replace('http://www.xubenshan.top');
            location.reload(true);
        })
    </script>
```

`navigator`对象

包含浏览器的信息。

**常用属性**

`userAgent` 返回由客户机发送服务器的user-agent的头部的值。

判断用户哪个终端打开页面  了解即可

<img src="https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220813112440843.png" alt="image-20220813112440843" style="zoom:67%;" />

`history`对象

**常用的方法**

`history.forward()` 前进

`history.back()`  后退

`history.go(前进或后退几页)`





