##### 背景:

> angular filter 常见于和ng-bind、差值表达式、ng-repeat 配合转换后端 unix 时间戳. 但 filter 不支持和 ng-model 一起使用.

##### 解决思路:

> 通过angular directive 结合 $filter服务封装一个支持转换 ng-model中 时间戳为指定格式的指令.

##### 代码如下:

```javascript
app.directive('dateFormat', dateFormat);

    app.$inject = ['$filter'];

    function dateFormat($filter) {
        return {
            restrict: 'A',
            require: 'ngModel',
            scope: {
                format: '@?' //这里和angular filter | date 写法一样
            },
            link: function (scope, elm, attrs, ctrl) {
                function formatter(value) {
                    if (!value) {
                        return '';
                    }
                    return $filter('date')(value, scope.format);
                }

                function parser() {
                    return ctrl.$modelValue;
                }

                ctrl.$formatters.push(formatter);
                ctrl.$parsers.unshift(parser);
            }
        }
    }
```

##### 使用:

```html
<input ng-model="model" date-format format="yyyy-MM-dd" placeholder="例如在input框中配合ng-model使用">
```

