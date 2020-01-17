>变量的命名规则？注释怎么写？要注意些什么？

#### 1.字符集
1. javascript是用Unicode字符集编写的。
2. Unicode：它是ASCII和Latin-1的超集。
3. 其他：es5要求支持Unicode3及以后版本。

#### 2.javascript相关
1. javascript区分大小写（html不区分，xhtml区分）。
2. javasciipt会忽略标识符之间的空格。
3. javascript可以识别的空格字符。
    1. 普通空格符(\u0020)
    2. 水平制表符(\u0009)
    3. 垂直制表符(\u000B)
    4. 换页符(\u000c)
    5. 不中断空白(\u00A0)
    6. 字节序标记(\uFEFF)
4. javascript将如下字符识别为行结束符
    1. 换行符(\u000A)
    2. 回车符(\u000D)
    3. 行分隔符(\u2028)
    4. 段分隔符(\u2029)
    5. 回车符和换行符在一起被解析为一个单行结束符。
5. 注释用法

>如下

```javascript
//这里是行级注释
/*我是块级注释*/
```
6. 直接量
    1. 定义：程序中可以直接使用的数据值
    2. 示例


```javascript
12                  数字
1.2                 小数
"hello world"       字符串文本
"hi"                另一个字符串
true                布尔值
false               另一个布尔值
/javascript/gi      正则表达式直接量
null                空

```

7. 标识符和保留字
    1. 标识符：就是给变量和函数命名的字符（不是字符串）。
    2. 规则：必须以字母、下划线、美元标志开始。后续字符可以是数字、字母、下划线和美元标志。==数字不允许开头。==
    3. 保留字：javascript把一些字符保留下来作为自己的关键字（js拿去自己用）。
    4. 关键字汇总，见下。


```javascript
break       delete      function        return      typeof  

case        do          if              switch      var 

catch       else        in              this        void

continue    false       instanceof      throw       while   

debugger    finally     new             true        with

default     for         null            try         class

const       enum        export          extend      import   

super       

```

8. 以下这些在普通javascript代码中是合法的，在严格模式下是保留字


```javascript
implements  let  private   public   yield   interface   package   protected   static  
```

9. 严格模式下对下面标识符做了严格限制，它们并不完全是保留字。但不能作为变量名、函数名或参数名


```javascript
arguments   eval
```

10. javascript预定了很多全局变量和函数，应当避免使用他们作为变量名和函数名


1 | 2 | 3 | 4 | 5
:---:|:---:|:---:|:---:|:---:
arguments | encodeURI| Infinity | Number | RegExp
Array | encodeURIComponent| isFinite| Object| String
Boolean | Error| isNaN| parseFloat| SyntaxError
Date | eval| JSON| parseInt| TypeError
decodeURI | evalError| Math| RangeError| undefined
encodeURIComponent | Function| NaN| ReferenceError| URIError

#### 3.javascript中的分号

1. 作用：提高代码的整洁性和可读性（我觉得相当于语文里句号的作用）
2. 可省的分号：在javascript中，分号有些情况下是可以省略的。
    1. 一个句子独占一行时；
    2. 右花括号后面；

>tips：不推荐省略，很容易出错.

比如：


```javascript
var y=x+f
(a+b).toString()
```

- 按照一般想法，会认为这是两条语句

- 但实际上浏览器会这样解析它，如下


```javascript
var y=x+f(a+b).toString()
```
>上面的示例中，浏览器会以为f（a+b）是一个函数调用

- 由上我们可以得到当一条语句以 “（“、”[“、”/“、”+“或”-“开始，那么它极有可能和前一条语句一起解析。（前一条语句没写分号的情况下）

比如


```javascript
x
++
y
```
会解析成


```javascript
x;
++y;
```
