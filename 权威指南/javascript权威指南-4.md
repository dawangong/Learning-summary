#### 1. function
1. 关键字function用来定义函数。
2. 下面的方式也可以定义函数。（并且会提升）
    

```javascript
function a (x){
    return x;
}

等同于之前的

var a=function (x){
    return x;
}
```


#### 2. if 语句：
1. if语句是一种基本语句，它让javascript可以选择执行路径。
2. 例子如下：


```javascript
var a=2;
if(a>1)
{
    alert('yes');       //符合条件执行{}里面的，否则执行外边的。
}

// yes
```
>当然也可以搭配else使用


```javascript
var a=2;
if(a>1)
{
    alert('yes');   //符合条件执行{}里面的，否则执行else里面的。
}
else{
    alert('no');  
}
```


#### 3. else if 语句
1. 定义：当指定条件为真，if语句会执行一段语句。如果条件为假，则执行另一段语句。
2. 语法：和if else基本一样，只是它可以有更多可选择的执行分支。
3. 示例：


```javascript
var a=2;
if(a<0)
{
    alert('情况1');   
}
else if(a=0){
    alert('情况2');  
}
else if(a<1){
    alert('情况3'); 
}
else{
    alert('其他');              //这里会alert“其他
}
```
#### 4. switch 语句
1. 定义：else if的变种，但是它更适合所有分支都依赖于同一个表达式的值。
2. 用法：直接看例子
    

```javascript
var a=2;
switch(a){
    case 0 :alert(0) ; break;
    case 1 :alert(1) ; break;
    case 2 :alert(2) ; break;
    case 3 :alert(3) ; break;
    case 4 :alert(4) ; break;
    default:alert('其他');
}
```
>上面的switch语句会根据a的值去选择合适的分支。

>一些注意点如下

- switch比较是全等比较，也就是类型也要一样
- break不能少，它代表不符合条件跳出此分支
- default不是必须的，而且位置是随意的，但是放在最后最合理。因为它代表不符合所有语句则执行default语句块。

#### 5. while 语句
1. 定义：在循环开始前判断是否满足条件进行循环。简单暴力的循环手段，如果条件不对可能造成无限循环，因此也可以用于小数据不知道循环次数的循环需求。
2. 语法示例


```javascript
var a=0;
while(a>3){
    alert('yse')
    a++;
}
```
#### 6. do while语句
1. 定义：和while语句十分相似，只不过它是先执行后判断条件。
2. 示例：
    

```javascript
var i = 0;
do {
    alert('yse');
    i++;
}
while (i < 5);
```
#### 7. for 语句
    1. 最常用的循环语句，功能强大用法看下面示例。
    

```javascript
for(var i=0 ;i<10;i++){
    console.log('yse');
}

```
>上面控制台总共输出10个yes字符。

>for循环“()”内第一个规定循环起始条件，第二个规定循环终止条件，第三个用来减少控制循环次数。

#### 8. for in 语句
1. 定义：以任意顺序遍历一个对象的可枚举属性。对于每个不同的属性，语句都会被执行。
2. 特点：for...in 循环只遍历可枚举属性。像 Array和 Object使用内置构造函数所创建的对象都会继承自Object.prototype和String.prototype的不可枚举属性，例如 String 的 indexOf()  方法或 Object的toString()方法。循环将遍历对象本身的所有可枚举属性，以及对象从其构造函数原型中继承的属性（更接近原型链中对象的属性覆盖原型属性）。
3. 数组也是可以用for in的。就像之前所有的。数组的属性就是它的索引。
4. 示例：


```javascript
var obj = {a:1, b:2, c:3};
    
for (var prop in obj) {
  console.log("obj." + prop + " = " + obj[prop]);
}

// Output:
// "obj.a = 1"
// "obj.b = 2"
// "obj.c = 3"
```

#### 9. 跳转语句
1. 概述：跳转语句顾名思义就是可以使执行位置从一处跳到另一处多搭配循环中。
2. 常见的是break和continue。
3. 特性：
    1. break直接跳出循环体。
    2. continue是跳出本次循环继续下次。

#### 10. 标签语句
1. 定义：可以通过下面这样给语句添加标签，就可以在程序任何地方通过标签引用这条语句。
2. 标签组成：标识符+：
3. break和continue是javascript唯一可以使用语句的地方。
4. 示例如下


```javascript
loop:while(token!=null){
    //这里是代码
    continue loop;  //跳转下一次循环
    //这里是代码
}
```
#### 11. return 语句
1. 概述：返回函数调用的值，只能在函数体内使用，但并不是函数体内必须的东西。在函数体外会报错。
    
#### 12. throw 语句
1. 什么是异常？所谓异常是指发生了某种异常情况或者错误时产生的一个信号。抛出异常就是信号通知发生了错误或异常。
2. 捕获异常：捕获异常是指处理这个信号。
3. 在javascript中，当产生错误时，使用throw语句时就会显式的抛出异常。使用try/catch/finally语句也可以捕获异常。
    
>其实throw就是用来自定义异常信号的

#### 13. try/catch/finally 语句
1. 定义：try/catch/finally语句用于处理代码中可能出现的错误信息。错误可能是语法错误，通常是程序员造成的编码错误或错别字。也可能是拼写错误或语言中缺少的功能（可能由于浏览器差异）。
2. 
    - try语句允许我们定义在执行时进行错误测试的代码块。
    - catch 语句允许我们定义当try代码块发生错误时，所执行的代码块。
    - finally 语句在 try 和 catch 之后无论有无异常都会执行。
3. 注意： catch 和 finally 语句都是可选的，但你在使用 try 语句时必须至少使用一个。
4. 提示： 当错误发生时，JavaScript会停止执行，并生成一个错误信息。使用 throw 语句 来创建自定义消息(抛出异常)。如果你将 throw 和 try 、 catch一起使用，就可以控制程序输出的错误信息。
5. 示例：

>参数说明

- try ：检查是否有错误的代码块。（必须）
- err ：必须(如果使用catch)。指定局部变量应用的错误。该变量可以引用 Error ：对象 (包含发生的错误信息，如 "'addlert' 没有定义")。如果异常通过 throw 语句创建 ，	该 变量引用了为在throw语句中指定的对象
- catch ：如果 try 语句发生错误执行的代码块。如果try语句没发生错误该代码不会执行。（可选）
- finally ：无论 try / catch 的结果如何都会执行（可选）

>try catch

```javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>demo</title>
</head>
<body>
<p>try 语句块中的函数未定义：</p>
<p id="demo"></p>

<script>
try {
    adddlert("欢迎光临！");
}
catch(err) {
    document.getElementById("demo").innerHTML = err.message;
}
</script>

</body>
</html>

结果：adddlert is not defined
```
>try catch+throw


```javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>demo</title>
</head>
<body>

<p>请输入 5 和 10 之间的一个数:</p>

<input id="demo" type="text">
<button type="button" onclick="myFunction()">检测输入</button>
<p id="message"></p>

<script>
function myFunction() {
    var message, x;
    message = document.getElementById("message");
    message.innerHTML = "";
    x = document.getElementById("demo").value;
    try { 
        if(x == "")  throw "为空";
        if(isNaN(x)) throw "不是一个数字";
        if(x > 10)   throw "太大了";
        if(x < 5)    throw "太小了";
    }
    catch(err) {
        message.innerHTML = "输入的值 " + err;
    }
}
</script>

结果：throw自定义的值
```
>try catch+throw


```javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>demo</title>
</head>
<body>

<p>请输入 5 到 10 之间的数:</p>

<input id="demo" type="text">
<button type="button" onclick="myFunction()">检测输入</button>

<p id="message"></p>

<script>
function myFunction() {
    var message, x;
    message = document.getElementById("message");
    message.innerHTML = "";
    x = document.getElementById("demo").value;
    try { 
        if(x == "")  throw "为空";
        if(isNaN(x)) throw "不是一个数字";
        if(x > 10)   throw "太大";
        if(x < 5)    throw "太小";
    }
    catch(err) {
        message.innerHTML = "输入的值 " + err;
    }
    finally {
        document.getElementById("demo").value = "";
    }
}
</script>

</body>
</html>

结果：catch语句捕捉返回错误信息
      finally执行其他操作
```
#### 14. with 语句
1. 定义：用于临时拓展作用域链；（放在作用于顶端）
2. 注意：在严格模式中with语句是被禁止的，同时使用它的代码块会很难优化，运行的很慢。
3. 用法：如下
    

```javascript
普通访问形式：
var f=document.form[0];
    f.name.value='';
    f.address.value='';
    f.email.value='';

如果使用with语句
with(document.form[0]){
    name.value='';
    address.value='';
    email.value='';
}
```
#### 15. debugger 语句
1. 定义：debugger 语句用于停止执行 JavaScript，并调用 (如果可用) 调试函数。
2. 用法： debugger 语句类似于在代码中设置断点。
3. 示例如下：
    

```javascript
开启 debugger ，代码在执行到第三行前终止。
var x = 15 * 5;
debugger;
document.getElementbyId("demo").innerHTML = x;

```
#### 16. "use strict"
1. 定义：JavaScript 严格模式（strict mode）即在严格的条件下运行。
2. 概述："use strict"指令在JavaScript1.8.5(ECMAScript5)中新增。
它不是一条语句，但是是一个字面量表达式，在 JavaScript 旧版本中会被忽略。"use strict" 的目的是指定代码在严格条件下执行。
严格模式下你不能使用未声明的变量。
3. 兼容性：支持严格模式的浏览器:Internet Explorer 10 +、 Firefox 4+ Chrome 13+、 Safari 5.1+、 Opera 12+。
4. 用法：严格模式通过在脚本或函数的头部添加 "use strict"; 表达式来声明。
5. 示例示范：


```javascript
<script>
"use strict";
x = 3.14;       // 报错 (x 未定义)
</script>
```

>为什么使用严格模式？

消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
- 消除代码运行的一些不安全之处，保证代码运行的安全；
- 提高编译器效率，增加运行速度；
- 为未来新版本的Javascript做好铺垫。

"严格模式"体现了Javascript更合理、更安全、更严谨的发展方向，包括IE 10在内的主流浏览器，都已经支持它，许多大项目已经开始全面拥抱它。
另一方面，同样的代码，在"严格模式"中，可能会有不一样的运行结果；一些在"正常模式"下可以运行的语句，在"严格模式"下将不能运行。掌握这些内容，有助于更细致深入地理解Javascript，让你变成一个更好的程序员。

>严格模式的限制

- 不允许使用未声明的变量
- 不允许删除变量或对象
- 不允许删除函数
- 不允许变量重名
- 不允许使用八进制
- 不允许使用转义字符
- 不允许对只读属性赋值
- 不允许对一个使用getter方法读取的属性进行赋值
- 不允许删除一个不允许删除的属性
- 变量名不能使用 "eval" 字符串
- 变量名不能使用 "arguments" 字符串
- 不允许使用with语句
- 由于一些安全原因，在作用域 eval() 创建的变量不能被调用
- 禁止this关键字指向全局对象

>末尾两点的补充说明：


```javascript
"use strict";
eval ("var x = 2");
alert (x);               // 报错
```



```javascript
function f(){
    return !this;
} 
// 返回false，因为"this"指向全局对象，"!this"就是false

function f(){ 
    "use strict";
    return !this;
} 
// 返回true，因为严格模式下，this的值为undefined，所以"!this"为true


function f(){
    "use strict";
    this.a = 1;
};
f();// 报错，this未定义

```
>严格模式中的保留字

- implements
- interface
- let
- package
- private
- protected
- public
- static
- yield
