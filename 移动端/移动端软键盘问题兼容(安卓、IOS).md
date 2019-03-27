> 解决软键盘顶起fixed元素 (IOS下fixed元素会变成absolute)

```javascript
// angular.js中 通过封装指令解决 主要思路是通过scrollHeight的前后差值 判断是否弹出软键盘 然后显示或隐藏被顶起的元素即可

// 指令配置如下:

{
        restrict: 'A',
        link: function (scope, element) {

            var h = document.body.scrollHeight;
            window.onresize = function () {

                if (document.body.scrollHeight < h) {
                    element[0].style.opacity = 0;
                    h = document.body.scrollHeight;
                }else{
                    element[0].style.opacity = 1;
                    h = document.body.scrollHeight;
                }
            }
        }
    }
```

