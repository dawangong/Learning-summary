>正则表达式是一个描述字符的对象。javascript的RegExp类表示正则表达式。正则拥有强大的模式匹配和文本检索与替换功能。

#### 1. 正则表达式的定义：javascript中用RegExp对象表示。可以使用RegExp()构造函数来创建RegExp()对象。当然正则也有直接量（或叫字面量）的定义方法，如下：


```javascript
var pattern=/s$/;

```javascript
>等价于下面的


```javascript
var pattern=new RegExp("s$");

```javascript
#### 2. 正则的一些字符

>修饰符

![image](http://upload.ouliu.net/i/201712060919589n899.png)

>方括号

![image](http://upload.ouliu.net/i/20171206092029qim9n.png)

>元字符

![image](http://upload.ouliu.net/i/20171206092222pahz3.png)

>tips：\w表示字母数字下划线

>量词

![image](http://upload.ouliu.net/i/201712060924004tjsm.png)

>对象属性

![image](http://upload.ouliu.net/i/201712060926486z21h.png)

>对象方法

![image](http://upload.ouliu.net/i/20171206092814w3u9a.png)

>支持正则的String对象方法

![image](http://upload.ouliu.net/i/20171206092828y2mbp.png)

#### 3. 一些简单的示例：

```javascript
var pattern=/[a-zA-Z0-9]/

//匹配大小写字母和数字
```javascript


```javascript
var pattern=/[^a-zA-Z0-9]/

//匹配除了括号里面字符之外的字符
```javascript

#### 4. 重复字符示例


```javascript
/\d{2,4}/       //匹配2-4个数字
/[^(]*/         //匹配一个或多个非左括号的字符
```javascript

#### 5. 非贪婪重复
1. 用法：在待匹配字符后面跟随一个问号。
2. 例如：??,+?,*?
3. 比如使用“aaa”作为匹配字符串。/a+/会匹配aaa，而/a+?/会尽可能少匹配，最后只会匹配一个a。

>但是非贪婪模式有时结果和期望却很不一样

>比如使用“aaab”作为匹配字符串，如果正则是/a+b/那结果是aaab，如果正则是/a+?b/,结果你期待匹配的是最后一个ab，实际上却会匹配整个字符串。==这是因为正则表达式的模式匹配总是会寻找字符串第一个可能匹配的位置。由于该匹配是从第一个字符开始的，因此不考虑它子串中更短的匹配。==

#### 6. 选择、分组

```javascript
let pattern=/a|ab/g;
let str='ab';
let result=pattern.test(str);
console.log(result);            //true
```javascript
>“|”符号可以用来做选择“或”，“()”可以作为分组


```javascript
let pattern=/[a-z]+(\d+)/g;
```javascript

#### 7. 指定位置匹配

>比如只想匹配单词javascript，就可以使用/^javascript$/

>如果你的正则是/javascript/，那情况就不会像你期待的那样了

#### 8. 支持正则的String对象方法
1. search()方法
    - 参数：正则表达式
    - 作用：返回第一个与之匹配的子串起始位置，如果找不到返回-1；
    - 注意：search不支持全局检索，会忽略g.
    

```javascript
"JavaScript".search(/script/i)      //4
```javascript
2. replace()方法
    - 参数：第一个正则表达式，第二个期待替换为的字符串
    - 作用：执行检索和替换功能
    - 注意：如果带g就会替换所有符合的子串，否则只替换第一个
    
3. match()方法
    - 参数：正则表达式
    - 作用：返回一个符合匹配的结果数组
    - 注意：如果使用了g则返回的数组包括所有匹配结果
    
4. split()方法
    - 参数：正则表达式
    - 作用：字符串转字符串组成的数组
    
#### 9. RegExp的属性
- source:一个只读字符串，包含正则表达式的文本
- global：一个只读布尔值，用以说明这个正则表达式是否带有修饰符g
- ignoreCase：一个只读布尔值，用以说明这个正则表达式是否带有修饰符i
- multiline：一个只读布尔值，用以说明这个正则表达式是否带有修饰符m
- lastIndex：一个可读写的整数，如果匹配模式带g修饰符，这个属性会被存储在整个字符串中下一次检索开始的位置。这个属性会被exec()和test()方法用到。

#### 10. RegExp的方法
- exec()方法：
    - 参数：一个字符串
    - 作用：在字符串中执行匹配检索，如果没找到则返回null，找到了就返回一个数组
    - 注意：与match()不同的是无论有没有g，都会返回一样的数组
    
- test()方法
    - 参数：一个字符串
    - 作用：检测字符串，如果包含正则表达式的一个匹配结果，则返回true