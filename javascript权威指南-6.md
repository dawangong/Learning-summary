#### 1.创造数组

1. 方法：
    1. 字面量
    2. new运算符
    3. 示例
    
>字面量

```javascript
var arr=[1,3];
```javascript
>new运算符


```javascript
var arr =new Array();
```javascript
#### 2.数组的读写


```javascript
var arr=[3,5,7];
alert(arr[2]);          //7
```javascript

#### 3.稀疏数组

1. 定义：包含从0开始不连续索引的数组，通常length大于元素个数
2. 创造：

>通过new运算符


```javascript
var arr=new Array(4);
```javascript

>通过字面量


```javascript
var arr=[];
arr.length=10;
```javascript

3. 注意：通过逗号省略创造的不会产生稀疏数组，实际元素undefined

#### 3.数组的添加删除
1. 基本方法
    1. 头部添加和删除：unshift()和shift()
    2. 尾部的添加删除：push()和pop()
2. 另种尾部添加的方法


```javascript
arr[arr.length]=5;
```javascript

3. splice方法
    1. 语法：
        1. array.splice(start)

        2. array.splice(start, deleteCount) 

        3. array.splice(start, deleteCount, item1, item2, ...)
        
    2. 参数：
    
        1. start 指定修改的开始位置（从0计数）。如果超出了数组的长度，则从数组末尾开始添加内容；如果是负值，则表示从数组末位开始的第几位（从1计数）；若只使用start参数而不使用deleteCount、item，如：array.splice(start) ，表示删除[start，end]的元素。
    
        2. deleteCount 可选 整数，表示要移除的数组元素的个数。如果 deleteCount 是 0，则不移除元素。这种情况下，至少应添加一个新元素。如果 deleteCount 大于start 之后的元素的总数，则从 start 后面的元素都将被删除（含第 start 位）。如果deleteCount被省略，则其相当于(arr.length - start)。
        3. item1, item2, ... 可选 要添加进数组的元素,从start 位置开始。如果不指定，则 splice() 将只删除数组元素。
    
    3. 返回值：由被删除的元素组成的一个数组。如果只删除了一个元素，则返回只包含一个元素的数组。如果没有删除元素，则返回空数组。

#### 4.数组遍历
>方法
1. for循环
2. for in循环
3. forEach()方法

#### 5.多维数组

>javascript不支持多维数组，但可以用数组的数组来近似


```javascript
var arr=[[2,3],[,4,5]]      //可以表示两行两列的数组
```javascript
#### 6.数组方法

1. join():将数组每一项拼接成字符串，接收一个参数可以控制字符串拼接的符号
2. sort():对数组进行排序，但是需要传入比较函数


```javascript
<script type="text/javascript">  
var arr=[{name:'zhangsan',age:'28'},{name:'lisi',age:'45'}]  
function pai(sx){  
return function(obj1,obj2){  
return obj1[sx]-obj2[sx]; 
}  
}  
  
var k=arr.sort(pai('age'));  
alert(k[0].age);  
</script>  
```javascript

3. reverse():颠倒数组
4. concat():接收一个参数，将两个数组连接在一起
5. slice():截取数组，返回截取后的数组。接收两个参数，左闭右开。
6. toString():将数组转换为字符串，和join()方法不用任何参数调用的结果一样
7. toLocaleString():将数组转换为字符串并且使用本地化分隔符将这些字符串连接起来。

#### 6.ECMAScript 5 中的数组方法

1. forEach():
    1. 定义：forEach() 方法对数组的每个元素执行一次提供的函数。
    2. 语法：array.forEach(callback[, thisArg])
    3. 参数说明:
        1. callback 为数组中每个元素执行的函数，该函数接收三个参数：
            1. currentValue(当前值)数组中正在处理的当前元素。
            2. index(索引)数组中正在处理的当前元素的索引。
            3. arrayforEach()方法正在操作的数组。
        2. thisArg可选 可选参数。当执行回调函数时用作this的值(参考对象)。
    4. 示例：


```javascript
var arr = ['a', 'b', 'c'];

arr.forEach(function(element) {
    console.log(element);
});

// a
// b
// c
```javascript


2. map()
    1. 定义：调用每个元素传递给指定函数，并返回一个新数组，包含该函数的返回值。
    2. 示例:


```javascript
var a=[23,4,5,6,7,8];
var b=a.map(function(x){return x+x})        //[46,8,10,12,14,16];
```javascript
    

3. filter()
    1. 定义：返回调用函数的一个子集。传递的函数是用来逻辑判断的。如果返回true，就会返回一个子集数组。
    2. 示例:
    

```javascript
var a=[23,4,5,6,7,8];
var b=a.filter(function(x){return x>5})     //[23,6,7,8];
```javascript

4. some()和every()

>对数组进行逻辑判断，返回true或false，some和every差异顾名思义。

5. reduce()和reduceRight()
    1. 定义：reduce() 方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。
    2. 注意: reduce() 对于空数组是不会执行回调函数的。
    3. 参数说明：
    

```javascript
function(total,currentValue, index,arr)

参数	        描述
total	        必需。初始值, 或者计算结束后的返回值。
currentValue	必需。当前元素
currentIndex	可选。当前元素的索引
arr	            可选。当前元素所属的数组对象。
```javascript

>reduceRight() 方法的功能和 reduce() 功能是一样的，不同的是 reduceRight() 从数组的末尾向前将数组中的数组项做累加。

6. indexOf()和lastIndexOf()

> indexOf()搜索第一个符合值得索引，没有返回-1，lastIndexOf()寻找方向相反

#### 7.类数组对象
1. javascript数组特性
    - 当有新元素添加到列表时，自动更新length
    - 设置较小length时将截断数组
    - 会从Array.prototype中继承一些方法
    - 其类属性为“Array
    
2. 类数组举例：arguments
3. 在es5中所有的数组方法都是通用的

#### 8.作为数组的字符串

>比如可以这样访问某个字符串


```javascript
var a='abcdefg';
alert(a[0]);            //a 
```javascript


