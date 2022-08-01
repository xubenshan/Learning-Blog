# JavaScript学习笔记

## 简介

JavaScript是一种解释型脚本语言，可以嵌入到HTML中，它会由浏览器进行执行。

Java和JavaScript基本上毫无联系，只是当时Java名气很高，然后Javascript的开发者想借Java的名气来更好的推广这门语言。

>  学习JavaScript我使用的是vscode编辑器。

引入JavaScript有两种基本方式。

* 在`<head>..</head>`中添加`<script>..</script>`。
* 新建一个`.js`文件，然后在HTML中引入该文件。`<script src="js文件的位置" type="text/javascript">...</script>`
* 行内嵌入

```javascript

```

注释

```javascript
// 单行注释
快捷键 ctrl+/
/* */ 多行注释
快捷键 shift+alt+A
```



## 基本语法

### 输入和输出语句

```javascript
 <script>
        //用户可以输入内容
        prompt('请输入你的年龄');
        // 弹出警示框
        alert('展示给用户的');
        //控制台打印输出信息
        console.log('程序员看到的');
 </script>
```

> prompt 取过来的值是字符串型的。

### 数据类型和变量

#### 变量

```javascript
//变量
//内存中用来存放数据的空间
//声明变量 variable
var age;
//赋值
age = 18;
//输出
console.log(age);
//变量的初始化 声明的同时赋值
var myname = 'xubenshan';
console.log(myname);
//变量更新
以最后一次赋值为准
//同时声明多个变量 变量之间逗号隔开
var age = 18,
    myname = xubenshan;
//特殊情况
1.只声明不赋值
undefined 未定义的
2.直接使用 会报错
3.不声明，直接赋值使用 是可以的。会变成全局变量。
//变量命名规范
字母 数字 下划线 美元符号组成
区分大小写
不能以数字开头
不能以关键字开头
驼峰命名法 首字母小写 后面单词首字母大写
```

> 尽量不要以name作为变量名。它有特殊含义。

```javascript
//交换两个变量的值 临时变量法
var a = 100;
var b = 23;
var temp;
temp = a;
a = b;
b = temp;
console.log(a, b);
//结果 a=23 b=100
```

#### 数据类型

> 根据数据占用的存储空间不同，分成了不同的数据类型。
>
> js是弱语言，只有在程序运行的过程中根据赋值才能确认变量的数据类型
>
> js是动态语言，同一个变量可用作不同的类型

```javas
//5种简单数据类型
数字型 Number
布尔值 Boolean
字符串类型
undefined
null
```

* 数字型

```javas
// 数字型进制
八进制 0开头 0~7
十六进制 0x开头 0~9 a~f
//范围
console.log(Number.MAX_VALUE);最大值
console.log(Number.MIN_VALUE);最小值
Infinity  无穷大
-Infinity 负无穷
NaN 非数值
//isNaN() 用来判断非数字，并且返回一个布尔值。是数字 返回false 非数字 返回true
```

* 字符串型

```javascript
//推荐使用单引号
//字符串嵌套 外双内单 外单内双
//字符串转义符
\n 换行 \t tab缩进 \b 空格
// 获取字符串长度 length
var myName = 'xubenshan is ';
console.log(myName.length);
//输出13
//字符串拼接 + 字符串和其他类型进行拼接，结果仍然是个字符串
console.log('xu' + 'ben'); //xuben
console.log('xu' + 18); //xu18
//字符串拼接加强
var age = 18;
console.log('我今年' + age + '岁'); //我今年18岁
```

* 布尔型

```javascript
// true false
// true参与数值运算当1，false当0
```

* undefined

声明变量但是没有赋值

```javascript
 var number = undefined;
 console.log(number + 'xu'); //undefinedxu
 console.log(number + 1); //NaN
```

* null 空值

```javascript
var number = null;
console.log(number + 'xu'); //undefinedxu
console.log(number + 1); //1
```

```javascript
//获取变量类型 typeof
var age = 23;
var name = 'xubenshan'
console.log(typeof age); //number
console.log(typeof name); //string
```

```javascript
console.log(12);
console.log('xu');
console.log(null);
console.log(undefined);
console.log(true);
```

![image-20220801113951152](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220801113951152.png)

>  可以发现在控制台中白色是字符串型 数字型和布尔型是蓝色 null和undefined是灰色。

#### 数据类型转换

* 转换成字符串型

```javascript
//将数字型转换成字符串型toString
var num = 10;
var str = num.toString(num);
console.log(str);//10
console.log(typeof str);//string
// String()
console.log(String(num));//string
// +拼接 隐式转换
console.log(num + '');//string
```

* 转换成数字型

```javascript

```



* 转换成布尔型

### 运算符

### 流程控制

#### 条件判断

#### switch语句

### 循环

### 数组

### 函数

## **对象**



## jQuery

## Ajax



