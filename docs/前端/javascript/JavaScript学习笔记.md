# JavaScript学习笔记

> 2022年8月1号开始学习Javascript

## 简介

JavaScript是一种解释型脚本语言，可以嵌入到HTML中，它会由浏览器进行执行。

Java和JavaScript基本上毫无联系，只是当时Java名气很高，然后Javascript的开发者想借Java的名气来更好的推广这门语言。

>  学习JavaScript我使用的是vscode编辑器。

引入JavaScript有两种基本方式。

* 在`<head>..</head>`中添加`<script>..</script>`。
* 新建一个`.js`文件，然后在HTML中引入该文件。`<script src="js文件的位置" type="text/javascript">...</script>`
* 行内嵌入

```javascript
<input 
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
//parseInt() 转化成整数 
var age = prompt('输入你的年龄');
 console.log(parseInt(age)); 
 console.log(parseInt('3.14'));//3
 console.log(parseInt('3.94'));//3
 console.log(parseInt('320px'));//320
 console.log(parseInt('ym320px'));//NaN

//parseFloat() 转化成浮点数
 console.log(parseFloat('3.14'));//3.14

//Number()
  var num = '13';
  console.log(Number(num));
//隐式转换
  console.log('12' - 0);
  console.log('123' - '23');//100
  console.log('123' * 1);//123
```

* 转换成布尔型

```javascript
//Boolean()
console.log(Boolean('345')); //true
转化成false有五个 '' 0 NaN null undefined 
```

> 解释型语言和编译型语言的区别
>
> 计算机只认识机器语言，所以要把程序语言转化成机器语言才能执行。程序语言翻译成机器语言的工具就是翻译器。
>
> 翻译有两种方式 一个是编译 一个是解释。区别在于翻译的时间点不同。
>
> js属于解释型语言，边解释边执行
>
> Java属于编译型语言，先编译完毕再执行

**案例**

```javascript
// 在页面中弹出一个提示框，我们输入出生年份后，能计算出我们的年龄
var year = prompt('请输入你出生年份');
var age = 2022 - year;//year隐式转换成数值型
alert('你今年' + age + '岁');
// 计算两个数的值， 用户输入第一个数，继续弹出第二个输入框输入第二个数，最后弹出窗口显示两次输入的数的和
var num1 = prompt('请输入第一个数');
var num2 = prompt('请输入第二个数');
var num = parseInt(num1) + parseInt(num2);//注意进行数据类型转换
alert('两数之和为' + num);
```

### 运算符

```javascript
//算数运算符
+ - * / %
//前置递增和后置递增运算符 ++num num++
前置递增 先加后用 
后置递增 先用后加
var n = 13, m = 12;
console.log(n++, ++m);//13 13
console.log(n, m);//14 13
// 比较运算符
< > <= >= != 
  相等  == 会自动转换成相同的数据类型
console.log(18 == '18') // true
  全等  === 数值和类型完全一样
console.log(18 === '18') // false
//逻辑运算符
&&与   ||或 !非
&& 全真为真 有假则假
|| 有真则真 全假则假
//表达式参与的逻辑运算
//短路运算（逻辑中断）
记住一句话，总是返回能决定表达式布尔值的那个表达式
console.log(123 && 234); //234
console.log('' && 234);// ''
console.log(234 || 345) //234
console.log(0 || 345 || 456);//345
//赋值运算符
= 右边的值给左边
+= -= /= %=
//运算符的优先级 从高到低
小括号()
一元运算符++ ! --
算数运算符先* / % 后+-
关系运算符> < >= <=
相等运算符== != === !==
逻辑运算符先&& 再||
赋值运算符=
逗号运算符,    
```

## 流程控制

> 流程控制分为顺序结构 分支结构 循环结构

### 条件判断

```javascript
// if (条件) {
	执行的语句
}
条件为真，执行花括号里面的语句
//if else 双分支语句
if (条件) {
    //执行语句1
    } else {
    //执行语句2
}
条件为假，执行语句2
//接收用户输入的年份，如果是闰年就弹出闰年，否则弹出平年
  var year = prompt('请输入年份：');
  if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0) {
         alert('该年是闰年');
     } else {
         alert('该年是平年');
     }
//if else if 多分支语句
if (条件1) {
    执行语句1
} else if (条件2) {
    执行语句2
} else if (条件3) {
    执行语句3
} else {
    执行语句4
}

//案例 接收用户输入的分数，根据分数输出对应的等级字母A，B，C，D，E
其中90分以上，输出A
80——90 输出B
70-80 输出C
60-70 输出D
60以下 输出E
var score = prompt('请输入你的分数：');
if (score >=90 ) {
    alert('A');
} else if (score >= 80 ) {
    alert('B');
} else if (score >= 70) {
    alert('C');
} else if (score >= 60) {
    alert('D');
} else {
    alert('E');
}
//三元表达式 三个操作数
条件表达式?表达式1:表达式2
条件表达式为真 执行表达式1 为假 执行表达式2
//案例 用户输入数字，如果数字小于10，则在前面补0，如果数字大于10，则不用补零。
var num = prompt('请输入一个数字');
var res = num < 10 ? '0' + num : num;
console.log(res);
```

### switch语句

```javascript
//switch(表达式) {
case value1:
执行语句1;
break;
case value2:
执行语句2;
break;
...
default:
执行语句n;
}
//注意每个case语句中的break不能省略，break是跳出switch语句，否则会一直执行后面的case
//表达式中的值必须和case中的value全等，才能匹配上。
//案例 用户在弹出框中输入一个苹果，如果有就弹出该水果的价格，如果没有该水果，就弹出“没有此水果”
var fruit = prompt('请输入一个水果');
switch (fruit) {
    case '苹果':
        alert('苹果的价格是13斤');
        break;
    case '榴莲':
        alert('榴莲的价格是34斤');
        break;
    default:
        alert('没有此水果');
        }
//用户输入一个数，数字1到数字7，返回星期几。
var num = prompt('请输入一个数：');
        num = parseInt(num);//将字符型转换成数字型，和case数据类型匹配。
        switch (num) {
            case 1:
                alert('星期一');
                break;
            case 2:
                alert('星期二');
                break;
            case 3:
                alert('星期三');
                break;
             case 4:
                alert('星期四');
                break;
            case 5:
                alert('星期五');
                break;
             case 6:
                alert('星期六');
                break;
            case 7:
                alert('星期七');
                break;
        }
```

>  `if else` `switch`语句的区别
>
> 一般情况下可以进行替换
>
> switch语句通常处理case为比较确定值的情况，if else 语句更加灵活，常用于范围判断
>
> 分支少的时候 ，if else语句效率高，分支多的时候，switch语句效率高

### 循环

* `for`循环

```javascript
for (初始状态; 循环条件; 计数器变量增或减 ) {
    循环体;
} 
//for循环的执行顺序
 for (var i = 1; i <= 10; i++) {
     循环体
 }
先执行初始条件i = 1,满足循环条件，执行循环体；之后执行i++，此时i=2，满足循环条件，继续执行循环体。以此类推，直到不满足条件为止。
初始条件i=1只执行一次。
//案例 
//求1~100所有数的平均数
        var sum = 0;
        for (var i = 1; i <= 100; i++) {
            sum += i;
        }
        // var ans = sum / 100;
        console.log(sum / 100);
//求1~100所有偶数和奇数的和
		var sum1 = 0, sum2 = 0;
        for (var i = 1; i <= 100; i++) {
            if (i % 2) {
                sum1 += i;
            } else {
                sum2 += i;
            }
        }
        console.log(sum1, sum2);//奇数2500  偶数2550
//求1~100所有能被3整除的数字之和
        var ans = 0;
        for (var i = 0; i <= 100; i++) {
            if (i % 3 == 0) {
                ans += i;
            }
        }
        console.log(ans); //1683
//要求用户输入班级人数，之后依次输入每个学生的成绩，最后打印出该班级的总成绩和平均成绩
		var num = prompt('请输入班级的人数');
        var sum = 0;
        for (var i = 1; i <= num; i++) {
            // sum += prompt('输入第' + 'i' + '个学生的成绩');
            var temp = prompt('输入第' + i + '个学生的成绩');
            sum += parseInt(temp);
        }
        alert('该班总成绩为' + sum + '' + '平均成绩为' + sum / num);
//一行打印五个星星⭐ 利用字符串拼接
		var str = '';
		for (var i = 1; i <= 5; i++ ) {
            str += ⭐;
        }
		console.log(str);
//双重for循环
外层循环执行一次，内层循环执行全部
//打印五行五列的星星
		 var str = '';
		 for (var i = 1; i <= 5; i++) {
             for (var j = 1; j <= 5; j++) {
                str += '*'; 
				}
             str += '\n';
         }
		console.log(str);
//打印n行n列的星星
		var str = '';
		var res1 = prompt('请输入行数：');
		var res2 = prompt('请输入列数：');
		for (var i = 1; i <= res1; i++) {
            for (var j = 1; j <= res2; j++) {
                str += '*';
            }
            str += '\n';
        }
		console.log(str);
//打印倒三角形
   		var str = '';
		for (var i = 1; i <= 10; i++) {
             for (var j = 1; j <= 10 - i + 1; j++) {			  
            	str += '*';	
            }
            str += '\n';
        }
		console.log(str);
//打印正三角形
		var str = '';
		for (var i = 1; i <= 10; i++) {
            //for (var j = 10; j >= 11 - i ; j--) {
            for (var j = 1; j <= i; j++) {
            	str += '*';	
            }
            str += '\n';
        }
		console.log(str);
//九九乘法表
		var str = '';
		for (var i = 1; i <= 10; i++) {
            //for (var j = 10; j >= 11 - i ; j--) {
            for (var j = 1; j <= i; j++) {
            	str += j + '*' + i + '=' + i * j + ' ';	
            }
            str += '\n';
        }
		console.log(str);
```

> 断点调试的方法 debug
>
> 按F12打开开发者工具，选择`Sources`项，就能看到我们本地的源代码了。
>
> ![image-20220802162001444](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220802162001444.png)
> 

> 点击要断点的语句前面的序号，然后刷新一下。在右侧的watch点击+号，输入要监视的变量名，按F11程序往后执行，按shift+F11程序往前执行。在执行过程中可以实时的监控变量的值，找到程序的问题所在。
>
> ![image-20220802162824439](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220802162824439.png)



* `while`循环

```javascript
while循环 一定要防止死循环
//while (条件表达式) {
      循环体
     }
//表达式为真，执行循环体；
//案例
//打印一个人的一生，从1岁到100岁
     var i = 1;
     while (i <= 100) {
         console.log('他今年' + i + '岁了');
         i++;
     }

//计算1~100之间所有整数的和
var sum = 0;
var i = 1;
while (i <= 100) {
		sum += i;
    	i++;
	}
console.log(sum);
//弹出提示框，你好吗，如果输入我好，就提示结束，否则，一直询问
var ans = prompot('你好吗');
while (ans != '我好') {
   ans = prompot('你好吗');
}
```



* `do while`循环



* `continue`和`break`

  

## 数组



## 函数



## 作用域



## **对象**



## DOM



## BOM



## jQuery



## Ajax



