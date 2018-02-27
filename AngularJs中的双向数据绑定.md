1.首先来了解$watch

- 作用：监听变量或者对象的变化，并在变化时提供操作空间。
- 语法：$watch(watchObj,watchFn,deepWatch)
- watchObj:监听对象（字符串形式）
- watchFn:回调函数（变化时的回调）
- deepWatch:深度监听（布尔值，默认false）
- 返回值：一个函数，用来注销对应的$watch
- 示例：

```javascript
    let app = angular.module('apps', []);
    app.controller('firstController', firstController);
    firstController.inject = ['$scope','$log'];

    function firstController($scope,$log) {
        $scope.name = '张三';
        $scope.count = 0;
        // 监听一个model 当model每次改变时 都会触发第2个函数
        let unbingWatch = $scope.$watch('name', function(newValue, oldValue) {
            // $log.log(oldValue);
            $scope.count ++;
            if($scope.count>5) {
            	// unbingWatch();
				$log.log('变化过五次了');
            }
        });
    }
```

2.双向数据绑定的背后

- 首先：AngularJS会在幕后会为你在scope模型上设置一个watcher。它用来在数据发生变化的时候更新view。这里的watcher和AngularJS中设置的$watch()是一样的。
- 其次：在$digest循环中，watchers会被触发（调用）。
- 具备上面两个基本概念后，请继续...
- Angular数据双向绑定更新的背后：AngularJS总是将我们的代码wrap到一个function中并传入$apply()，$apply会调用$rootScope.$digest()，一轮$digest循环在$rootScope开始，随后会访问到所有的children scope中的watchers。而watcher是用来检查数据是否变化的，$digest则会触发watcher并识别是否发生数据变化，如果发生变化，那么watcher对应的回调会被调用。
- 注意，$digest循环会持续运行直到model不再发生变化，或者$digest循环的次数达到了10次。
- tips： $digest循环最少也会运行两次，即使在listener函数中并没有改变任何model。它会多运行一次来确保models没有变化。
- 脏检查：$digest循环所做的事就是脏检查机制。

3.$watch和$apply的使用时机

- $watch：需要手动监听一个变量或对象，并需要根据变化做出一些操作时。
- $apply：angular上下文之外修改dom需要手动调用。
- 例子：

```javascript
angular.module('myApp',[]).controller('MessageController', function($scope) { 
$scope.getMessage = function() { 
setTimeout(function() { 
$scope.$apply(function() { 
//wrapped this within $apply 
$scope.message = 'Fetched after 3 seconds'; 
console.log('message:' + $scope.message); 
}); 
}, 2000); 
} 
$scope.getMessage(); 
});
```

