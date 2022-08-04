

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

### `switch`语句

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

#### `for`循环

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



#### `while`循环

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
var ans = prompt('你好吗');
while (ans !== '我好') {
   ans = prompt('你好吗');
}
alert ('回答正确');
```



#### `do while`循环

```javascript
do {
    循环体
} while (条件表达式)
    先执行一次循环体，再去进行条件判断，为真就继续循环
    //案例 打印一个人的一生，从1岁到100岁
    var i = 1;
    do {
        console('我今年' + i + '岁了');
        i++;
    } while (i <= 100)
    // 计算1~100之间所有整数的和
    var sum = 0;
	var i = 1;
	do {
        sum += i;
        i++;
    } while (i <= 100)
    console.log (sum);
	//弹出提示框，你好吗，如果输入我好，就提示结束，否则，一直询问
	do {
        var ans = prompt('你好吗');
    } while (ans !== '你好')
        alert('回答正确');
```



* `continue`和`break`

  ```javascript
  continue是跳出本次循环，继续执行下次循环。
  //求1~100之间，除了能被7整除之外的整数和
  var sum = 0;
  for (var i = 1; i <= 100; i++) {
      if (i % 7 == 0) {
          continue;
      }
      sum += i;
      console.log(sum);
  }
  `break`是跳出整个循环。不再执行该循环
  多层循环时，只能跳出当前层的循环
  ```

  ```javascript
  //综合案例
  里面存有100块钱，如果存钱，就用输入钱数加上先存的钱数，之后弹出显示余额提示框
  如果取钱，就减去取得钱数，之后弹出余额提示框
  如果显示余额，就输出余额
  如果退出，就弹出退出信息提示框
  		var sum = 100;
          var ans = prompt('请输入你要的操作:' + '\n1.存钱' + '\n2.取钱' + '\n3.显示余额' + '\n4.退出');
          while (ans != 4) {
              if (ans == 1) {
                 var ans1 = prompt('请输入你存的钱数');
                 sum = ans1 - 0 + sum;
                 alert('你现在的钱数为:' + sum);
                 
              }
              if (ans == 2) {
                  var ans2 = prompt('请您输入取的钱数');
                  if (sum >= ans2) {
                      sum = sum - ans2;
                  alert('你现在的钱数为:' + sum); 
                  } else {
                      alert('你的余额不足');
                  }
              }
              if (ans == 3) {
                  alert('余额为：' + sum);
              } 
              ans = prompt('请输入你要的操作:' + '\n1.存钱' + '\n2.取钱' + '\n3.显示余额' + '\n4.退出');
              
          }
         alert ('你已经退出，请重新登陆');
  ```

## **数组**

> 数组可以把一组相关的数据存放在一起，并且可以很方便的访问它们。

```javascript
// 创建数组
1. new
 var arr = new Araay();
2. 利用数组字面量
 var arr = [];
 var arr1 = [1, 2, 3];
 var arr2 = [1, 'xu', true];//数组中的元素可以是任意数据类型。
// 遍历数组 数组下标从0开始 所谓的遍历数组就是说将数组中的元素依次访问一遍
var arr = [1, 2, 3];
for (var i = 0; i < arr.length; i++) { //变量名.length动态获取数组的长度
    console.log(arr[i]);
}
// 求数组的最大值
		var arr = [1, 2, 3, 4, 56, 45];
        var max = arr[0];
        for (var i = 1; i < arr.length; i++) {
            if (arr[i] > max) {
                max = arr[i];
            }
        }
        console.log(max);
// 数组转化为分割字符串
		var arr = ['xu', 'ben', 'shan'];
        var str = '';
        var temp = '|';
        for (var i = 0; i < arr.length; i++ ) {
            str = str + arr[i] + temp;
        }
        console.log(str);   //xu|ben|shan|

// 数组新增元素 
 索引号增加元素
	    var arr = ['xu', 'ben', 'shan'];
        console.log(arr[3]);// undefined
        arr[3] = 'blog';
        console.log(arr[3]);// blog
        console.log(arr.length);// 4
// 数组存放1~10个值
		var arr = [];
		for (var i = 0; i < 10; i++) {
   		 	arr[i] = i + 1;
			console.log(arr[i]);
		} // 1 2 3 4 5 6 7 8 9 10

//将数组[2, 0, 6, 1, 77, 0, 25, 7]中大于等于10的元素选出来，放入新数组。
	   var arr = [2, 0, 6, 1, 77, 0, 25, 7];
       var newarr = [];
       var j = 0;
       for (var i = 0; i < arr.length; i++) {
        if (arr[i] > 10) {
            newarr[j] = arr[i];
            j++;
        }
       }
       console.log(newarr);
法二：不用引进新变量
 var arr = [2, 0, 6, 1, 77, 0, 25, 7];
       var newarr = [];
       for (var i = 0; i < arr.length; i++) {
        if (arr[i] > 10) {
            newarr[newarr.length] = arr[i];
        }
       }
       console.log(newarr);
// 删除数组指定元素 （数组去重）
// 将数组[2, 0, 6, 1, 77, 0, 52, 0, 25, 7]中的0去除掉，形成一个不含0的新数组。
	   var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
       var newarr = [];
       for (var i = 0; i < arr.length; i++) {
            if (arr[i]) {
                newarr[newarr.length] = arr[i];
            }
       }
       console.log(newarr);

//翻转数组
	   var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
       var newarr = [];
       for (var i = arr.length - 1; i >= 0; i--) {
            newarr[newarr.length] = arr[i];
       }
		console.log(newarr);
```

> 在JavaScript中，数组下标越界，不会报错，访问越界的元素会显示undefined。

**冒泡排序**

```javascript
var arr = [5, 3, 7, 2, 1];
for (var i = 1; i < arr.length; i++) {
    for (var j = 0; j < arr.length - i; j++) {
        if (arr[j] > arr[j + 1]) {
			var temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
        }
    }
}
console.log(arr);
```

## **函数**

> 函数就是封装一段可以重复使用的代码块， 提高代码复用。

```javascript
//函数使用分两步 声明函数和调用函数
声明函数有两种方式：
1.关键字function声明函数 命名函数
function 函数名（参数1，参数2...）{
		函数体
}
函数名();
2.函数表达式 匿名函数
var 变量名 = function(参数1， 参数2...){函数体};
变量名();
函数只有调用的时候才被执行
//形参和实参
 形参 函数声明时的参数
 实参 函数调用时的参数
//return返回
1. return只能返回一个值，如果用逗号隔开，以最后一个值为准。要返回多个值的时候可以用数组
2. 函数无return时，默认返回undefined。
3. return后面的语句不会被执行
//arguments的使用
当我们不确定有多少个参数传递的时候，可以用arguments。
arguments是函数的一个内置对象，存储了传递过来的所有实参。
arguments是一个伪数组，因此可以进行遍历。
伪数组的特点：
1.具有length属性
2.可以通过索引号访问伪数组里面的元素
3.没有数组的一些方法，如pop(),push()等
        function fn() {
            console.log(arguments); // [1,2,3]
            console.log(arguments.length); // 3
            console.log(arguments[2]);// 3
       }
       fn(1, 2, 3);
//案例 利用函数求任意个数的最大值
		function max() {
            var res = arguments[0];
            for (var i = 1; i < arguments.length; i++) {
                if (arguments[i] > res) {
                    res = arguments[i];
                }
            }
            return res;
        }
        console.log(max(1, 5, 3)); // 5
		console.log(max(2,4,1,6,7)); // 7
// 利用函数封装的方式，翻转任意一个数组
		function reverse(arr) {
            var newArr = [];
            for (var i = arr.length - 1 ; i >= 0; i--) {
                newArr[newArr.length] = arr[i];
            }
            return newArr;
        }
        console.log(reverse([2, 3, 4, 5]));
// 函数封装冒泡排序
	function sort(arr) {
        for (var i = 1; i < arr.length; i++) {
            for (var j = 0; j < arr.length - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    var temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
        return arr;
    }
    console.log(sort([1, 2, 5, 3, 1, 8]));
// 利用函数判断闰年 闰年：能被4整除并且不能被100整除，或者能被400整除
		function isRunYear(year) {
            var flag = false;
            if (year % 4 == 0 && year % 100 || year % 400 == 0 ) {
                flag = true;
            } 
            return flag;

        }
        console,log(isRunYear(2022));
        console,log(isRunYear(2000));
 函数之间可以相互调用
// 用户输入年份，输出当前年份2月份天数
 		 function isRunYear(year) {
            var flag = false;
            if (year % 4 == 0 && year % 100 || year % 400 == 0 ) {
                flag = true;
            } 
            return flag;

        }
        function backDay() {
        var year = prompt('请输入一个年份');
        if (isRunYear(year)) {
            alert('该年份2月份有29天');
        } else {
            alert('该年份2月份有28天');
        }
    }
        backDay();
```

## **作用域**

```javascript
// 作用域
代码名字在某个范围内起作用和效果。目的提高程序的可靠性，减少命名冲突。
全局作用域：整个<script>标签，或者单独的一个js文件
局部作用域：在某个函数内部有效
	   var num = 10;// 全局变量 作用域是全局作用域
       function fn() {
        var num = 20;
            num1 = 30;//注意在函数内部直接赋值没有声明的变量也是全局变量（不建议使用）
        console.log(num);// 局部变量 作用域是局部作用域
       }
       fn();// 20
       console.log(num);// 10  
	   console.log(num1);// 30
// 全局变量 只有浏览器关闭之后才被销毁，比较占内存
// 局部变量 当含局部变量的代码块执行完毕后，就被销毁
// 作用域链 内部函数访问外部变量采用就近原则
	   var num = 10;
       function fn() {
        var num = 20;
        function fn1() {
            console.log(num);// 20
        }
        fn1();
       }
       fn();
```

## **预解析**

```javascript
// 解释器运行js分为两步：预解析和代码执行
// 1.预解析 js引擎会将js里面所有的var还有function提升到当前作用域的最前面。
// 2.代码执行 从上到下按顺序执行代码
// 3.预解析分为变量预解析和函数预解析
变量预解析（变量提升） 把所有的变量声明提升到当前作用域的最前面，不提升赋值操作。
console.log(num);
var num = 10;
//上述代码先进行预解析，将变量声明提升到前面去。变成：
var num;
console.log(num);
num = 10;
显然输出为 undefined
函数预解析（函数提升） 把所有的函数声明提升到当前作用域的最前面，不调用函数。
fn();
function fn() {
	console.log(11);
}
//进行预解析，将函数声明提升到前面。变成：
function fn(){
    console.log(11);
}
fn();
//显然输出为11.
fn();
var fn = function(){
    console.log(11);
}//该程序会报错，因为预解析后变成：
var fn;
fn();
fn = function(){
    console.log(11);
}//显然fn还未赋值，就进行使用，会报错
//因此我们在利用函数表达式使用函数时，要先进行声明，才可以调用。

```

```javascript
// 案例
```





## **对象**



## 正则表达式



## **DOM**



## **BOM**



## ES6新特性



## **jQuery**



## Ajax



