#### 1. 对象概述：
对象是一种复合值。它将多个值聚合在一起可以通过名字访问这些值。对象可以看成无序集合，每个属性都是一个名值对。对象除了自己的属性方法，还可以从一个称为原型的对象上继承属性。这是“原型式”继承是javascript核心。
#### 2. javscript语言:
javscript语言是动态的，可以新增属性也可以删除属性。
除了字符串、数字、true、false、null和undefined外，javascript中的值都是对象。而字符串、数字、true、false、null和undefined它们的行为和不可变对象非常类似。
#### 3. 属性:
属性包括名字和值。属性名可以使包含字符串在内的任意字符串，但对象中不能存在两个同名属性除了名字和值，每个属性都有一些与之相关的值，称为“属性特征”

- 可写，表明是否可以设置该属性的值
- 可枚举，表明是否可以通过for in循环返回该属性值
- 可配置，表明是否可以删除或修改该属性的值

除了包含属性之外，每个对象还有三个相关的对象特征

- 对象的原型：指向另一个对象，对象的属性都是继承自它的原型对象
- 对象的类：是一个标识对象类型的字符串
- 对象的拓展标记：指明了是否可以向该对象添加新属性

最后用下面术语对三类javascript对象和两类属性做区分
- 内置对象：由ECMAScript规范定义的对象或类。例如数组、函数
- 宿主对象:所有非本地对象都是宿主对象（host object），即由ECMAScript 实现的宿主环境提供的对象。所有 BOM 和 DOM 对象都是宿主对象。
- 自定义对象：由运行中的javascript代码创建的对象
- 自有属性：直接在对象上定义的属性
- 继承属性：在对象原型对象中定义的属性

#### 4. 创建对象
1. 字面量
2. new运算符


```
字面量：

var obj={};
obj.x=3;

var lcg={
    y:'yes'
}
```

```
new运算符
var obj=new Object();
obj.z=33;
```

#### 5. 原型

>每个对象都有一个关联对象（除了null），那就是原型。

1. 通过{}和new运算符创造的对象都继承自Object.prototype。就像new Date()创造的实例对象的属性继承自Date.prototype一样。而这一系列原型对象所组成的就是所谓的原型链。
2. 没有原型的对象并不多，Object.prototype就是其中一个。

#### 6. Object.create()
1. 语法：Object.create(proto[, propertiesObject])
2. 参数说明：
    1. proto
新创建对象的原型对象。
    2. propertiesObject 可选。如果没有指定为undefined，则是要添加到新创建对象的可枚举属性（即其自身定义的属性，而不是其原型链上的枚举属性）对象的属性描述符以及相应的属性名称。这些属性对应Object.defineProperties()的第二个参数。
    3. 返回值：在指定原型对象上添加新属性后的对象。
    4. 注意：如果proto参数不是 null 或一个对象，则抛出一个 TypeError 异常。
    5. 示例：（其实就是个寄生组合式继承）
    

```
// Shape - superclass
function Shape() {
  this.x = 0;
  this.y = 0;
}

// superclass method
Shape.prototype.move = function(x, y) {
  this.x += x;
  this.y += y;
  console.info('Shape moved.');
};

// Rectangle - subclass
function Rectangle() {
  Shape.call(this); // call super constructor.
}

// subclass extends superclass
Rectangle.prototype = Object.create(Shape.prototype);
Rectangle.prototype.constructor = Rectangle;

var rect = new Rectangle();
```


#### 7. 继承

>javascript对象具有“自有属性”，也具有从原型对象上继承的属性。

1. 如果要给一个对象的属性赋值，如果已经有了这个属性，且这个属性是自有的，那么这个操作只会改变属性的值。如果不存在，那么就会添加并赋值。如果是继承来的，那么这个属性会被同名属性覆盖。

#### 8. 删除属性

1. delete可以删除属性，但它仅仅是断开属性和宿主对象的联系而不会去操作属性中的属性。
2. delete只能删除自有属性，无法删除继承属性。
3. 成功删除时delete会返回一个true，否则返回false。如果delete后面跟的不是属性访问表达式，也会返回true。
4. delete无法删除可配置型为false的属性。
5. 在非严格模式中，这些情况下delete会返回false。
    

```
delete Object.prototype //属性是不可配置的

var x=1;
delete this.x           //无法删除全局变量

function a(){}
delete this.a;          //同样无法删除全局函数
```

#### 9. 检测属性
1. 常见的方法：
    1. in运算符
    2. hasOwnproperty()
    3. propertyIsEnumerable()
2. 
    1. in运算符返回true(不区分是自有属性还是继承属性)
    2. hasOwnproperty()只检测是不是自有属性，是的话返回true
    3. propertyIsEnumerable()只有是自有属性同时可枚举性为true才会返回true
    4. 下面是示例

```
var o={a:12}
"a" in o ; //true 
```


```
var o={a:12}
o.hasOwnproperty('x'); //true
```


```
var o={a:12}
o.propertyIsEnumerable('x'); //true
```

    
3. 另一种更简单的方法


```
var o={a:12}
o.x !== undefined  //true
```
>但是上述方法有一个缺憾，比如


```
var o={a:undefined}
o.x !== undefined  //false
```

>但是显然上面的对象是存在这个属性的

#### 9. 枚举属性
>除了for in循环外，es5还定义了两个可以枚举属性名的函数

1. Object.keys()

>它返回一个数组，这个数组由可枚举的自有属性名称组成。

2. Object.getOwnpropertyNames();

>它也返回一个数组，这个数组由自有属性名称组成。(不可枚举的一样能取到)

#### 10.getter和setter

1. 对象的属性值可以用一或两个方法替代，这两个方法就是getter和setter。由getter和setter定义的属性称作“读取器属性”。它不同于“数据属性”，数据属性只有一个简单的值。
2. 与数据属性不同，如果属性同时具有getter和setter两个方法，它就具有可读写性。如果只具有getter它就只有可读性，反之只有可写性。
3. 和数据属性一样，存储器属性是可以继承的。

>下面用getter实现一种“神奇属性”。


```
var random={
    get octet(){
        return Math.floor(Math.random()*256)
    },
    get uint16(){
        return Math.floor(Math.random()*65536)
    },
    get int16(){
        return Math.floor(Math.random()*65536)-32768;
    }
}
```

#### 11.对象的三个属性

1. 原型属性
    1. 定义：对象的原型属性是继承来的
    2. 检测：isPrototypeOf()方法


```
a.isPrototypeOf(b);
```
2. 类属性
    1. 定义：用来表示对象类型信息的一个字符串
    2. 获取：调用toString()，然后返回第八个到倒数第二个位置之间的字符
    3. 很多对象继承的toString()被重写，为了调用正确的toString()，得间接调用Function.call()
    
3. 可拓展性
    1. 定义：表示是否可以给对象添加新属性
    2. 判断：Object.preventExtensible()
    3. 转换为不可拓展：Object.preventExtensions()
    4. Object.seal():也能设置不可拓展，同时可以把自有属性设置为不可配置。
    
#### 12.对象序列化
1. 定义：将对象的状态转为字符串，也可将字符串还原为对象
2. 方法：JSON.stringify()和JSON.parse()
3. 测试：


```
var o={x:1,y:{z:2}};            //测试对象
var s=JSON.stringify(o);
var p=JSON.parse(s);
```

#### 13.对象方法

1. toString():返回调用这个方法的对象值的字符串(可以接收参数，转换进制)
2. toLocaleString():返回调用这个方法对象的本地化字符串。
3. toJSON():Object.prototype实际上没有定义这个方法，但对于需要序列化的对象来说，JSON.stringify()方法会调用toJSON()。如果待序列化的对象存在这个方法则调用它，返回序列化结果。
4. valueOf():当需要将对象转换为某种非字符串时才会调用。