1. export module 的 name

   开发angular1.x + es6项目 的萌新可能经常会看到这样的写法：

   ```javascript
   export default angular.module("moduleA", [])
       .service("ServiceA", ServiceA)
       .service("ServiceB", ServiceB)
       .name;
   ```

   > 那么这里为什么要export module的name呢？

   **这是为了这个module的引用者方便，如果某个module改名了，所有依赖它的module可以不修改代码。**

2. 指令中的不常见配置项解读

   - priority：指令的优先级，默认为0, 常用指令优先级如下:

     - ngRepeat : 1000

     - ngSwitchWhen : 800
     - ngIf : 600
     - ngInclude : 400
     - ngView : 400

   - terminal：设置为true, 意味着元素上优先级小于当前指令的其他指令都不会执行, 也就是说执行到当前指令就结束了, 相同优先级的指令不包含在内.

   - templateNamespace：指定template的文档类型, 可选'html'、'svg'、'math', 默认为'html'.

   - require：为了给父子指令或者兄弟指令的Controller之间搭建一个桥梁. 被require的指令的Controller会作为当前指令link函数的第四个参数. 这样就可以调用外部Controller的方法. 它的值与link函数的参数有以下几种对应方式：

     - 字符串: 对应单个controller

     - 数组: 对应一个数组, 通过顺序获取controller

     - 对象: key随便取, value为需要require的指令, 对应一个对象, 通过key获取controller

     - 修饰符如下表：

       | 修饰前缀 |                         意义                         |
       | :------: | :--------------------------------------------------: |
       |    无    |                 在当前指令作用域查找                 |
       |    ^     |  在当前及父级作用域查找，如果没有找到会抛出一个错误  |
       |    ?     |   在当前作用域没有找到时将null作为link的第四个参数   |
       |    ^?    | 指定在当前作用域中查找，找不到时，不抛出严重的错误。 |
       |    ^^    |                 只会在父级节点查找.                  |

   - replace：设置成true, Angular会用模板的内容来替换当前元素, 但是这里有个坑需要注意, 我们必须保证模板内容只有一个根节点, 否则会抛出[Invalid Template Root Exception](https://link.jianshu.com/?t=https://docs.angularjs.org/error/%24compile/tplrt).

   - transclude：设置成true, 配合ngTransclude指令使用, 可以将指令包裹的子元素添加进模板进行编译, 但是这里又一个坑需要注意, 被包裹的子元只能访问指令外部的作用域 ( scope ) , 而不能访问指令自己的作用域.

   - bindToController：指令中通过scope:{}属性声明的变量仍然会被自动绑定到scope, 而不是控制器上, 通过设置bindToController为true, scope上的变量会自动绑定到控制器.

3. 指令中scope下的绑定

   - '@' 将独立作用域中的变量与DOM属性绑定，绑定结果总是一个字符串。

   - '<' 单向数据绑定。

   - '=' 双向数据绑定。

   - '&'绑定函数或执行表达式。

   - **写法上的一些差异。**

     写法1：

     ```javascript
     //scope属性
     {
       name: '@'
     }
     ```

     写法2：

     ```javascript
     //scope属性
     {
       name: '@hi',
     }
     //html
     <my-directive hi='John'>
     ```

     > 当绑定到scope上的属性名和html里面的属性名一致时，可以简写为写法1的形式

     写法3:

     ```javascript
     //scope属性
     {
     	isOpen: '=?',
     }
     ```

     **这种写法中的？和require中的修饰前缀？作用是类似的。用来指定属性是可选的，不会在绑定的属性是不可用的时候抛出[Non-Assignable Expression](https://link.jianshu.com/?t=https://docs.angularjs.org/error/%24compile/nonassign)**

     

      

      

      

