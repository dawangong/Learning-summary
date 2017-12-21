#### 1. 原始表达式：
1. 定义：最简单的表达式（可以直接写出来的）
2. 示例如下：
    


直接量：
```javascript
1.23
'hello'
/pattern/
```
保留字：
```javascript
true
false
null
this
```
变量:
```javascript
a、b
```
#### 2. 对象和数组初始化表达式
    1. 定义：实际上是一个新创建的对象和数组。它们不是原始表达式。
    2. 对象和数组初始化表达式示例
    


数组:
```javascript
[]              //空数组
[1,2]           //拥有两个元素的数组
```

对象:
```javascript
var p={}        //空对象
var p={x:2,y:3} //拥有两个属性成员的对象
```
#### 3. 函数表达式
1. 定义：函数表达式可以称为函数直接量一般如下形式。
2. 特点：这样写函数不会提升。
    

```javascript
var a=function (x) {
    return x;
}
```
#### 4. 属性访问表达式
1. 用法：访问一个对象的属性或者数组的值
2. 如下示例：
    

```javascript
var a={x:3,y:4};
var b=[1,2];
a['x']/a.x        //访问a对象下的x属性
b[0]              //访问b数组第一项的值

```
#### 5. 调用表达式


```javascript
function add(){}

add();
```
#### 6. 对象创建表达式


```javascript
new Object();
```

#### 7. 运算符概述

>算术运算符

运算符|	描述|	例子|	x 运算结果|	y 运算结果
:---:|:---:|:---:|:---:|:---:
\+	|加法|	x=y+2|	7|	5	
\-	|减法|	x=y-2|	3|	5	
\*	|乘法|	x=y*2|	10|	5	
\/	|除法|	x=y/2|	2.5|5	
\%	|取余|	x=y%2|	1|	5	
\++	|自增|	x=++y|	6|	6
\++	|自增|  x=y++|	5|	6	
\--	|自减|	x=--y|	4|	4	
\--	|自减|  x=y--|	5|	4

>赋值运算符

运算符	|例子|	等同于|	运算结果
:---:|:---:|:---:|:---:
=	|x=y	|      |  x=5
+=	|x+=y	|x=x+y	|x=15
-=	|x-=y	|x=x-y	|x=5	
\*=	|x\*=y	|x=x*y	|x=50
/=	|x/=y	|x=x/y	|x=2	
%=	|x%=y	|x=x%y	|x=0

>比较运算符


运算符|	描述|	比较|	返回值
:---:|:---:|:---:|:---:
==	|等于|	x==8|	false	
===	|绝对等于（值和类型均相等）	|x==="5"|	false	
!=	 |不等于|	x!=8|	true	
!==	 |不绝对等于（值和类型有一个不相等，或两个都不相等）	|x!=="5"|	true	
\>	| 大于	|x>8	|false	
\<	 |小于	|x<8	|true	
\>=	 |大于或等于|	x>=8|	false	
\<=	 |小于或等于|	x<=8|	true

>逻辑运算符


运算符|	描述|	例子
:---:|:---:|:---:
&&	|and|	(x < 10 && y > 1) 为 true
\|\|	|or|	(x\==5 \|\| y\==5) 为 false
!	|not|	!(x==y) 为 true

>条件运算符


```javascript
variablename=(condition)?value1:value2； 
```

#### 8. 运算符优先级

>见下图

![image](http://upload.ouliu.net/i/20171130160521qyhzg.png)

#### 9. 运算符副作用
    1. 赋值运算符：给一个变量赋值，用到这个变量的变量或表达式都会发生变化；
    2. delete运算符：删除属性后会给属性赋值undefined。

#### 10. 位运算符

    1. 概述：按位操作符（Bitwise operators） 将其操作数（operands）当作32位的比特序列（由0和1组成），而不是十进制、十六进制或八进制数值。例如，十进制数9，用二进制表示则为1001。按位操作符操作数字的二进制形式，但是返回值依然是标准的JavaScript数值。
    2. 下面的表格总结了JavaScript中的按位操作符:
    
![image](http://upload.ouliu.net/i/201711301619111whiq.png)

>详细请看[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators)

#### 11. in 运算符
1. 定义：测试一个对象中是否存在一种属性。
2. 用法：

```javascript
result = property in object

参数：
result
必需。任何变量。
property
必需。计算结果为字符串表达式的表达式。
object
必需。任意对象。
```
>当然in也可以用来测试数组属性，数组的属性指的是它的索引


```javascript
 var arr = [1];
  console.log("1" in arr); // false
  console.log("0" in arr); // true
  console.log(0 in arr);   // true
```

#### 12. instanceof 运算符
1. 定义：用来测试一个对象在其原型链中是否存在一个构造函数的 prototype 属性。
2. 语法


```javascript
object instanceof constructor

参数：
object
要检测的对象.
constructor
某个构造函数
```
#### 13. typeof 运算符
    1. 定义：返回一个用于标识表达式的数据类型的字符串。
    2. 语法
    

```javascript
typeof '3';
```
一些特性:
```javascript
typeof     运算符把类型信息以字符串形式返回。 
typeof     返回六种可能的值：“数字”、“字符串”、“布尔值”、“对象”、“函数”和“未定义”。
typeof     语法中的圆括号是可选的。
```
#### 14. void 运算符
1. 定义：禁止表达式返回值。
2. 备注：expression 参数是任何有效的 JavaScript 表达式。void 运算符计算其表达式，并返回undefined。当应计算表达式，但又不希望脚本的其他部分看见其结果时，该运算符很有用。  


```javascript
void expression 
```
#### 15. delete 运算符
    1. 定义：操作符用于删除对象的某个属性。
    2. 用法示例：


```javascript
delete object.property 
delete object['property']
```
参数：
```javascript
object
对象的名称，或计算结果为对象的表达式。
property
要删除的属性。
```
返回值：
```javascript
对于所有情况都是true，除非属性是一个自己的不可配置属性，在这种情况下，非严格模式返回 false。
```
异常：
```javascript
在严格模式下，如果是对象自身的不可配置属性，会抛出Global_objects/SyntaxError。
```
#### 16. eval 运算符
1. 解释：eval()它是一个函数也是一个运算符。
2. eval()它接受一个参数，如果不是字符串就直接返回，如果是字符串，它会当成javascript代码去对待。


```javascript
参数：

string
一串表示JavaScript表达式，语句，或者是一系列语句的字符串。表达式可以包括变量以及已存在对象的属性。
返回值

执行指定代码之后的返回值。如果返回值为空，返回undefined
```

>tips: 避免在不必要的情况下使用eval

- eval() 是一个危险的函数， 他执行的代码拥有着执行者的权利。如果你用eval()运行的字符串代码被恶意方（不怀好意的人）操控修改,您可能会利用最终在用户机器上运行恶意方部署的恶意代码，并导致您失去您的网页或者扩展程序的权限。更重要的是，第三方代码可以看到某一个eval()被调用时的作用域，这也有可能导致一些不同方式的攻击。相似的Function就是不容易被攻击的。

- eval()的运行效率也普遍的比其他的替代方案慢，因为他会调用js解析器，即便现代的JS引擎中已经对此做了优化。

    
#### 17. new 运算符
1. 定义：创建一个新对象。
2. 语法

```javascript

new Object; 

参数：
constructor
必需。对象的构造函数。若构造函数没有参数，则可省略圆括号。
arguments
可选。任意传递给新对象的构造函数的参数。
```
>运算符执行下列任务：

- 创建一个没有成员的对象。
- 它为该对象调用构造函数，并将一个指针作为this指针传递给新创建的对象。
- 然后，构造函数根据传递给它的参数初始化该对象。

#### 18. 逗号运算符
1. 定义：顺序执行两个表达式。
2. 语法
    

```javascript
expression1, expression2

参数：
expression1
任何表达式。
expression2
任何表达式。
```
#### 19. Spread 运算符
1. 定义：允许从iterable表达式（如另一个数组文本）初始化部分数组文本，或允许表达式扩展到多个参数（在函数调用中）。
2. 用法
    

```javascript
var array = [[arg0ToN ,] ...iterable [, arg0ToN]]  
func([args ,] ...iterable [, args | ...iterable]) 

参数：
iterable
必需。 迭代对象。
arg0ToN
可选。 数组文本的一个或多个元素。
args
可选。 函数的一个或多个参数。
```
