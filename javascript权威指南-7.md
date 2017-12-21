#### 1. 函数概述

1. 定义：只定义一次，却可以被执行和调用多次的javascript代码。
2. 构成：
    - 函数名称标识符：函数名称是函数声明语句的必须部分。它的用途就像变量的名称一样。新定义的函数对象会赋值给这个变量。对函数定义表达式来说，这个名字是可选的，如果存在，改名字只存在于函数体中，并只带该函数对象本身。
    - 一对圆括号：其中包含0或多个逗号隔开的标识符列表。这些标识符是函数的参数名称，它们就像函数体中的局部变量一样。
    - 一对花括号：其中包含0或多条javascript与语句。这些语句构成了函数体，一旦被调用就会执行这些语句。
3. 其他：
    - 函数表达式可以包含名称，这在递归时很有用
    - 函数表达式也可以作为参数传给其他函数

4. 函数语句声明的实质：实际上声明了一个变量，并把一个函数对象赋值给它。相对而言，定义函数表达式时并没有声明一个变量。函数可以命名，如果一个函数定义表达式包含名称，函数的局部作用域将会包含一个绑定到函数对象的名称。实际上，函数的名称将成为函数内部的一个局部变量。

5. 函数提升：以表达式方式定义的函数不具备提升能力，虽然被赋值的变量提升了，但是赋值没有提升，所以无法在函数定义之前调用。

6. return语句：导致函数停止，并返回它的表达式（如果存在）的值给调用者。如果没有相关表达式，return会返回undefined，如果没有return语句，会返回undefined给调用者。

7. 函数是可以嵌套的。

#### 2. 函数调用

1. 方式：
    - 作为函数
    - 作为方法
    - 作为构造函数
    - 通过call、apply间接调用
    
2. 函数调用

```javascript
function add(x,y){
    return x+y;
}

add(1,2)            //3
```

3. 方法调用

```javascript
var o={
    add:function(x,y){
       return x+y; 
    }
}

o.add(1,2);         //3
```

>方法调用和函数调用的区别：调用上下文（方法调用的调用上下文为拥有此方法的对象）

4. 方法链

>当方法不需要返回值时，最好返回this，这样可以达到链式调用的特点

>需要注意的是this是一个关键字,无法给this赋值，另外this会因为环境而改变，有时存储this的值（指向）是必须的技巧。

5. 构造函数调用
    1. 构造函数都做了什么？
        - 创造一个新的空对象
        - 这个对象继承了构造函数的prototype属性
        - 将这个对象作为调用上下文
        - 因此可以用this引用这个新创建的对象
    2. 构造函数通常没有return，但如果显示的写了会怎样？
        - 如果返回值时一个基本类型（原始值），则会被忽略
        - 如果返回值是引用类型（数组，对象或者函数）的数据，那么这个函数作为构造函数用new运算符执行构造时，运算的结果将被它的返回值取代，这时候，构造函数体内的this值丢失了，取而代之的是被返回的对象。
    3. 构造函数的调用如下：

```javascript
function Add(){
    //代码
}
Add.prototype.check=function(){
    //代码
}

new Add();  
```

6. 间接调用（call,apply）


```javascript
function add(a,b){
    return a+b;
}

add.call(this,2,5);     //7

add.apply(this,[2,5]);  //7
```

>具体的后面介绍

#### 3. 函数的实参和形参

1. 可选形参


```javascript
function add(a,b,c){
    var c=c||3;
    return a+b+c
}

add(1,2)            //6
```
>另外，实参在传递时，也可以选择传入一个null作为占位符，当然也可以用undefined


>当调用函数传入的实参个数超过函数定义时的形参个数时，无法直接获得为，未命名值的引用。参数对象解决了这个问题。在函数体内，标识符arguments时指向实参对象的引用，实参对象是一个类数组对象，可以通过数字下标访问。

2. 可变长的实参列表：实参对象
    1. 作用：
        - 可以通过验证实参个数来进行相应操作
        - 让函数可以操作任意数量的实参。

    2. 可以接受任意数实参的函数也称为“不定实参函数”
    
    3. 注意：
        - arguments并不是真正的数组，它是一个实参对象，每个实参对象都包含以数组为索引的一组元素以及length属性，但它不是真正的数组。
        - 在严格模式下，arguments会变成一个保留字，无法使用arguments作为实参名或者局部变量名，也不能给arguments赋值。
    
    4. callee和caller：严格模式下对这两个属性读写都会造成错误。但非严格模式下，callee指代正在执行的函数，而caller是非标准的，虽然大多数浏览器实现了这个属性。callee对递归还是非常有用的。
    

```javascript
function fac (x){
    if(x<=1){
        return 1;
    }
    return x*arguments.callee(x-1);
}
```

#### 4. 自定义函数属性
1. javascript函数并不是原始值，而是一种特殊对象，也就是说可以拥有属性
2. 使用情况：当一个函数需要一个“静态”变量来调用保持某个值不变，最方便的就是给函数定义属性。
3. 如下:


```javascript
function timer(){
    timer.counter=0;
    return timer.counter++;
}
```

#### 5. 作为命名空间的函数

1. 作法：定义一个匿名函数并且立即调用
2. 示例：


```javascript
(function(){
    //代码
})()
```
#### 6. 闭包

1. 定义：当一个函数嵌套另一个函数，外部函数将嵌套函数对象作为返回值返回时。
2. 作用：访问私有变量。


```javascript
function scope(){
    var a=3;
    return function(){
        return a;
    }
}


alert(a);               //a is not defined

alert(scope()());       //3
```
#### 7. length属性

- 在函数体内arguments.length表示传入函数参数的个数。
- 函数本身的length是只读属性，代表形参个数，也就是函数定义时期望传入的参数数量（设定的参数数量）
- prototype属性：每个函数都要包含一个prototype属性。这个属性是指向一个对象的引用，这个对象称作“原型对象”。每个函数都有不同的原型对象，当函数用作构造函数时，新创建的对象就会从原型对象上继承。

#### 8. call()、apply()

1. 概述：两者用法很相似
2. 示例：


```javascript
function add(x,y){
    return x+y;
}

add.call(this,3,4);

add.apply(this,[3,4]);
```

3. es5严格模式下，call()和apply()的第一个实参都会变成this的值，哪怕传入的实参是原始值甚至null或者undefined。es3非严格模式下,传入的null和undefined都会被全局对象替代，其他原始值则会被相应的包装对象所替代。

4. 差别：传入实参的形式不同
    - call是直接传入，apply是放入一个数组

#### 9. bind()方法

1. 概述：es5中新增的方法
2. 用法：把一个方法和一个对象两者关联起来
3. 示例：


```javascript
function add(a,b){
    return this.x+a+b;
}

var o={
    x:1
}

var ads=add.bind(o);
ads(1,2);               //4
```

>bind的实现


```javascript
if (!Function.prototype.bind) {
 Function.prototype.bind = function (oThis) {
  if (typeof this !== "function") {
   // closest thing possible to the ECMAScript 5 internal IsCallable function
   throw new TypeError("Function.prototype.bind - what is trying to be bound is not callable");
  }
 
  var aArgs = Array.prototype.slice.call(arguments, 1), 
    fToBind = this, 
    fNOP = function () {},
    fBound = function () {
     return fToBind.apply(this instanceof fNOP && oThis
                 ? this
                 : oThis || window,
                aArgs.concat(Array.prototype.slice.call(arguments)));
    };
 
  fNOP.prototype = this.prototype;
  fBound.prototype = new fNOP();
 
  return fBound;
 };
}
```
#### 10. toString()方法
>函数也有toString()方法，实际上大多数函数的toString()方法都是返回完整代码


```javascript
function add(a,b){
    return a+b;
}

document.write(add.toString());

//function add(a,b){ return a+b;}
```

#### 11. Function构造函数


```javascript
var f=new Function('x','y','return x+y');

var f=function(x,y){
    return x+y;
}
```

>上面两段代码几乎等价

>关于构造函数的几个注意点：

- Function()构造函数允许javascript在运行时动态创建并编译函数。
- 每次调用Function()构造函数都会解析函数体，并创建新的函数对象。如果是在一个循环或多次调用的函数中执行这个构造函数，执行效率会受影响。相比之下，循环中嵌套函数和函数定义表达式则不会每次执行都重新编译。
- 构造函数创建的函数并不是使用词法作用域，相反，函数体代码的编译总是会在顶层函数执行。

#### 12. 使用函数处理数组

>比如计算一堆数字的平均值和标准差


```javascript
var sum=function(x,y){return x+y}
var square=function(x){return x*x}

var data=[1,1,3,5,5];
var mean=data.reduce(sum)/data.length;
var deviations=data.map(function(x){return x-mean});
var stddev=Math.sqrt(deviations.map(square).reduce(sum)/(data.length-1));
```
#### 13. 高阶函数

1. 定义：操作函数的函数，接收一个或者多个函数作为参数
2. 示例：


```javascript
var Moqi = function(p1){
    this.add = function (p2){
        return p1 + ' ' + p2;
    };
    return add;
};

console.log(Moqi('Hello')('World'));
```

#### 14. 不完全函数

1. 函数f()的bind()方法返回一个新函数，给新函数传入特定的上下文和一组指定的参数，然后调用f()。

>我们说它把函数 "绑定至" 对象并传入一部分参数。bind()方法只是将实参放在（完整实参列表的）左侧，也就是说传入bind()的实参都是放在传入原始函数的实参列表开始的位置，但有时我们期望将传入bind()的实参放在（完整实参列表的）右侧：


```javascript
 //实现一个工具函数将类数组对象（或对象）转换为真正的数组

    //在后面的示例代码中用到了这个方法将arguments对象转换为真正的数组

    function array(a,n){ return Array.prototype.slice.call(a,n||0); }

    //这个函数的实参传递至左侧

      function partialLeft(f /*,...*/){

           var args = arguments; //保存外部的实参数组

           return function(){   //并返回这个函数

             var a= array(args,1); //开始处理外部的第1个args

             a = a.concat(array(arguments)); //然后增加所有的内部实参

            return f.apply(this,a); //然后基于这个实参列表调用f()

        };

      }

    //这个函数的实参传递至右侧

     function partialRight(f/*,...*/){

        var args = arguments; //保存外部实参数组

        return function(){

           var a = array(arguments); //从内部参数开始

           a = a.concat(array(args,1)); //然后从外部第1个args开始添加

           return f.apply(this,a); //最后基于这个实参列表调用f()

          };

       }

    //这个函数的实参被用做模板

   //实参列表中的undefined值都被填充

   function partial(f/*,...*/){

      var args = arguments; //保存外部实参数组

      return function(){

          var a = array(args,1); //从外部args开始

          var i = 0,j =0;

          //遍历args,从内部实参填充undefined值

          for(;i<a.length;i++)

             if(a[i] === undefined) a[i] = arguments[j++];

          //现在将剩下的内部实参都追加进去

            a = a.concat(array(arguments,j))

            return f.apply(this,a);

         };

        }

      //这个函数带有三个实参

      var f = function(x,y,z){ return x*(y-z); };

      //注意这三个不完全调用之间的区别

      partialLeft(f,2)(3,4)  //=>-2:绑定第一个实参：2*(3 - 4

      partialRight(f,2)(3,4) //=>6:绑定最后一个实参：3*(4 -2)

      partial(f,undefined,2)(3,4) //=>-6:绑定中间的实参：3*(2-4)
```
   

2. 利用已有的函数来定义新的函数

>利用这种不完全函数的编程技巧，可以编写一些有意思的代码，利用已有的函数来定义新的函数：


```javascript
var increment = partialLeft(sum,1);

   var cuberoot = partialRight(Math.pow,1/3);

   String.prototype.first = partial(String.prototype.charAt,0);

   String.prototype.last = partial(String.prototype.substr,-1,1);
   
```

>当将不完全调用和其他高阶函数整合在一起的时候，事情就变得格外有趣了。比如，这里的例子定义了not()函数，它用到了刚才提到的不完全调用：
```javascript
   var not = partialLeft(compose,function(x){ return !x;});

   var even = function(x){ return x%2 ==0; };

   var odd = not(even);

   var isNumber = not(isNaN);
```


>我们也可以使用不完全调用的组合来重新组织平均数和标准差的代码，这种编程风格是非常纯粹的函数式编程：


```javascript
     var data = [1,1,3,5,5]; //我们要处理的数据

     var sum = function(x,y){ return x+y; };  //两个初等函数

     var produce = function(x,y){ return x*y; };

     var neg = partial(product,-1);

     var square = partial(Math.pow,undefined,2);

     var sqrt = partial(Math.pow,undefined, .5);

     var reciprocal = partial(Math.pow,undefined,-1);

     //现在计算平均值和标准差，所有的函数调用都不带运算符

      var mean =product(reduce(data,sum),reciprocal(data.length));

      var stddev = sqrt(product(reduce(map(data,compose(squaer,partial(sum,neg(mean)))),sum),reciprocal(sum(data.length,-1))));
```

#### 15. 记忆

1. 定义：函数记忆是指将上次的计算结果缓存起来，当下次调用时，如果遇到相同的参数，就直接返回缓存中的数据。
2. 示例：


```javascript
function add(a, b) {
  return a + b;
}
 
// 假设 memorize 可以实现函数记忆
var memoizedAdd = memorize(add);
 
memoizedAdd(1, 2) // 3
memoizedAdd(1, 2) // 相同的参数，第二次调用时，从缓存中取出数据，而非重新计算一次

```

>tips：函数记忆只是一种编程技巧，本质上是牺牲算法的空间复杂度以换取更优的时间复杂度，在客户端 JavaScript 中代码的执行时间复杂度往往成为瓶颈，因此在大多数场景下，这种牺牲空间换取时间的做法以提升程序执行效率的做法是非常可取的。
