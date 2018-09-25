>先按普遍支持的es5语法来划分

- 数据类型
    - 基本数据类型（原始类型）
        - Number
        - String
        - String
        - Null
        - Undefined
    - 引用数据类型（Object）（对象类型）
        - Function
        - Date
        - Array
        - RegExp
        - 等等...
 
>如果算上es6的话基本类型会再多一个Symbol

- 对象类型分类
    - 本地对象（就是指js中的引用类型）
        - Object
        - Function
        - Array
        - String
        - Boolean
        - Number
        - Date
        - RegExp
        - Error
        - EvalError
        - RangeError
        - ReferenceError
        - SyntaxError
        - TypeError
        - URIError
    - 内置对象
        - Global
        - Math
    - 宿主对象
        - BOM
        - DOM
        


#### 1. 数字

1. 特点：javascript中不区分整数值和浮点数值，所有的数字均用浮点数值表示。
2. 一个数字直接出现在javascript中，我们称之数字直接量。
3. javscript同样可以识别十六进制的值。16进制是指以“0x”或“0X”为前缀其后跟随十六位进制数串的直接量。十六位进制值是0-9之间的数字和a(A)-f(F)之间的字母组成a-f的字母对应表示数字10-15
#### 2. 运算符：+、-、*、/、%等。

  函数  |  说明
   --- | ---
 Math.pow(2,53)|2的53次幂
 Math.round(0.6)|四舍五入
 Math.ceil(0.6)|向上取整
 Math.floor(0.6)|向下取整
 Math.abs(-5)|求绝对值
 Math.max(x,y,z)|求最大值
 Math.min(x,y,z)|求最小值
 Math.random()|生成一个在0到1之间的随机数
 Math.PI | 圆周率
 Math.E | 自然对数的底数
 Math.sqrt(3)|3的平方根
 Math.pow(3,1/3)|3的立方根
 Math.sin(0)|三角函数
 Math.exp(3)|e的三次幂
 
 - **JavaScript中算术溢出不会报错，上溢出时结果为Infinity，下溢出时结果为-Infinity**
 - **JavaScript中被0整除不会报错，会返回Infinity或者-Infinity，但是0除以0返回NaN**
 - **JavaScript中NaN不等于NaN，负值0于正值0相等**

#### 3. 文本
    1. 形式：javascript用16位值组成不可变的有序序列表示文本。它们通常来自于Unicode字符集。
    2. 字符串直接量：在javascript中字符串直接量是由单引号或双引号括起来的字符序列。
    3. 字符串间可以通过+号拼接。
#### 4. 转义：javascript的转义通过“\”去实现。比如\n就是一个转义字符，它表示换行。

#### 5. 日期与时间
 
   >JavaScript中包括Date构造函数，用来创建表示日期和时间的对象；
   
 
方法	|描述
---|---
Date()	|返回当日的日期和时间。
getDate()|	从 Date 对象返回一个月中的某一天 (1 ~ 31)。
getDay()|	从 Date 对象返回一周中的某一天 (0 ~ 6)。
getMonth()|	从 Date 对象返回月份 (0 ~ 11)。
getFullYear()|	从 Date 对象以四位数字返回年份。
getYear()	|请使用 getFullYear() 方法代替。
getHours()	|返回 Date 对象的小时 (0 ~ 23)。
getMinutes()|	返回 Date 对象的分钟 (0 ~ 59)。
getSeconds()|	返回 Date 对象的秒数 (0 ~ 59)。
getMilliseconds()|	返回 Date 对象的毫秒(0 ~ 999)。
getTime()	|返回 1970 年 1 月 1 日至今的毫秒数。
getTimezoneOffset()	|返回本地时间与格林威治标准时间 (GMT) 的分钟差。
getUTCDate()|	根据世界时从 Date 对象返回月中的一天 (1 ~ 31)。
getUTCDay()	|根据世界时从 Date 对象返回周中的一天 (0 ~ 6)。
getUTCMonth()	|根据世界时从 Date 对象返回月份 (0 ~ 11)。
getUTCFullYear()|	根据世界时从 Date 对象返回四位数的年份。
getUTCHours()	|根据世界时返回 Date 对象的小时 (0 ~ 23)。
getUTCMinutes()	|根据世界时返回 Date 对象的分钟 (0 ~ 59)。
getUTCSeconds()	|根据世界时返回 Date 对象的秒钟 (0 ~ 59)。
getUTCMilliseconds()	|根据世界时返回 Date 对象的毫秒(0 ~ 999)。
parse()	|返回1970年1月1日午夜到指定日期（字符串）的毫秒数。
setDate()	|设置 Date 对象中月的某一天 (1 ~ 31)。
setMonth()	|设置 Date 对象中月份 (0 ~ 11)。
setFullYear()	|设置 Date 对象中的年份（四位数字）。
setYear()	|请使用 setFullYear() 方法代替。
setHours()	|设置 Date 对象中的小时 (0 ~ 23)。
setMinutes()|	设置 Date 对象中的分钟 (0 ~ 59)。
setSeconds()|	设置 Date 对象中的秒钟 (0 ~ 59)。
setMilliseconds()|	设置 Date 对象中的毫秒 (0 ~ 999)。
setTime()	|以毫秒设置 Date 对象。
setUTCDate()|	根据世界时设置 Date 对象中月份的一天 (1 ~ 31)。
setUTCMonth()|	根据世界时设置 Date 对象中的月份 (0 ~ 11)。
setUTCFullYear()|	根据世界时设置 Date 对象中的年份（四位数字）。
setUTCHours()	|根据世界时设置 Date 对象中的小时 (0 ~ 23)。
setUTCMinutes()	|根据世界时设置 Date 对象中的分钟 (0 ~ 59)。
setUTCSeconds()	|根据世界时设置 Date 对象中的秒钟 (0 ~ 59)。
setUTCMilliseconds()	|根据世界时设置 Date 对象中的毫秒 (0 ~ 999)。
toSource()	|返回该对象的源代码。
toString()	|把 Date 对象转换为字符串。
toTimeString()	|把 Date 对象的时间部分转换为字符串。
toDateString()	|把 Date 对象的日期部分转换为字符串。
toGMTString()	|请使用 toUTCString() 方法代替。
toUTCString()	|根据世界时，把 Date 对象转换为字符串。
toLocaleString()|	根据本地时间格式，把 Date 对象转换为字符串。
toLocaleTimeString()	|根据本地时间格式，把 Date 对象的时间部分转换为字符串。
toLocaleDateString()	|根据本地时间格式，把 Date 对象的日期部分转换为字符串。
UTC()	|根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数。
valueOf()	|返回 Date 对象的原始值。


#### 6. 字符串直接量
>JavaScript中字符串直接量是由单引号或双引号括起来的字符序列，单引号定界的字符串可以包含双引号，双引号定界的字符串也可以包含单引号；
 字符串直接量可以拆分成多行（ECMAScript5之后才可以），每行必须用\结束，反斜线和行结束符不算是字符串直接量的内容；在使用单引号的时候要注意英语
 单词中的撇号，使用时应进行转义；
 
#### 6.1 转义字符

   转义字符 | 含义说明
   ----| ----
   \o | NUL字符
   \b |退格符
   \t |水平制表符
   \n | 换行符
   \v | 垂直制表符
   \f | 换页符
   \r | 回车符
   \\" |双引号
   \\' | 单引号
   \\ | 反斜线
   \xXX | 由两位十六进制数XX指定的Latin-l字符
   \uXXX | 由四位十六进制XXXX指定的Unicode字符
   
#### 6.2 字符串的使用
>JavaScript中字符串是固定不变的，类似replace()与toUpperCase()等方法都是返回新的字符串，原字符串本身是没有改变的；
 
 - 字符串属性
 
 属性	| 描述
 ----|---
 constructor|	对创建该对象的函数的引用
 length	|字符串的长度
 prototype|	允许您向对象添加属性和方法
 
 - 字符串提供很多调用方法：
 
 方法|描述
 ---|---
 anchor()	|创建 HTML 锚。
 big()	|用大号字体显示字符串。
 blink()	|显示闪动字符串。
 bold()	|使用粗体显示字符串。
 charAt()	|返回在指定位置的字符。
 charCodeAt()	|返回在指定的位置的字符的 Unicode 编码。
 concat()	|连接字符串。
 fixed()	|以打字机文本显示字符串。
 fontcolor()	|使用指定的颜色来显示字符串。
 fontsize()	|使用指定的尺寸来显示字符串。
 fromCharCode()|	从字符编码创建一个字符串。
 indexOf()	|检索字符串。
 italics()	|使用斜体显示字符串。
 lastIndexOf()	|从后向前搜索字符串。
 link()	|将字符串显示为链接。
 localeCompare()	|用本地特定的顺序来比较两个字符串。
 match()	|找到一个或多个正则表达式的匹配。
 replace()	|替换与正则表达式匹配的子串。
 search()	|检索与正则表达式相匹配的值。
 slice()	|提取字符串的片断，并在新的字符串中返回被提取的部分。
 small()	|使用小字号来显示字符串。
 split()	|把字符串分割为字符串数组。
 strike()	|使用删除线来显示字符串。
 sub()	|把字符串显示为下标。
 substr()	|从起始索引号提取字符串中指定数目的字符。
 substring()	|提取字符串中两个指定的索引号之间的字符。
 sup()	|把字符串显示为上标。
 toLocaleLowerCase()	|把字符串转换为小写。
 toLocaleUpperCase()	|把字符串转换为大写。
 toLowerCase()	|把字符串转换为小写。
 toUpperCase()	|把字符串转换为大写。
 toSource()	|代表对象的源代码。
 toString()	|返回字符串。
 valueOf()	|返回某个字符串对象的原始值。

#### 7. javascript的浮点数和四舍五入.

1. javascript采用IEEE-754浮点数表示法。这是一种可以精确表示分数却无法精确表示小数的表示法。也就是我们常说的javascript浮点运算能力弱。它没办法精确表示0.1这样的简单数字。

#### 8.javascript语言核心包括DATE()函数，它为日期计算提供了很多API。具体的之后详解。

#### 9. javascript定义了RexExp()构造函数，用来创造匹配文本的对象。也就是我们说的正则。正则虽然不是基本类型，却可以有直接量写法（字面量）。同样它也具备很多API。

#### 10. 布尔值：用来指代真和假，通过保留字true或false表示。

#### 11. 模式匹配
>JavaScript中定义了RegExp()构造函数，用来创建表示文本匹配模式的对象 ，这些模式成为“正则表达式”，RegExp不是JavaScript中的基本类型，是一种特殊对象，与Date相似。
  在两条斜线之间的文本构成一个正则表达式直接量，第二条斜线之后可以跟随一个或多个字母进行匹配模式的修饰；
  
  - 直接语法方式： /pattern/attributes
  - 创建RegExp对象方法： new RegExp(pattern,attributes);
   
    
     1、参数说明
     
        参数pattern是一个字符串，制定了正则表达式的模式或者其他正则表达式；
        
        参数attributes是一个可选的字符串，包括属性’g‘，’i‘，’m‘，分别用于指定匹配全局、区分大小写匹配，匹配多行；
       
     2、返回值说明   
     
        一个新的RegExp对象，具有指定的模式和标志，如果pattern是正则表达式而不是字符串，那么 RegExp() 构造函数将用与指定的 RegExp 相同的模式和标志创建一个新的 RegExp 对象。
        
        如果不用 new 运算符，而将 RegExp() 作为函数调用，那么它的行为与用 new 运算符调用时一样，只是当 pattern 是正则表达式时，它只返回 pattern，而不再创建一个新的 RegExp 对象。
      
     3、抛出说明
     
        SyntaxError - 如果 pattern 不是合法的正则表达式，或 attributes 含有 "g"、"i" 和 "m" 之外的字符，抛出该异常。
        
        TypeError - 如果 pattern 是 RegExp 对象，但没有省略 attributes 参数，抛出该异常。


 - RegExp中的修饰符
 
     修饰符 | 描述
     ---|---
     i	|执行对大小写不敏感的匹配。
     g	|执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。
     m	|执行多行匹配。
     
     
 - RegExp中的方括号
    
   表达式	| 描述
   ----|---
   [abc]	|查找方括号之间的任何字符。
   [^abc]	|查找任何不在方括号之间的字符。
   [0-9]	|查找任何从 0 至 9 的数字。
   [a-z]	|查找任何从小写 a 到小写 z 的字符。
   [A-Z]	|查找任何从大写 A 到大写 Z 的字符。
   [A-z]	|查找任何从大写 A 到小写 z 的字符。
   [adgk]	|查找给定集合内的任何字符。
   [^adgk]	|查找给定集合外的任何字符。
   (red/blue/green)	|查找任何指定的选项。 
   
 - RegExp中的元字符
 
   元字符	|描述
   ---|---
   .	|查找单个字符，除了换行和行结束符。
   \w	|查找单词字符。
   \W	|查找非单词字符。
   \d	|查找数字。
   \D	|查找非数字字符。
   \s	|查找空白字符。
   \S	|查找非空白字符。
   \b	|匹配单词边界。
   \B	|匹配非单词边界。
   \0	|查找 NUL 字符。
   \n	|查找换行符。
   \f	|查找换页符。
   \r	|查找回车符。
   \t	|查找制表符。
   \v	|查找垂直制表符。
   \xxx	|查找以八进制数 xxx 规定的字符。
   \xdd	|查找以十六进制数 dd 规定的字符。
   \uxxxx	|查找以十六进制数 xxxx 规定的 Unicode 字符。

 - RegExp中的量词
 
   量词	| 描述
   ---|---
   n+	|匹配任何包含至少一个 n 的字符串。
   n*	|匹配任何包含零个或多个 n 的字符串。
   n?	|匹配任何包含零个或一个 n 的字符串。
   n{X}	|匹配包含 X 个 n 的序列的字符串。
   n{X,Y}	|匹配包含 X 至 Y 个 n 的序列的字符串。
   n{X,}	|匹配包含至少 X 个 n 的序列的字符串。
   n$	|匹配任何结尾为 n 的字符串。
   ^n	|匹配任何开头为 n 的字符串。
   ?=n	|匹配任何其后紧接指定字符串 n 的字符串。
   ?!n	|匹配任何其后没有紧接指定字符串 n 的字符串。
   
   
 - RegExp中的对象属性
 
   属性 | 描述 
    ---|---
   global	|RegExp 对象是否具有标志 g。声明了给定的正则表达式是否执行全局匹配，该标志被设置则属性为true，未设置为false	
   ignoreCase	|RegExp 对象是否具有标志 i，设置了i标志则返回true，否则返回false；
   lastIndex	|一个整数，标示开始下一次匹配的字符位置。该属性存放一个整数，它声明的是上一次匹配文本之后的第一个字符的位置.上次匹配的结果是由方法 RegExp.exec() 和 RegExp.test() 找到的，它们都以 lastIndex 属性所指的位置作为下次检索的起始点。这样，就可以通过反复调用这两个方法来遍历一个字符串中的所有匹配文本。该属性是可读可写的。只要目标字符串的下一次搜索开始，就可以对它进行设置。当方法 exec() 或 test() 再也找不到可以匹配的文本时，它们会自动把 lastIndex 属性重置为 0。
   multiline	|RegExp 对象是否具有标志 m。是否可以进行多行匹配，如果被设置则该属性为true，否则为false
   source	|返回正则表达式的源文本，不包括正则表达式直接量使用的定界符，也不包括g、i、m
 
 - RegExp的对象方法
 
   方法 | 描述 |  参数说明
   ---| --- |---
   compile | 用于在脚本执行过程中编译正则表达式，也可以改变和重新编译，语法：RegExpObject.compile(regexp,modifier); |regexp是正则表达式，modifier规定匹配类型，i、g、m可结合使用
   exec() | 用于检索字符串中的正则表达式的匹配，返回一个数组，其中放匹配结果，未找到匹配返回null，语法：RegExpObject.exec(string); / 如果 exec() 找到了匹配的文本，则返回一个结果数组。否则，返回 null。此数组的第 0 个元素是与正则表达式相匹配的文本，第 1 个元素是与 RegExpObject 的第 1 个子表达式相匹配的文本（如果有的话），第 2 个元素是与 RegExpObject 的第 2 个子表达式相匹配的文本（如果有的话）， 以此类推。除了数组元素和 length 属性之外，exec() 方法还返回两个属性。index 属性声明的是匹配文本的第一个字符的位置。input 属性则存放的是被检索的字符串 string。我们可以看得出，在调用非全局的 RegExp 对象的 exec() 方法时，返回的数组与调用方法 String.match() 返回的数组是相同的。但是，当 RegExpObject 是一个全局正则表达式时，exec() 的行为就稍微复杂一些。它会在 RegExpObject 的 lastIndex 属性指定的字符处开始检索字符串 string。当 exec() 找到了与表达式相匹配的文本时，在匹配后，它将把 RegExpObject 的 lastIndex 属性设置为匹配文本的最后一个字符的下一个位置。这就是说，您可以通过反复调用 exec() 方法来遍历字符串中的所有匹配文本。当 exec() 再也找不到匹配的文本时，它将返回 null，并把 lastIndex 属性重置为 0。
   test() | 用于检测一个字符串是否匹配某个模式，如果字符串 string 中含有与 RegExpObject 匹配的文本，则返回 true，否则返回 false。语法：RegexpObject.test(string); |调用 RegExp 对象 r 的 test() 方法，并为它传递字符串 s，与这个表示式是等价的：(r.exec(s) != null)。
  
 - 支持正则表达式的String对象的方法

     方法 | 描述 | 说明
     ---| --- | ----
     search	|检索与正则表达式相匹配的值。该参数可以是需要在 stringObject 中检索的子串，也可以是需要检索的 RegExp 对象。语法：	stringObject.search(regexp);|stringObject 中第一个与 regexp 相匹配的子串的起始位置。search() 方法不执行全局匹配，它将忽略标志 g。它同时忽略 regexp 的 lastIndex 属性，并且总是从字符串的开始进行检索，这意味着它总是返回 stringObject 的第一个匹配的位置。
     match	|找到一个或多个正则表达式的匹配。该方法类似 indexOf() 和 lastIndexOf()，但是它返回指定的值，而不是字符串的位置。语法：stringObject.match(searchvalue)';stringObject.match(regexp); |searchvalue规定要检索的字符串值,regexp规定要匹配的模式的 RegExp 对象。如果该参数不是 RegExp 对象，则需要首先把它传递给 RegExp 构造函数，将其转换为 RegExp 对象。
     replace	|替换与正则表达式匹配的子串。语法：stringObject.replace(regexp/substr,replacement)  |regexp/substr规定子字符串或要替换的模式的 RegExp 对象。如果该值是一个字符串，则将它作为要检索的直接量文本模式，而不是首先被转换为 RegExp 对象。 replacement一个字符串值，规定了替换文本或生成替换文本的函数。
     split	|把字符串分割为字符串数组。语法：stringObject.split(separator,howmany) |separator字符串或正则表达式，从该参数指定的地方分割 stringObject；howmany可选参数，该参数可指定返回的数组的最大长度。如果设置了该参数，返回的子串不会多于这个参数指定的数组。如果没有设置该参数，整个字符串都会被分割，不考虑它的长度。


#### 12. null和undefined
    1. null：是一个空对象的引用，数据类型是对象。原型链末端就是null；
    2. undefined：表示值的空缺。
#### 13. 全局对象：

1. 定义：全局对象是预定义的对象，作为 JavaScript 的全局函数和全局属性的占位符。通过使用全局对象，可以访问所有其他所有预定义的对象、函数和属性。全局对象不是任何对象的属性，所以它没有名称。
2. 全局对象的属性时全局定义的符号，javascript可以直接使用。当打开新的页面，javascript解释器会创建一个新的全局对象，并给它一组初始属性。全局对象的属性并不是保留字，但是要当做保留字对待。
    - 全局属性：比如undefined、Infinity以及NaN。
    - 全局函数：比如isNaN()、isFinite()、parseInt()和eval()等。
    - 构造函数：比如Date()、RegExp()、String()、Object()和Array()等。
    - 全局对象：比如Math、JSON和Number对象均为该全局对象的属性。

#### 14. 全局对象是谁？
1. 在浏览器环境下：Window充当全局对象；
2. 在node环境中，Global充当全局对象。

#### 15. 不可更改的基本类型值
1. 现象：任何方法都无法改变原始值。（任何方法指js中自带的函数）
2. 例子：如下


```javascript

var s='hello';
s.toUppercase();
s => 'hello' 值没变
```

#### 16. 类型转换
1. 显式转换：使用Boolean（）、Number（）、String（）、Object（）函数转换。
2. 隐式转换：如下


```javascript
1.      2+'5'='25';
2.      '5'-2=3;
```
>tips：除了null和undefined外的任何值都具有toString（）方法。

#### 17. 包装对象
1. 定义：在存取字符串、数字或者布尔值的属性或方法时创建的临时对象叫做包装对象
2. 用法：临时变量

#### 18. 变量声明：
1. javascript程序使用var（es6之前）来声明变量，同时存入一个初始值undefined。
2.javascript的重复声明是合法无害的，相当于再次赋值。如果遗忘声明，程序会报错。

```javascript
var i;      //undefined
var i=3;    //3
```
#### 19. 变量作用域：
1. 定义：变量作用域是程序源代码中个定义变量的区域。
2. 特点：javascript全局声明的变量具有全局作用域，函数中声明的是局部变量，具有局部作用域。函数参数也是局部作用域，只在函数体内有定义。
3. 函数体内的局部变量优先级高于同名全局变量。

#### 20. 函数作用域和声明提前
1. javascript没有块级作用域，但是有函数作用域。
2. 每个函数都会生成一个作用域，全局作用域中无法访问函数内部局部作用域的变量。
3. 声明提前：
    1. 变量提升
    2. 函数提升
    3. 特点：函数提升会在变量提升之前，假如变量声明并且赋值了，那么同名的函数就会被覆盖掉。
    
#### 21. 作为属性的变量：当声明一个全局变量时，实际上是定义了一个全局对象的属性，当用var声明时，这个属性是不可配置的，也就是这个变量无法通过delete运算符删除。

#### 22. 作用域链：
1. 定义：从局部作用域到全局作用域的搜寻顺序，是一个比较抽象的概念。
2. 作用：决定了选择变量的规则，从局部向全局依次撒网，如果全局也没找到，会抛出一个异常。
3. 示例如下：
    
情况1：
```javascript
var a=2;
function b () {
    var a=3;
    alert(a);   //3
}


```
情况2:
```javascript
var a=2;
function b () {
    alert(a);   //2
}
作用域链阐述了寻找变量的规则
```

end
