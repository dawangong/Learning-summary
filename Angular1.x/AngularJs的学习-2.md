#### 1. angular的依赖注入
1. 定义：依赖注入（Dependency Injection）是一种经典的设计模式，主要是用来处理组件如何获取依赖的问题。依赖注入可以简单的理解为：在一个容器中我们定义了很多个模块和组件化服务，当模块需要某些服务时，只需要跟容器说我需要这些服务，并且只需要提供服务的名称，容器就会自动提供这些服务的实例。调用服务的模块不需要考虑这些服务是怎么来的，这些服务会由容器通过依赖注入提供给对应的模块。
2. 注入声明方式:
    1. 推断式的注入声明
    2. 显示注入声明
    3. 行内注入声明
    

```javascript
//推断式的注入声明
var app = angular.module('myApp', []);
app.controller('myCtrl', function ($scope, $http) {
	   // do something
});
```
>代码一旦被压缩，参数名称就会被替换为简单的字符，AngularJS将会找不到这些函数依赖，从而导致注入失败。

```javascript
//显示注入声明
var app = angular.module('myApp', []);
app.controller('myCtrl', myCtrl);
myCtrl.$inject = ['$scope', '$http'];
function myCtrl(a, b) {
    // do something
}
```
>只需要为函数对象新增一个$inject属性，值为一个字符串数组，数组的每个元素代表依赖名称，注意数组元素必须和注入参数的顺序一个一个对应，在字符串的拼写时必须与定义的时候一致。使用这种方式参数相当于形参，名称并没有多大关系，因此代码压缩也不会影响使用。

```javascript
//行内注入声明
var app = angular.module('myApp', []);
 app.controller('myCtrl', ['$scope', '$http', function ($scope, $http) {
      // do something
 }]);
```
>这种方式是显示注入声明方式的一种更为简洁的表现方式。这种方式是显示注入声明方式的一种更为简洁的表现方式。（推荐）

3. 依赖注入的优点
    1. 各模块之间的解耦，每个部分专注于自己的功能，对象的注入通过容器来完成
    2. 避免全局对象的污染
    
#### 2. angular的内置服务

>服务是一个对外提供某个特定功能，如消息服务、文件压缩等的独立模块。在AngularJS中，服务是一个单例对象或者函数。具有以下的两个特点：

1. 服务是一个单例，即无论这个服务被注入到任何地方，对象始终只有一个实例。
2. 定义服务的方式也是通过function，但是与我们自己定义一个function然后在其他地方调用不同，因为服务是被定义在一个模块中，所以其使用的范围是可以被管理的，这一点体现了AngularJS非常强的避免全局变量污染意识。
3. 一些介绍
    - $rootScope：每个应用都仅有一个rootScope。其他的例如controller中的scope都是rootScope的后代scope。scope通过监听数据层的变化，实现了数据层和模型层的分离。注册在$rootScope上的值可以被子$scope覆盖。
    - $http：是AngularJS和远程服务器通过ajax请求进行通信的核心服务。$http的API是基于$q服务的，它返回的是一个promise。根据返回的状态码判断执行成功的回调还是失败的回调，当状态码为200到299时执行成功回调，不在这个范围内的都执行失败回调。
    - $location：用于解析地址栏URL的服务，可以监听和改变地址栏的URL。当改变地址栏或者点击前进和后退时可以与浏览器同步URL
        - absUrl( )：只读；返回带有所有的片段的url
        - host( )：只读；返回url中的主机路径
        - port( )：只读；返回当前路径的端口号
        - protocol( )：只读；返回当前url的协议
        - hash( )：读、写；当带有参数时，返回哈希碎片；当在带有参数的情况下，改变哈希碎片时，返回$location
        - path( )：读、写；当没有任何参数时，返回当前url的路径；当带有参数时，改变路径，并返回$location
        - search( )：读、写；当不带参数调用的时候，以对象形式返回当前url的搜索部分
        - replace( )：如果被调用，就会用改变后的URL直接替换浏览器中的历史记录，而不是在历史记录中新建一条信息，这样可以阻止『后退』

#### 3. angular的一些自定义服务
1. 定义服务的方式，常见的有以下三种：
    1. 使用Module的provider方法
    2. 使用Module的factory方法
    3. 使用Module的service方法
    
2. 注意点：
    1. provider
        - 通过provider方法创建的服务一定要包含$get方法，provider注入的结果就是$get方法返回的结果，如果不包含$get方法，则程序会报错。
        - 如果在provider中有返回值，只能返回this或者基本数据类型或者具有$get方法的对象类型
        - 在三种创建服务的方法中，只有使用provider方法创建的服务才可以传进config函数，以用于在对象启用之前，对模块进行配置。但是在config中进行配置的只能是在$get函数之外定义的变量
        - 注入config函数中时，参数名必须由服务名+Provider组成
    2. factory
        - 通过factory方法创建的服务必须有返回值，即必须有return函数，它可以返回任意类型的值，包括基本数据类型或者对象类型。如果没有return函数，则会报错。
        - factory注入的结果就是return返回的结果，可以在被注入的对象中使用注入的结果定义的各种方法
    3. service
        - 通过service方法创建的服务，可以不用返回任何值，因为service方法本身返回一个构造器，系统会用new关键字来创建一个对象，所以我们可以在service内部使用this关键字，对service进行扩展。
        - 如果使用具有返回值的写法，返回的值必须是一个对象，如果只返回基本类型，则实际返回的还是相当于this
    
3. 三种方法的比较
- 需要在config中进行全局配置的话，只能选择provider方法
- factory和service是使用比较频繁的创建服务的方法。他们之间的唯一区别是：service方法用于注入的结果通常是new出来的对象，factory方法注入的结果通常是一系列的functions
- provider是创建服务最为复杂的方法，除非你需要创建一个可以复用的代码段并且需要进行全局配置，才需要使用provider创建
- 所有具有特定性目的的对象都是通过factory方法去创建

4. 依赖注入的时机

>当在使用以上三种方法创建服务时，它们可能也需要依赖于别的服务，此时它们的依赖注入时机是有差别的。

>provider是在$get方法中进行依赖注入的，当在定义provider时依赖注入则会报错

```javascript
angular.module('providerModule', [])
       .provider('myProvider', function () {
        this.$get = ['$http', function ($http) {
            return {};
        }];
});
```

>factory和service的依赖注入发生在定义时

```javascript
angular.module('serviceModule', [])
     .service('myService', ['$http', function ($http) {
}]);
```

```javascript
angular.module('factoryModule', [])
      .factory('myFactory', ['$http', function ($http) {
         return {};
}]);
```

5. AngularJS官方文档也对这几种方法做了对比，结果如下表格所示：

特性 | Factory|	Service	|Provider
---|---|---|---
是否可以依赖注入|	是|	是|	是|
是否依赖注入友好|	否|	是|	否|
是否可在config中进行配置|	否|	否	|是
是否可以创建函数|	是|	是	|是
是否可以创建基本数据类型|	是|	否|	是

6. angular中provider们的详细分析可以参考[这篇](https://segmentfault.com/a/1190000003096933)或[这篇](http://hellobug.github.io/blog/angularjs-providers/)。