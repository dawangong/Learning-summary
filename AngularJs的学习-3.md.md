1. $compile
    1. 作用：编译html字符串或dom
    2. 用法：
        1. 直接使用
        2. 指令中的使用
    3. 示例
    

```javascript
<!--直接使用-->
        angular.module('myApp', [])
            .controller('MyController', function ($scope, $compile) {
                let vm = this;
                vm.msg = 'hello';
                // 创建编译函数
                let compileFn = $compile('<p>{{vm.msg}}</p>');
                // 传入scope，将作用域(scope)和模版"链接"到一起，得到编译好的dom对象(已封装为jqlite对象)
                let $dom = compileFn($scope);
                // 添加到文档中
                angular.element(document.getElementsByTagName('body')[0]).append($dom);
			})
```

2. track by $index
    1. 缘由：ng-repeat不允许collection中存在两个相同Id的对象。因此，数组中是不允许存在两个相同的数字的。
    2. 解决：定义自己的track by表达式。
    3. 方案：track by $index
    
3. angular中的repeat嵌套

>示例如下：


```javascript
<body ng-app="apps" ng-controller="ctrl">
<ul ng-repeat="i in data">
    <li>{{i.title}}</li>
    <ul ng-repeat="j in i.contents">
        <li>{{j}}</li>
    </ul>
</ul>
    <script>
        angular.module('apps',[]).controller('ctrl',ctrl);
        ctrl.$inject = ['$scope'];
        function ctrl($scope) {
			$scope.data = [
				{
					'title': '标题一',
					'contents': ['1-1','1-2','……']
				},
				{
					'title': '标题二',
					'contents': ['2-1','2-2','2-3','……']
				}
            ]
		}
    </script>
</body>
```


