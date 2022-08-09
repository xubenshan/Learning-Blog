# JavaScript学习笔记

## **简介**

JavaScript是一种解释型脚本语言，可以嵌入到HTML中，它会由浏览器进行执行。

Java和JavaScript基本上毫无联系，只是当时Java名气很高，然后Javascript的开发者想借Java的名气来更好的推广这门语言。

>  学习JavaScript我使用的是vscode编辑器。

引入JavaScript有三种基本方式。

* 在`<head>..</head>`中添加`<script>..</script>`。
* 新建一个`.js`文件，然后在HTML中引入该文件。`<script src="js文件的位置" type="text/javascript">...</script>`
* 行内嵌入，直接写在元素里面

```javascript
<input type="button" value="点击" onclick="alert('你好')">
```

注释

```javascript
// 单行注释
快捷键 ctrl+/
/* */ 多行注释
快捷键 shift+alt+A
```

## **基本语法**

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
 形参和实参匹配问题：
 实参个数大于形参，只取到形参的个数
 实参个数小于形参，就会出现问题
 		function getSum(num1, num2) {
            console.log(num1 + num2);
        }
        getSum(1);//实参个数小于形参 NaN num2为undefined 和数值型相加得到NaN
        getSum(1, 2, 3);// 实参个数大于形参 3
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
//因此我们在利用函数表达式使用函数时，要先进行声明，才可以调用。在利用关键词function声明函数时，调用和声明顺序无所谓。

```

```javascript
// 案例 1
      var num = 10;
       fun();
       function fun() {
        console.log(num);
        var num = 20;
       } // undefined
预解析之后变成：
var num;
function fun() {
    var num;
    console.log(num);
    num = 20;
}
num = 10;
fun();
显然最后输出undefined
// 案例 2
 	   var num = 10;
       function fun() {
        console.log(num);
        var num = 20;
        console.log(num);
       }
       fun(); //undefined 20
预解析之后变成：
var num;
function fun() {
	var num;
	console.log(num);
    num = 20;
    console.log(num);
}
fun();
显然最后输出undefined 20
// 案例 3 经典
	   f1();
       console.log(c);
       console.log(b);
       console.log(a);
       function f1() {
        var a = b = c = 9;// 相当于 var a = 9;b = 9;c = 9 b,c当全局变量看，a为局部变量
        console.log(a);
        console.log(b);
        console.log(c);
       }
```

![image-20220804211457981](https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/image-20220804211457981.png)



## **对象**

> 对象是一个具体的事物。是一组无序的方法和属性的集合

### 自定义对象

```javascript
// 创建对象的三种方式：
1.利用字面量创建对象
		var obj = {
            uname: 'xbs',
            sex: '男',
            age: 19,
            sayHi: function(){
                console.log('nihao');
            }
        }
        console.log(obj.uname);
		console.log(obj['age']);
		obj.sayHi();
//注意事项：(1) 键值对的方式储存属性和方法 属性名:属性值 (2) 属性之间逗号隔开 (3)方法冒号跟的是一个匿名函数
//调用对象的属性 obj.uname 或 obj['uname']
//调用对象的方法 obj.sayHi();
2.利用new object创建对象
	var obj = new Object();//创建一个空对象
	obj.uname = 'xbs';//追加属性和方法
	obj.age = 18;
	obj.sex = '男';
	obj.sayHi = function(){
        console.log('nihao');
    }
3.利用构造函数创建对象
// 创建多个具有共性(具有相同的属性和方法)的对象，就需要函数将共性的东西抽象封装起来，称为构造函数。
	function 构造函数名() {
		this.属性名 = 属性值;
        this.方法名 = 方法值
    }
	var obj = new 构造函数名();
//(1) 构造函数首字母一般大写 (2) 实例化一个对象用new (3)构造函数不需要return，就可以返回对象
	function Creat(name, age, sex) {
        this.uname = name;
        this.sex = age;
        this.age = sex;
        this.sayHi = function(sing){
            console.log(sing);
        }
    }
    var obj = new Creat('xbs', 19, 'nan');
	obj.sayHi('sayhi');
    console.log(typeof obj);// object
    console.log(obj.uname);// xbs
//构造函数和对象的区别
对象是一个具体的存在，特指某一个；构造函数是一个抽象的概念，泛指某一大类
利用构造函数创建对象的过程就叫做对象的实例化。
//遍历对象
for ..in ..
	var obj = new Object();//创建一个空对象
	obj.uname = 'xbs';//追加属性和方法
	obj.age = 18;
	obj.sex = '男';
	obj.sayHi = function(){
        console.log('nihao');
    }

    for (var k in obj) {
        console.log(k);// 得到属性名
        console.log(obj[k]);// 得到属性值
    }

```

> new关键字在构造函数中的执行过程
>
> 1. 在内存中创建一个空对象
>
> 2. this指向当前创建的空对象
>
> 3. 执行构造函数的代码，给对象添加属性和方法
>
> 4. 返回这个对象

### 内置对象

> js中的对象分成三种：自定义对象 内置对象 浏览器对象
>
> 内置对象：js语言自带的对象，它提供一些必要的属性和方法给开发者。

#### Math对象

```javascript
//Math不是一个构造函数，可以直接使用属性和方法，不需要new一个对象
//最大值 最小值 PI
	console.log(Math.PI);// 3.141592653589793
    console.log(Math.max(1, 3, 2));// 3
    console.log(Math.min(1, 4, 0));// 0
    console.log(Math.max(1, 4, 'xu'));// NaN    
    console.log(Math.max());// -Infinity	
//案例 利用对象封装数学对象，里面有最大值 最小值 PI
var myMath = {
        PI: 3.14159,
        max: function() {
            var max = arguments[0];
            for (var i = 1; i < arguments.length; i++) {
                if (arguments[i] > max) {
                    max = arguments[i];
                }
            }
            return max;
        },
        min: function() {
            var min = arguments[0];
            for (var i = 1; i < arguments.length; i++) {
                if (arguments[i] < min) {
                    min = arguments[i];
                }
            }
            return min;
        }
    }
    console.log(myMath.PI);// 3.14159
    console.log(myMath.max(1, 2 ,3));// 3
    console.log(myMath.max(1, 5 ,3));// 5
    console.log(myMath.min(1, 2 ,3));// 1
//绝对值 向下取整 向上取整 四舍五入
	console.log(Math.abs(-12)); // 12 绝对值
    console.log(Math.floor(1.2));// 1
    console.log(Math.floor(1.5));// 1
    console.log(Math.floor(1.8));// 1
    console.log(Math.floor(-1.2));// -2
	console.log(Math.ceil(1.3));// 2向上取整 往大了取
    console.log(Math.ceil(1.7));// 2
    console.log(Math.round(1.5));// 2
    console.log(Math.round(-1.5));// -1 注意这个
    console.log(Math.round(-1.8));// -2
//Math随机数方法
Math.random() //返回[0,1)中的随机数 ，没有参数
Math.floor(Math.random() * (max - min + 1)) + min// 得到两个整数之间的随机整数，包含这两个整数。
function getRandom(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min// 得到两个整数之间的随机整数，包含这两个整数。
   } 
   console.log(getRandom(0, 10));// 得到0~10之间的一个整数
// 案例 随机点名
var arr = ['xbs', '小明', '小红', '小黄', '小绿'];
var rad = getRandom(0, 4);
console.log(arr[rad]);
// 猜数字游戏
程序随机生成一个1~10之间的数字，并让用户输入一个数字：
如果大于该数字，就提示，数字大了；
如果小于该数字，就提示，数字小了；
如果等于该数字，就提示猜对了。
var rad = getRandom(1, 10);
   while (true) {
    var res = prompt('请输入一个1~10的数：');
    if (res == '') {
        alert('不要试图卡bug');
    }
    else if (rad < res) {
        alert('输入的数大了');
    } else if (rad > res) {
        alert('输入的数字小了');
    } else if(rad == res) {
        alert('猜对了');
        break;
    } else {
        alert('你输入的数格式不正确');
    }
   }
// 限制用户猜的次数
var rad = getRandom(1, 10);
   var count = 10;
   while (count--) {//只能猜10次，第11次时主动退出循环。
    var res = prompt('请输入一个1~10的数：');
    if (res == '') {
        alert('不要试图卡bug');
    }
    else if (rad < res) {
        alert('输入的数大了');
    } else if (rad > res) {
        alert('输入的数字小了');
    } else if(rad == res) {
        alert('猜对了');
        break;
    } else {
        alert('你输入的数格式不正确');
    }
   }
//当count--为0时，循环主动退出，此时count=-1;
   if (count == -1) {
   alert('你的次数已经用光了');
   }

```

#### 日期对象

```javascript
//通过构造函数来创建日期对象
var arr = new Date();
1.无参数，返回系统的当前时间
2.有参数 数字型 2022, 8, 05 字符串型 '2022-8-5 21:20:20'
	var date = new Date();
    console.log(date);
    var date1 = new Date(2022, 8, 05);
    console.log(date1);// 返回的是7月不是八月
    var date2 = new Date('2022-8-5 21:20:20');
    console.log(date2);
3.日期的格式化
//格式化年月日
var date = new Date();
    console.log(date.getFullYear());// 2022
    console.log(date.getMonth() + 1);// 7 ,月份是从0~11，要显示正确的月份，应+1
    console.log(date.getDate());// 5
    console.log(date.getDay());// 5 星期日显示是0
    var arr = ['星期天','星期一','星期二','星期三','星期四','星期五','星期六'];
    var year = date.getFullYear();
    var month = date.getMonth();
    var dates = date.getDate();
    var day = date.getDay();
    console.log('今天是: ' + year + '年' + month + '月' + dates + '日 ' + arr[day]); // 今天是: 2022年7月5日 星期五
//格式化时分秒
	var date = new Date();
	console.log(date.getHours());//时
    console.log(date.getMinutes());//分
    console.log(date.getSeconds());//秒
    //封装一个函数，返回当前的时分秒 08:09:01
   function getTime() {
        var time = new Date();
        hour = time.getHours();
       hour = hour < 10 ? '0' + hour : hour;
        minutes = time.getMinutes();
        minutes = minutes < 10 ? '0' + minutes : minutes;
        second = time.getSeconds();
        second = second < 10 ? '0' + second : second;
        return hour + ':' + minutes + ':' + second;
   }
   console.log(getTime());
// 获取日期的总的毫秒数(时间戳)
距离1970.1.1过了多少毫秒数
1. 通过valueof() getTime()
	var date = new Date();
	console.log(date.valueOf());
	console.log(date.getTime());
2. 常用的写法
	var date = +new Date();
	console.log(date);
3. H5新增的写法
	console.log(Date.now());
//案例 倒计时
思路：倒计时就是将来的时间减去现在的时间。可以用时间戳进行相减，然后将得到的结果转化成时分秒
	function countTime(time) {
        var nowTime = +new Date();
        var inputTime = +new Date(time);
        var times = (inputTime - nowTime) / 1000;
        var d = parseInt(times / 60 / 60 / 24);//得到天数
        d = d < 10 ? '0' + d : d;
        var h = parseInt(times / 60 / 60 % 24);//得到小时
        h = h < 10 ? '0' + h : h;
        var m = parseInt(times / 60 % 60);//得到分
        m = m < 10 ? '0' + m :m;
        var s = parseInt(times % 60);//得到秒
        s= s < 10 ? '0' + s : s;
        return d + '天' + h + '时' + m + '分' + s + '秒';
    }
    console.log(countTime('2022-8-5 22:25:00'));
```

#### 数组对象

```javascript
//数组创建的两种方式 字面量 new
var arr = [];
var arr1 = Array();//创建了一个空数组
var arr2 = Array(2);//创建了一个长度为2的空数组
var arr3 = Array(1,2)//创建数组[1,2]
//检测是否为数组的两种方式 instanceof isArray()
var arr = new Array(1,2);
var arr1 = 'string';
console.log(arr instanceof Array);// true
console.log(arr1 instanceof Array);// false
console.log(Array.isArray(arr));// true
console.log(Array.isArray(arr1));// false
//添加数组元素 
//push末尾添加元素，返回数组的长度
1. var arr = [1,2,3];
	console.log(arr.push(4,5));//5
	console.log(arr);// [1,2,3,4,5]
//unshift()数组前面添加元素，返回数组的长度
	var arr = [1,2,3];
	console.log(arr.unshift(0,6));//5
	console.log(arr);//[0,6,1,2,3]
//删除数组元素 
//pop删除数组的最后一个元素，返回删除的元素
1. var arr = [1,2,3,4];
   console.log(arr.pop());// 4
   console.log(arr);// [1,2,3]
//shift删除数组的第一个元素，返回删除的元素
	var arr = [1,2,3,4];
	console.log(arr.shift());//1
	console.log(arr);//[2,3,4]
//案例 筛选数组 有一个包含工资的数组[1500,1200,2000,2100,1800],要求将数组中工资超过2000的删除，剩余的放在新数组中。
	var arr = [1500,1200,2000,2100,1800];
	var newArr = [];
	for (var i = 0; i < arr.length; i++) {
        if(arr[i] < 2000) {
            //newArr[newArr.length] = arr[i];
            newArr.push(arr[i]);
        }
    }
	console.log(newArr);
//翻转数组 reverse()
var arr = [3,2,1,4,2];
arr.reverse();
console.log(arr);// [2, 4, 1, 2, 3]
//数组排序 sort
 var arr = [3,5,1,7,4];
 arr.sort();
 console.log(arr);// [1, 3, 4, 5, 7]
但是这个sort进行排序有些问题
var arr = [1,12,23,21,4];
arr.sort();
console.log(arr);// [1, 12, 21, 23, 4] 出现问题，因为sort排序是按照ASCii码进行排序
//正确写法
var arr = [1,12,23,21,4];
arr.sort(function(a,b) {
    return a - b;//升序排序   降序排序  return b - a;
});
console.log(arr);// [1, 4, 12, 21, 23]
//获取数组元素的索引
1.indexOf(数组元素) 查找给定元素的第一个索引号，不存在则返回-1
var arr = ['xbs','xu','xuben'];
console.log(arr.indexOf('xbs'));//0
2.lastIndexOf(数组元素) 查找给定元素的最后一个索引号，不存在则返回-1
var arr = ['xbs','xu','xuben','xbs'];
console.log(arr.lastIndexOf('xbs'));//3
//案例 数组去重 有一个数组,['c','a','z','a','x','a','x','c','b'],要求去除数组中重复的元素
思路：将原数组按顺序遍历，每访问一个元素，判断其有没有出现在新数组中，若有，则不添加到新数组，若没有，则添加到新数组中
/*var arr = ['c','a','z','a','x','a','x','c','b'];
var newArr = [];
for  (var i = 0; i < arr.length; i++) {
    if (newArr.indexOf(arr[i]) == -1) {
        newArr.push(arr[i]);
    }
}
console.log(newArr);*/
封装一个去重函数
function unique(arr) {
    var newArr = [];
    for  (var i = 0; i < arr.length; i++) {
    if (newArr.indexOf(arr[i]) == -1) {
        newArr.push(arr[i]);
    }
}
 return newArr;   
}
var demo = unique(['c','a','z','a','x','a','x','c','b']);
console.log(demo);
//数组转化成字符串
1.toString() 将数组转化成字符串，逗号隔开
var arr = ['x','b','s'];
console.log(arr.toString());// x,b,s

2.join('分隔符') 将数组转化成字符串，分隔符隔开
var arr = ['x','b','s'];
console.log(arr.join('|'));// x|b|s
//concat() 连接两个或多个数组
var array1 = ['a', 'b', 'c'];
var array2 = ['d', 'e', 'f'];
var array3 = array1.concat(array2);
console.log(array3);// ['a', 'b', 'c', 'd', 'e', 'f']
//slice(begin,end) 截取数组 包括begin，不包括end 
var arr = [1,2,3,4,5,6,7];
console.log(arr.slice(0,3));// [1,2,3]
//splice(begin,删除的个数) 删除数组的元素 返回由被删除的元素组成的一个数组
var arr = [1,2,3,4,5,6,7];
console.log(arr.splice(0,3));// [1,2,3]
console.log(arr);// [4,5,6,7] 原数组发生改变
```

#### 字符串对象

> 基本包装类型
>
> 把基本数据类型包装成复杂数据类型

```javascript
var str = 'xbs';
console.log(str.length);
相当于
var temp = new String('xbs');
str = temp;
temp = null;
```

```javascript
//字符串不可变
字符串里面的值不变，只是看上去变了，但其实是地址变了，内存中开辟一个新空间
字符串中所有的方法都不会改变原字符串，会返回一个新字符串
var str = 'xbs';
console.log(str);//xbs
str = 'xubenshan';
console.log(str);//xubenshan
//根据字符返回位置
//indexOf(查找的元素，从索引号为多少开始查找)
1.	var str = 'xubenshan';
	console.log(str.indexOf('n'));//4
	console.log(str.indexOf('n',5));//8
	console.log(str.lastIndexOf('n'));//8

//查找字符串'abcoefoxyozzopp'中所有o出现的位置以及次数
思路：先查找到第一个o所在的位置，只要indexOf()不是-1，就索引值加1，一直查找。
var str = 'abcoefoxyozzopp';
var temp = str.indexOf('o');
var count = 0;
while (temp != -1) {
    console.log(temp);
    count++;
    temp = str.indexOf('o', temp + 1);
}
console.log('出现的次数' + count);
// 3 6 9 12 出现的次数为4

//根据位置返回字符
2.
//charAt(index)
var str = 'xubenshan';
for (var i = 0; i < str,length; i++) {
    console.log(str.charAt(i));
}
//charCodeAt(index) 返回字符的ASCii码
var str = 'xubenshan';
console.log(str.charCodeAt(0));// 120
//str[index]
var str = 'xubenshan';
console.log(str[0]);// x
// 案例 判断一个字符串'abcoefoxyozzopp'中出现次数最多的字符，并统计其次数。
var str = 'abcoefoxyozzopp';
var obj = {};
for (var i = 0; i < str.length; i++) {
    /*var temp = str.charAt(i);// 为什么不能用.来调用属性，必须用[]来调用
    if (obj[temp]) {
        obj[temp]++;
    } else {
        obj[temp] = 1;
    }*/
    if (obj[str[i]]) {
        obj[str[i]]++;
    } else {
        obj[str[i]] = 1;
    }
}
var max = 0;
var ch = '';
for (var k in obj) {
	if (obj[k] > max) {
        max = obj[k];
        ch = k;
    }
}
console.log(ch, max);//o 4

// 拼接和截取字符串
concat(字符串1，字符串2..)
var str1 = 'xbs';
console.log(str1.concat('123'));// xbs123
// substring(start,end) 从start位置开始截取到end位置，不取end
var str = 'xubenshan';
console.log(str.substring(0,3));//xub
// 替换字符 replace('被替换字符'，'替换字符') 只替换第一个满足条件的字符
案例 有一个字符串'abcoefoxyoxxopp' 要求把里面的所有o替换成*
    思路：循环，每替换一次，将得到的新字符串代替原来的字符串，直到无法替换为止。
	var str = 'abcoefoxyoxxopp';
	var newstr = '';
	while (str != newstr) {
        newstr = str;
        str = str.replace('o', '*');
    }
	console.log(str);
//更简洁的写法
	var str = 'abcoefoxyoxxopp';
	while (str.indexOf('o') != -1) {//indexOf(字符)查找字符串中有没有这个字符，没有就返回-1
        str = str.replace('o', '*');
    }
	console.log(str);
//字符转化成数组
split('分割符') join将数组转化成字符串
 	var str = 'blue, yellow, red';
    console.log(str.split(','));
// toUpperCase() 转换大写
//  toLowerCaes() 转换小写
```

```javascript
//综合案例 给定一个字符串 如“abaasdffggghhjjkkgfddsssss3444343”
1.字符串的长度
2.取出指定位置的字符，如0，3，5，9
3.查找指定字符是否存在 i，c, b
4.替换指定的字符 g替换22 ss替换b
5.截取指定开始位置到结束位置的字符串 如取得1~5的字符串
6.找出以上字符串中出现次数最多的字符和出现的次数
```

简单数据类型和复杂数据类型

* 简单数据类型（值类型） 

`string` `number` `boolean` `undefined` `null`

存储到栈里面 ，里面直接开辟一个空间，存储简单数据类型的值

```javascript
// null类型返回的是一个空对象（注意）
	var obj = null;
    console.log(typeof obj);// object
因此如果有一个变量我们打算存储为对象，但是现在不确定放什么，可以用null
```

* 复杂数据类型 （引用类型）

通过`new`关键字创建的对象

`Object` `Array`

存储到堆里面，在栈里面开辟一个空间存放地址，通过这个地址指向堆里面的数据···

**简单数据类型和复杂数据类型的传参问题**

```javascript
//简单数据类型传参
function fn(a) {//实参x的值复制一份给形参，开辟另一个空间储存a的值10
    a++;
    console.log(a);
}
var x = 10;//在栈里面开辟一个空间，存储x的值10
fn(x);//11
console.log(x);//10
值传参，形参不能改变实参
//复杂数据类型
function Person(name) {
	this.name = name;
}
function f1(x) {
    console.log(x.name);// xbs
    x.name = 'xubenshan';
    console.log(x.name);// xubenshan
}
var p = new Person('xbs');
console.log(p.name);// xbs
f1(p);//把引用类型的实参传给形参，就相当于将栈中存放的堆地址复制给形参，形参和实参保存的是同一个地址，操作的是同一个对象
console.log(p,name);// xubenshan
地址传递，形参可以改变实参
```

## **Web APIs**

> `javascript`包括`js`的语法部分和`Web APIs`的`DOM`和`BOM`部分
>
> `API`就是预先封装好的接口（函数），可以直接使用，不用关心内部原理。

### DOM

`df`

##### 获取元素

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
        console.log(lis);//  [li, li, li, li, li]
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

##### 事件基础

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

##### 操作元素

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

==按钮点击案例==

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

<img src="https://cdn.jsdelivr.net/gh/xubenshan/pic-blog@main/img/carbon.png" alt="carbon"  />

##### 节点操作



### BOM



## ES6新特性



## 正则表达式



## **jQuery**



## Ajax



