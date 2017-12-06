#### 1. 使用构造函数定义范围类


```
   function Range(from,to) {
       this.from=from;
       this.to=to;
   }

   Range.prototype={
       includes:function (x) {
           return this.from<=x&&x<=this.to;
       },
       forEach:function (f) {
           for(let x=Math.ceil(this.from);x<=this.to;x++){
               f(x);
           }
       }
   };
   let ranges=new Range(1,10);
   console.log(ranges.includes(3));     //true
   ranges.forEach(console.log);         //1-10
```

#### 2. constructor属性

1. 每个javascript函数（除es5 Function.BIND()方法）都会自动拥有一个prototype属性。这个属性的值是一个对象。这个对象包含唯一一个不可枚举的属性constructor。


```
function F(){}
var p=F.prototype;
var c=p.constructor;
c===F                   //true
```
2. 可以看出来构造函数原型中预先定义好了constructor属性。这意味着通常继承的constructor均指代它们的构造函数。由于构造函数是类的“公共标识”，因此这个constructor属性为对象提供了类。


```
var o=new F();
o.constructor===F       //true
```

3. 问题：之前写的范围了的constructor属性被一个新的对象覆盖替换掉了，所以Range类的实例不具有constructor属性，解决方法有两个。
    1. 显示的指定constructor属性
    2. 在预定义原型时依次给原型添加方法

>显示的指定constructor属性
    
```
   function Range(from, to) {
    this.from = from;
    this.to = to;
}

Range.prototype = {
    constructor: Range,
    includes: function(x) {
        return this.from <= x && x <= this.to;
    },
    forEach: function(f) {
        for (let x = Math.ceil(this.from); x <= this.to; x++) {
            f(x);
        }
    }
};
let ranges = new Range(1, 10);
console.log(ranges.includes(3)); //true
ranges.forEach(console.log); //1-10

```

>在预定义原型时依次给原型添加方法

```
   function Range(from,to) {
       this.from=from;
       this.to=to;
   };

   Range.prototype.includes=function(x){
       return this.from<=x&&x<=this.to;
   };
   
   Range.prototype.forEach=function(f){
       for(let x=Math.ceil(this.from);x<=this.to;x++){
               f(x);
           }
   }
   
   let ranges=new Range(1,10);
   console.log(ranges.includes(3));     //true
   ranges.forEach(console.log);         //1-10    
  
```

#### 3. 类的扩充

1. 概述：javascript中基于原型的继承机制时动态的：也就是说如果创建对象之后原型的属性发生变化，也会影响到这个原型的所有实例对象。这也就意味着我们可以通过给原型对象添加方法来扩充javascript类。
2. 举例：


```
if(!Function.prototype.bind){
    Function.prototype.bind=function(o){
        //代码
    }
}
```

3. 可以给Object.prorotype添加方法，从而使所有对象都可以调用这些方法。但这种做法不推荐。

#### 4. 类和类型

1. instanceof运算符:实际上检测的是对象的继承关系，而不是创建对象的构造函数。
2. isPrototypeOf()方法：检测对象原型链上是否存在某个特定的原型对象。
>两者的缺点：无法通过对象来获取类名

>instanceof另一个缺点：B框架页面的Array实例不是A框架页面的Array实例。instanceof返回false

3. constructor属性
>另一种识别对象是否属于某个类的方法是使用constructor属性，因为构造函数是类的公共标识。

- 缺点：
    - 和instanceof一样，无法在多个执行上下文环境中工作
    - 并不是所有的javascript对象都有constructor属性

#### 5. 构造函数的名称

>另一种可能性的解决方案是使用构造函数的名字而不是构造函数本身作为标识符。一个窗口的Array和另一个窗口的Array名字是一样的。在一些javascript中为函数提供了非标准的属性name，用来表示函数名。


```
function type(o){
    var t,c,n;
    if(o===null){
        return "null"
    }
    if(o!==o){
        return "nan"
    }
    if((t=typeof o)!=="objcet"){
        return t;
    }
    if((c=classof(o))!=="Object"){
        return c;
    }
    if(o.constructor&&typeof o.constructor === "function" && (n =o.constructor.getName())){
        return n;
    }
    return "Object";
    function classof(o){
        return Object.prototype.toString.call(o).slice(8,-1);
    }
    Function.prototype.getNmae=function(){
        if("name" in this) {
            return this.name;
        }
        return this.name=this.toString().match(/function\s*([^(]*])\(/)[1];
    };
}
```
#### 6. 鸭式辩型

1. 定义：关注对象能做什么，而不是对象的类是什么

>James Whitcomb Riley提出像鸭子一样走路、游泳和嘎嘎叫的鸟就是鸭子

>主要对象包含walk(),swim(),bike()这三个方法就可以作为参数传入

>利用鸭式辨型实现的函数


```
function quackImplements(o/*,...*/){
    for(var i=1; i<arguments.length;i++){
        var arg=arguments[i];
        switch(typeof arg){
            case 'string':
                if(typeof o[arg]!=="function")
                    return false;
                continue;

            case 'function':
                arg=arg.prototype;

            case 'object':
                for (var m in arg){
                    if(typeof arg[m]!=="function") continue;
                    if(typeof o[m]!=="function") return false;

            }
        }
    }
    return true;
}
```
- 对于字符串直接检查命名方法

- 对于对象检查是否有同名方法

- 对于函数检查构造函数的原型对象中是否有相同方法

#### 7. javascript中的面向对象技术

1. 集合类例子：


```
function Set(argument) {
    this.values = {};
    this.n = 0;
    this.add.apply(this, arguments);
}

Set.prototype.add = function(argument) {
    for (var i = 0; i < arguments.length; i++) {
        var val = arguments[i];
        var str = Set._v2s(val);
        if (!this.values.hasOwnProperty(str)) {
            this.values[str] = val;
            this.n++;
        }
    }
    return this;
};

Set.prototype.remove = function() {
    for (var i = 0; i < arguments.length; i++) {
        var str = Set._v2s(arguments[i]);
        if (this.values.hasOwnProperty(str)) {
            delete this.values[str];
            this.n--;
        }
    }
    return this;
};

Set.prototype.contains = function() {
    return this.values.hasOwnProperty(Set._v2s(value));
};

Set.prototype.foreach = function(f, context) {
    for (var s in this.values) {
        if (this.values.hasOwnProperty(s)) {
            f.call(context, this.values[s]);
        }
    }
};

Set._v2s = function(val) {
    switch (val) {
        case undefined:
            return 'u';
        case null:
            return 'n';
        case true:
            return 't';
        case false:
            return 'f';
        default:
            switch (typeof val) {
                case 'number':
                    return '#' + val;
                case 'string':
                    return '"' + val;
                default:
                    return '@' + objectId(val);
            }

    }
}

function pbjectId(o) {
    var prop = "|**objectid**|";
    if (!o.hasOwnProperty(prop)) {
        o[prop] = Set._v2s.next++;
    }
    return o[prop];
}
Set._v2s.next = 100;

```
2. 枚举类例子：

>使用枚举类型定义一副扑克牌

```

定义一个表示“ 玩牌” 的类

function Card(suit, rank) {
    this.suit = suit;
    this.rank = rank;
}
//使用枚举类型定义花色和点数
Card.Suit = enumeration({ Clubs: 1, Diamonds: 2, Hearts: 3, Spades: 4 });
Card.Rand = enumeration({ Two: 2, Three: 3, Four: 4, Five: 5, Six: 6, Seven: 7, Eight: 8, Nine: 9, Ten: 10, Jack: 11, Queen: 12, King: 13, Ace: 14 });
Card.prototype.toString = function() {
    return this.rank.toString() + "of" + this.suit.toString();
}

//比较扑克牌中两张牌的大小
Card.prototype.compareTo = function(that) {
    if (this.rank < that.rank) return -1;
    if (this.rank > that.rank) return 1;
    return 0;
}

//以扑克牌的玩法规则对牌进行排序的函数
Card.orderByRank = function(a, b) {
    returna.compareTo(b));

//以桥牌的玩法规则对扑克牌进行排序的函数
Card.orderBySuit = function(a, b) {
    if (a.suit < b.suit) return -1;
    if (a.suit > b.suit) return 1;
    if (a.rank < b.rank) return -1;
    if (a.rank > b.rank) return 1;
    return 0;
};

//定义用以表示一副标准扑克牌的类
function Deck() {
    var cards = this.cards = [];
    Card.Suit.foreach(function(s) {
            Card.Rank.foreach(function(r) {
                    cards.push(new Card(s, r);
                    });
            });
    }

    //洗牌的方法，重新洗牌并返回好的牌
    Deck.prototype.shuffle = function() {
        //遍历数组中的每个元素，随机找出牌面最小的元素，并与当前遍历元素交换
        var deck = this.cards,
            len = deck.length;
        for (var i = len - 1; i > 0; i--) {
            var r = Math.floor(Math.random() * (i + 1)),
                temp;
            temp = deck[i], deck[i] = deck[r];, deck[r] = temp;
        }
        return this;
    }

    //发牌方法：返回牌的数组
    Deck.prototype.deal = function(n) {
        if (this.cards.length < n) throw "Out of cards";
        return this.cards.splice(this.cards.length - n, n);
    };
    //创建一副新扑克牌，洗牌并发牌
    var deck = (new Deck()).shuffle();
    var hand = deck.deal(13).sort(Card.orderBySuit);
```


3. 标准转换方法
    - toString():返回一个可以表示这个对象的字符串
    - toLocaleString():和上面的极为相似，通过本地敏感性的方式将对象转换为字符串
    - valueOf():用来把对象转换为原始值
    - toJSON():这个方法由JSON.stringify()自动调用的。

>在下面的例子中，Set类并没有定义上述方法中的任何一个。Javascript中没有那个原始值表示集合，因此也没必要定义valueOf()方法，但该类包含toString()、toLocaleString()、和toJSON()方法。可以用如下代码来实现。注意extend()函数的用法，这里使用extend()来向Set.prototype来添加方法：


```
 //将这些方法添加至Set类型的原型对象中
            extend(Set.prototype, {
                //将集合转换为字符串
                toString: function() {
                    var s = "{",
                        i = 0;
                    this.foreach(function(v) {s += ((i++ > 0) ? "," : "") + v;});
                    return s + "}";
                },
                //类似toString,但是对于所有的值都将调用toLocaleString()
                toLocaleString: function() {
                    var s = "{",i = 0;
                    this.foreach(function(v) {
                                if (i++ > 0) s += ",";
                                    if (v == null) s += v; //null和undefined
                                    else s += v.toLocaleString(); //其它情况
                                });
                            return s + "}";
                        },
                //将集合转换为值数组
                toArray:function() {
                    var a = [];
                    this.foreach(function(v) {a.push(v);});
                    return a;
                }
            });
             //对于要从JSON转换为字符串的集合都当做数组来对待
            Set.prototype.toJSON = Set.prototype.toArray;
```

    
4. 比较方法
>javascript比较对象时，比较的是引用而不是值。也就是说给定两个对象的引用，如果要看它们是否指向同一个对象，不要检查这两个对象是否具有相同的属性名和属性值，而是直接比较这两个单独的对象是否相等，或者比较它们的顺序。

>如下：给Set添加equals()方法

```
Set.prototype.equals = function(that){
  if(this===that) return true;
  if(!(that instanceof Set)) return false;
  if(this.size()!=that.size()) return false;
  try{
    this.foreach(function(v){if(!that.contains(v)){throw false;});
    return true;
   }catch(x){
     if(x===false) return false;
    throw x
   }
}
同样道理我们可以定义一个compareTo方法，如给Range类加一个这样的方法
Range.prototype.compareTo = function(that){
  if(!(that instanceof Range)){
      throw new Error("Can't compare a Rangewith"+that);
   }
  var diff = this.from-that.from;
  if(diff==0)diff=this.to-that.to;
  return diff;
}
 
则我们对range对象数组排序可以如：
ranges.sort(function(a,b){return  a.compareTo(b);});
```


5. 方法借用
    1. javascript方法无非是一些简单的函数，赋值给了对象的属性，可以通过对象来调用它。一个函数可以赋值给两个属性，然后作为两个方法来调用它。

    2. 多个类中的方法可以共用一个单独函数。比如，Array类通常定义了一些内置的方法，如果定义了一个类，它的实例是类数组的对象，则可以慈宁宫Array.prototype中函数复制至所定义的类的原型对象中。如果以经典面向对象语言的视觉来看javascript的话，把一个类的方法用到其他类中的做法也陈做“多重继承”（multiple inherittance）。然而在javaScript并不是经典的面向对象语言，我们更倾向于将这种方法重用更正式的称为“方法借用”（borrowing）。
    

```
             /*方法借用的泛型实现*/
            var genric = {
                //返回一个字符串，这个字符串包含构造函数的名字（如果构造函数包含名字）
                //以及所有非继承来的、非函数属性的名字和值
                toString: function() {
                    var s = '['
                        //如果这个对象包含构造函数，且构造函数包含名字
                        //如果这个名字作为返回字符串的一部分
                        //需要注意的是函数的名字属性属性是非标准的，并不是在所有的环境中都可用
                    if (this.constructor && this.constructor.name)
                        s += this.constructor.name + ":";
                    //枚举所有非继承且非函数的属性
                    var n = 0;
                    for (var name in this) {
                        if (!this.hasOwnProperty(name)) continue; //跳过继承来的属性
                        var value = this[name];
                        if (typeof value === "function") continue; //跳过方法
                        if (n++) s += ",";
                        s += name + '=' + value;
                    }
                    return s + ']';
                },
                //通过比较this和that的构造函数和实例属性来判断它们是否相等
                //这种方法只适合用于那行实例属性是原始值的情况，原始值可以通过"==="来比较
                //这里还处理一种特殊情况，就是忽略由set类添加的特殊属性
                equals: function(that) {
                    if (that == null) return false;
                    if (this.constructor !== that.constructor) return false;
                    for (var name in this) {
                        if (name === "|**object**|") continue; //跳过特殊属性
                        if (!this.hasOwnProperty(name)) continue; //跳过继承来的属性
                        if (this[name] !== that[name]) return false; //比较是否相等
                    }
                    return true; //如果所有属性都匹配，两个对象相等
                }
            };
```


6. 私有状态
 
>通过变量闭包在一个构造函数内模拟实现私有字段，调用构造函数会创建一个实例，为了做到这点，需要在构造函数内部定义一个函数，并将这个函数赋值给新创建对象的属性。

```
function Range(from, to) {
    this.from = function() {
        return from;
    };
    this.to = function() {
        return from;
    };
};

Range.prototype.includes = function(x) {
    return this.from() <= x && x <= this.to();
};

Range.prototype.forEach = function(f) {
    for (let x = Math.ceil(this.from()); x <= this.to(); x++) {
        f(x);
    }
}
```

>tips：这种封装技术造成了更多的系统开销。使用闭包来封装类的状态的类一定比不适用封装的状态变量的等价类运行速度更慢，并且占用更多内存。

7. 构造函数的重载和工厂方法

>可以通过重载这个构造函数让它根据传入参数的不同来执行不同的初始化方法。


```
function Set(argument) {
    this.value = {};
    this.n = 0;
    if (arguments.length == 1 && isArrayLike(arguments[0])) {
        this.add.apply(this, arguments[0]);
    } else if (arguments.length > 0) {
        this.add.apply(this, arguments);
    }
}
```


>这段定义的Set()构造函数可以显式的将一组元素作为参数列表传入，也可以传入元素组成的数组。但这个构造函数与有多义性，如果集合的某个成员是一个数组就无法通过构造函数来创建这个集合了。

>下面使用工厂方法来初始化Set对象


```
Set.fromArray=function (a) {
    s=new Set();          //创建一个空集合
    s.add.apply(s, a);    //将数组a的成员作为参数传入add()方法
    return s;             //返回新集合
}
```
#### 8. 子类
>在面向对象编程中，类b可以继承类a。我们将a成为父类，b成为子类。

1. 方法链：b的方法重载了a的方法，b中的重载方法可能会调用a中的重载方法，这种做法就叫做“方法链”。
2. 构造函数链：子类构造函数b有时需要调用父类构造函数a，这种做法叫做构造函数链。
3. 定义子类：用一个简单的函数创建简单的子类


```
function defineSubclass(superclass, constructor, methods, statics) {
    constructor.prototype = inherit(superclass.prototype);
    constructor.prototype.constructor = constructor;
    if (methods) {
        extend(constructor.prototype, methods);

    }
    if (statics) {
        extend(constructor, statics);
    }
    return constructor;
}
```

4. 构造函数和方法链

>定义子类时，我们往往希望对父类的进行修改或扩充，而不是完全替换掉。为了做到这一点，构造函数和子类的方法需要调用或链接到父类构造函数和父类方法。


```
function NonNullSet(){
//仅链接到父类
//作为普通函数调用父类的构造函数来初始化通过该构造函数调用创建的对象
Set.apply(this,arguments);
}
NonNullSet.prototype = inherit(Set.prototype);
NonNullSet.prototype.constructor = NonNullSet;
//为了将null和undefined排除在外，只须重写add()方法
NonNullSet.prototype.add = function(){
for(vari=0;i<arguments.length;i++){
    if(arguments[i]==null){
   throw new Error(“Can’t add null or undefinedto a NonNullSet”);
}
}
return Set.prototype.add.apply(this,arguments);
}
 
/*
这个函数返回具体Set类的子类，并重写该类的add()方法用以对添加的元素做特殊的过滤
*/
function filteredSetSubclass(superclass,filter){
var constructor =function(){
   superclass.apply(this,arguments);
};
var proto =constructor.prototype = inherit(superclass.prototype);
proto.constructor =constructor;
proto.add =function(){
     for( var i=0;i<arguments.length;i++){
          var v = arguments[i];
           if(!filter(v))throw (“value”+v+”rejectedby filter”);
}
superclass.prototype.add.apply(this,arguments);
}
return constructor;
}
```
>上例中用一个函数将创建子类的代码包装起来，这样就可以在构造函数和方法链中使用父类的参数，而不是通过写死某个父类的名字来使用它的参数。也就是说如果想修改父类，只须修改一处代码即可，而不必对每个用到父类类名的地方都做修改。
值得强调：类似这种创建类工厂的能力是js语言动态特性的一个体现，类工厂是一种非常强大和有用的特性。Java和c++中没有的。

5. 组合vs子类

>之前上面定义的集合可以根据特定的标准对集合成员做限制，而且使用了子类的技术来实现的这种功能，所创建的自定义子类使用了特定的过滤函数来对集合中的成员做限制。父类和过滤函数的每个组合都需要创建一个新的类。
然而还有更好的方法来写成这种需求，即OOP中一条广为人知的设计原则：“组合优于继承”可以利用组合的原理定义一个新的集合实现，它“包装”了另外一个集合对象，在将受限制的成员过滤掉之后会用到这个集合对象。下面将展示其工作原理。

```
var FilteredSet = Set.extend(function FilteredSet(set,filter){
   this.set =set;
   this.filter= filter;
},
{
  add:function(){
   if(this.filter){
      for(var i=0;i<arguments.length;i++){
        var v = arguments[i];
       if(!this.filter(v)){
             throw new Error(“FilteredSet:value “+v+”rejected by filter”);
       }
      }    
    }
    this.set.add.apply(this.set,arguments);
    return this;
  },
remove:function(){
    this.set.remove.apply(this.set,arguments);
    return this;
},
contains:function(v){return  this.set.contains();},
size:function(){return  this.set.size();},
foreach:function(f,c){this.set.foreach(f,c);}
});
```

>上面这个例子使用组合的一个好处是，只须创建一个单独的FilteredSet子类即可。可以利用这个类的实例来创建任意带有成员限制的集合实例。

5. 类的层次结构和抽象类
    1. 什么是抽象类：虚函数是类成员中的概念，是只做了一个声明而未实现的方法，具有虚函数的类就称之为抽象类，这些虚函数在派生类中才被实现。抽象类是不能实例化的，因为其中的虚函数并不是一个完整的函数，不能被调用。所以抽象类一般只作为基类被派生以后再使用。
    2. 示例：
    

```
/*抽象类和非抽象类Set类的层次结构*/
        //这个函数可以用作任何抽象方法，非常方便
        function abstractmethod() {throw new Error("abstract method");} 
        /*AbstractSet类定义了一个抽象方法：contains()*/
        function AbstractSet(){throw new Error("can not instantiate abstract classes");}
        AbstractSet.prototype.contains = abstractmethod;
        
        /**
         *NotSet是AbstractSet的一个非抽象子类
         * 所有不在其他集合中的成员都在这个集合中
         * 因为它是在其它集合中不可写的条件下而定义的，同时由于它的成员个数是无限个，因此它是不可枚举的
         * 我们只能用它来检测元素成员的归属情况
         * 注意我们使用了Function.prototype.extend()方法来定义这个子类
         **/
        var NotSet = AbstractSet.extend(
            function NotSet(set){this.set = set;},
            {
                contains:function(x){return !this.set.contains(x);},
                toString:function(x){return "~" + this.set.toString();},
                equals:function (that){
                    return that instanceof NotSet && this.set.equals(that.set);
                }
            }
        );
        
        /**
         * AbstractEnumerableSet是AbstractSet的一个抽象子类
         * 它定义了抽象方法size()和foreach(),然后实现了非抽象方法isEmpty、toArray、to[locale]String()和equals()方法
         * 子类实现了contains()、size()和foreach()，这三个方法可以很轻易的地调用这5个非抽象方法
         **/
        var AbstractEnumerableSet = AbstractSet.extend(
            function(){throw new Error("can not instantiate abstract classes");},
            {
                size:abstractmethod,
                foreach:abstractmethod,
                isEmpty:function(){return this.size()==0;},
                toString:function(){
                    var s = "{",i = 0;
                    this.foreach(function(v){
                        if(i++ > 0) s += ",";
                        s += v;
                    });
                    return s + "}";
                },
                toLocaleString:function(){
                    var s = "{", i = 0;
                    this.foreach(function(v){
                        if (i++ > 0) s += ",";
                        if (v == null) s += v; //null和undefined
                        else s += v.toLocaleString(); //其它情况下
                    });
                    return s + "}";
                },
                toArray:function(){
                    var a = [];
                    this.foreach(function(v){a.push(v);});
                    return a;
                },
                equals: function(that){
                    if(!(that instanceof AbstractEnumerableSet)) return false;
                    //如果他们的大小不同，则它们不相等
                    if(this.size() != that.size()) return false;
                    //检测每一个元素是否也在that中
                    try{
                        this.foreach(function(v){if (!that.contains(v)) throw false;});
                        return true; //所有的元素都匹配：集合相等
                    }catch(x){
                        if(x === false)return false; //集合不相等
                         throw x; //发生了其它的异常：重新抛出异常
                    }
                }
            }
        );
        
        /**
         * SingletonSet是AbstractEnumerableSet的非抽象子类
         * singleton的集合是只读的，它只包含一个成员
         **/
        var SingletonSet = AbstractEnumerableSet.extend(
            function SingletonSet(member){this.member = member;},
            {
                contains:function(x){return x === this.member;},
                size:function(){return 1;},
                foreach:function(f,ctx){f.call(ctx,this.member);}
            }
        );
        
        /**
         *AbstractWriteableSet是AbstractEnumerableSet的抽象子类
         * 它定义了抽象方法add()和remove()
         * 然后实现了非抽象方法union(),intersection()和difference()
         **/
        var AbstractWritableSet = AbstractEnumerableSet.extend(
            function(){throw new Error("can not instantiate abstract classes");},
            {
                add:abstractmethod,
                remove:abstractmethod,
                union:function(that){
                    var self = this;
                    that.foreach(function(v){self.add(v);});
                    return this;
                },
                intersection:function(that){
                    var self = this;
                    this.foreach(function(v){if(!that.contains(v)) self.remove(v);});
                    return this;
                },
                difference:function(that){
                    var self = this;
                    that.foreach(function (v){self.remove(v);});
                    return this;
                }
            }
        );
        
        /**
         *ArraySet是AbstractWritableSet的非抽象子类
         * 它以数组的形式表示集合中的元素
         * 对于它的contains()方法使用了数组的线性查找，因为contains()方法的算法复杂度是0(n)而不是0(1)
         * 它非常使用于相对小型的结合，注意，这里的实现用到了ECMAscript5数组方法indexof()和forEach()
         **/
        var ArraySet = AbstractWritableSet.extend(
            function ArraySet(){
                this.values = [];
                this.add.apply(this,arguments);
            },
            {
                contains:function(v){return this.values.indexOf(v) != -1;},
                size:function(){return this.values.forEach(f,c);},
                add:function(){
                    for (var i = 0; i<arguments.length; i++){
                        var arg =arguments[i];
                        if(!this.contains(arg)) this.values.push(arg);
                    }
                    return this;
                },
                remove:function(){
                    for(var i = 0; i < arguments.length; i++){
                        var p = this.values.indexOf(arguments[i]);
                        if(p == -1) continue;
                        this.values.splice(p,1);
                    }
                    return this;
                }
            }
        );
```

#### 9. ECMAScript5中的类
1. 定义不可枚举的属性

```
/**
             *定义不可枚举的属性
             **/
             //将代码包装至一个匿名函数中这样定义的变量就在这个函数作用域内
            (function() {
                    //定义一个不可枚举的属性objectId,它可以被所有对象继承，当读取这个属性时，调用getter函数
                    //它没有定义setter，因此它是只读的，而且它是不可配置的，因此它是不能删除的
                    Object.defineProperty(Object.prototype, "objectId", {
                        get: idGetter, //取值器
                        enumerable: false, //不可枚举
                        configurable: false //不可删除
                    });
                    //当读取objectId的时候直接调用getter函数
                    function idGetter() { //getter函数返回该id
                        if (!(idprop in this)){ //如果这个对象中不存在id
                                if (!Object.isExtensible(this)) //并且可以增加属性
                                    throw Error("can not define id for none extensible objects");
                                Object.defineProperty(this, idprop, {
                                    value: nextid++, //给它一个值
                                    writable: false, //只读的
                                    enumerable: false, //不可枚举的
                                    configurable: false //不可删除的
                                });
                            }
                            return this[idprop]; //返回已有活新的值
                        };
                        // idGetter()用到了这些变量，这些都属于私有变量
                        var idprop = "|**objectId**|"; //假设这个属性没有用到
                        var nextid = 1; //给它设定初始值
                    }()); //包装函数立即执行
```
2. 定义不可变类


```
/**
             *创建一个不可变的类，它的属性和方法都是只读的
             **/
             //这个方法可以使用new调用，也可以省略new，它可以用作构造函数也可以用作工厂函数。
            function Range2(from, to) {
                    //这些都是对from和to只读属性的描述符
                    var props = {
                        from: {
                            value: from,
                            enumerable: true,
                            writable: false,
                            configurable: false
                        },
                        to: {
                            value: to,
                            enumerable: true,
                            writable: false,
                            configurable: false
                        }
                    };
                    if (this instanceof Range2) //如果作为构造函数来调用
                        Object.defineProperties(this, props); //定义属性
                    else
                        return Object.create(Range2.prototype, //创建并返回这个新Range2对象
                            props); //属性由props指定
                }
                //如果用同样的方法给Range2.protptype对象添加属性，那么需要给这些属性设置他们的特性
                //因为我们无法识别出他们的可枚举性，可写性和可配置性，这些属性的特征默认false
                
                Object.defineProperties(Range2.prototype,{
                    includes:{
                        value:function(x){return this.from <= x && x <= this.to;}
                    },
                    foreach:{
                        value:function(f){
                            for(var x = Math.ceil(this.from); x <= this.to; x++)f(x);
                        }
                    },
                    toString:{
                        value:function(){return "(" + this.from + "..." + this.to + ")";}
                    }
                });
                
                var c = Range2(100,22); //
                console.log(c.toString()) //=> (100...22)
```

3. 封装对象状态


```
/**
             *封装对象状态
             **/
             //这个版本的Range类是可变的，但将端点变量进行了狂好的封装。但是端点大小顺序还是固定的：from <= to
            function Range(from, to){
                //from大于to
            if (from > to) throw new Error("from mustbe <= to");
             //定义存取器方法以维持不变
            function getFrom() {
                return from;
            }

            function getTo() {
                return to;
            }

            function setFrom(f){//设置from的值时，不允许from大于to
                if (f <= to) form = f;
                else throw new Error("from mustbe <= to");
            }
            
            function setTo(t){//设置to的值时，不允许to小于from
                if(t >= form) to = t;
                else throw new Error("to mustbe >= from");
            }
                         //将使用取值器的属性设置为可枚举并且不可配置之的。
            Object.defineProperties(this, {
                from: {
                    get: getFrom,
                    set: setFrom,
                    enumerable: ture,
                    configurable: false
                },
                to: {
                    get: getTo,
                    set: setTo,
                    enumerable: ture,
                    configurable: false
                }
            });
            }
            //和前面的例子相比，原型对象没有做任何修改
            //实例方法可以像读取普通的属性一样读取from和to
            Range.prototype = hideProps({
                constructor:Range,
                includes:function(x){return this.from <= x && x <= this.to;},
                foreach:function(f){for(var x = Math.ceil(this.from);x <= this.to; x++) f(x);},
                toString:function(){return "(" + this.from + "..." + this.to + ")";}
            });
```
4. 子类和ECMAScript5

>下面实现子类困难之处在于需要使用难看的属性描述符

```
/**
         * StringSet:利用ECMAScript5的特性定义子类
         **/
        function StringSet(){
            this.set = Object.create(null); //创建一个不可包含原型的对象
            this.n = 0;
            this.add.apply(this,arguments);
        }
        //注意，使用Object.create()可以继承父类的原型
        //而且可以定义单独调用的方法，因为我们我们制定属性的可写性、可枚举性和可配置性。
        //因此这些属性特性的默认值都是false ， 只读方法让这个类难于子类化(被继承)
        StringSet.prototype = Object.create(AbstractEnumerableSet.prototype,{
            constructor:{value:StringSet},
            contains:{value:function(x){return x in this.set;}},
            size:{value:function(x){return this.n;}},
            foreach:{value:function(f,c){Object.keys(this.set).forEach(f,c);}},
            add:{
                value:function(){
                    for(var i = 0; i< arguments.length; i++){
                        if(!(arguments<[i] in this.set)){
                            this.set[arguments[i]] = true;
                            this.n++;
                        }
                    }
                    return this;
                }
            },
            remove:{
                value:function(){
                    for(var i = 0; i < arguments.length; i++){
                        if (arguments[i] in this.set){
                            delete this.set[arguments[i]];
                            this.n--;
                        }
                    }
                    return this;
                }
            }
        });
```
5. 属性描述符

>来看看属性操作示例


```
/**
             * ECMAScript5属性操作
             * 给Object.prototype定义properties()方法，这个方法返回一个表示调用它的对象上的属性名列表的对象
             * （如果不带参数调用它，就表示该对象的所有属性）
             * 返回的对象定义了4个有用的方法：toString()、descriptors()、hide()和show()
             **/
            (function namespace() { //将所有逻辑闭包在一个私有函数作用域中
                //这个函数成为所有对象的方法
                function properties() {
                        var names; //属性名组成的数组
                        if (arguments.length == 0) //所有的自由属性
                            names = Object.getOwnPropertyNames(this);
                        else if (arguments.length == 1 && Array.isArray(arguments[0]))
                            names = Array.prototype.splice.call(arguments, 0);
                        //返回一个新的properties对象，用以表示属性名字
                        return new properties(this, names);
                    }
                    //将它设置为Object.prototype的新的不可枚举的属性
                    //这是从私有函数作用域导出的唯一一个值
                Object.defineProperty(Object.prototype, "properties", {
                    value: properties,
                    enumerable: false,
                    writable: true,
                    configurable: true
                });
                //这个构造函数是由上面的properties()函数所调用的
                //properties类表示一个对象的属性集合
                function Properties(o, names) {
                        this.o = o; //属性所属的对象
                        this.names = names; //属性的名字
                    }
                    //将代表这些属性的对象设置为不可枚举的
                Properties.prototype.hide = function() {
                    var o = this.o,
                        hidden = {
                            enumerable: false
                        };
                    this.names.forEach(function(n) {
                        if (o.hasOwnProperty(n))
                            Object.defineProperty(o, n, hidden);
                    });
                    return this;
                };
                //将这些属性设置为只读的和不可配置的
                Properties.prototype.freeze = function() {
                    var o = this.o,
                        frozen = {
                            writable: false,
                            configurable: false
                        };
                    this.names.forEach(function(n) {
                        if (o.hasOwnProperty(n))
                            Object.defineProperty(o, n, frozen);
                    });
                    return this;
                };
                
                //返回一个对象，这个对象是名字到属性描述符的映射表，用它来复制属性，联通属性特征一起赋值
                //Object.defineProperties(dest,src.properties().descriptors());
                Properties.prototype.descriptors = function(){
                    var o = this.o,desc ={};
                    this.names.forEach(function(n){
                        if(!o.hasOwnProperty(n)) return;
                        desc[n] = Object.getOwnPropertyDescriptor(o,n);
                    });
                    return desc;
                };
                
                //返回一个格式化良好的属性列表
                //列表中包含名字、值和属性特性，使用"permanent"表示不可配置，使用"readonly"表示不可写，使用"hidden"表示不可枚举
                //普通的可枚举，可写和可配置属性不包含特性列表
                Properties.prototype.toString = function(){
                    var o = this.o; //在下面嵌套的函数中使用
                    var lines = this.names.map(nameToString);
                    return "{\n" + lines.join(",\n") + "\n";
                    function nameToString(n){
                        var s = "",desc = Object.getOwnPropertyDescriptor(o,n);
                        if(!desc) return "nonexistent" + n + ":undefined";
                        if (!desc.configurable) s += "permanent";
                        if((desc.get && !desc.set) || !desc.writable) s += "redyonly";
                        if(!desc.enumerable) s += "hidden";
                        if(desc.get ||desc.set) s += "accessor" + n
                        else s += n + ":" +((typeof desc.value ==="function")?"function":desc.value);
                        return s;
                    }
                };
                //最后，将原型对象中的实例方法设置为不可枚举的
                //这里用到了刚定义的方法
                Properties.prototype.properties().hide();
            }());//执行匿名函数
```
#### 10.模块
1. 什么叫模块？
    - 解答：类不是唯一的模块化代码方式。一般来讲，模块是一个独立的javascript文件。模块文件可以包含一个类定义、一组相关的类、一个使用函数库或者是一些待执行的代码。只要以模块的形式编写代码。任何javascript代码段就可以当做一个模块
2. 模块化的目标？
    - 解答：模块化的目标是支持大规模程序的开发，处理分散源中代码的组装，并且能让代码正确的运行，哪怕包含了作者所部期望出现的模块代码，也可以正确执行代码。为了做到这一点，不同的模块必须避免修改全局执行执行上下文，因此后续模块应当在它们所期望的运行元素（或接近原始）上下文中执行（这里的“原始上下文”是指调用模块时所在的上下文，可能处在一个很深的闭包中，但这个模块的逻辑不应该影响到其他上下文特别是全局上下文。）。这实际上意味着模块应当尽可能少地定义全局标识。理想状况是，所有模块都不应当定义超过一个（全局标识）。
    
3. 如何实现模块化？
    - 初步：用对象做命名空间
    - 进一步：用函数作命名空间（一般常用匿名函数自执行）
    - 或者：借助第三方库（比如requireJS）

```
/**
         * 模块函数中的Set类
         **/
        //声明全局变量Set,使用一个函数的返回值给它赋值
        //函数结束时紧跟的一堆圆括号说明这个函数定义后立即执行
        //它的返回值将赋值给Set,而不是将这个函数赋值给Set
        //注意它是一个函数表达式，不是一条语句，因此函数"invocation"并没有创建全局变量
        var Set = (function invocation(){
            function Set(){//这个构造函数是局部变量
                this.values = {};//这个对象的属性用来保存这个集合
                this.n = 0; //集合中值的个数
                this.add.apply(this,arguments);//将所有的参数都添加至集合中
            }
            //给Set.prorotype定义实例方法
            //这里省略了详细代码
            Set.prototype.contains = function(value){
                //注意我们调用了v2s()而不是调用带有笨重前缀的set._v2s()
                return this.values.hasOwnProperty(v2s(value));
            };
            Set.prototype.size = function(){return this.n};
            Set.prototype.add =function(){/*...*/};
            Set.prototype.remove =function(){/*...*/};
            Set.prototype.foreach =function(f,context){/*...*/};
            
            //这里是上面方法调用到的一些辅助的函数和变量
            //它们不属于模块的共有API,但它们都隐藏在函数的作用域内
            //因此我们不必将它们定义为Set的属性或使用下划线做其前缀
            
            function v2s(val){/*...*/}
            function objectId(o){/*...*/}
            var nextId = 1;
            //这个模块的共有API是Set()构造函数
            //我们需要把这个函数从私有命名空间中导出来
            //以便在外部可以使用它，在这种全局下，我们通过返回这个构造函数来导出它
            //它变成第一行代码所芝的表达式的值
            return Set;
        }());
```
