1. 首先实现一个可以监控属性变化的observer函数。

   我们期待如下方式使用:

   ```javascript
    new Vue({
           el: 'app',
           data: {
               a: '1',
               b: {
                   c: '2'
               },
               test: '2333'
           }
       });
   ```

   我们按照上述使用方式先写一个Vue类

   ```javascript
   class Vue {
       constructor(obj) {
           this.data = obj.data;
           this.observer(this.data);
       }
       
       observer(obj) {
       	// ...
       }
   }
   ```

   当observer接收的参数是一个不为null的对象时，我们借助Object.defineProperty()的get、set方法将属性监控起来。

   ```javascript
   class Vue {
       constructor(obj) {
           this.data = obj.data;
           this.observer(this.data);
       }
   
       observer(obj) {
         if(typeof obj === 'object' && obj !== null) {
             for (let prop in obj) {
                 this.defineHandle(obj, prop, obj[prop]);
             }
         }
       }
       
       defineHandle(obj, prop, val) {
           Object.defineProperty(obj, prop, {
               get: function () {
                   return val
               },
               set: function (newVal) {
                   console.log('变化了');
               }
           });
       }
   }
   ```

   但这样显然不是我们想要的。运行后改变对象的属性可以发现属性c并没有被监控上，故这里可以建立两者之间的联系，通过递归深层监控一个对象所有的属性。

   我们对defineHandle稍加修改即可：

   ```javascript
   defineHandle(obj, prop, val) {
           this.observer(val);
           Object.defineProperty(obj, prop, {
               get: function () {
                   return val
               },
               set: function (newVal) {
                   console.log('变化了');
               }
           });
       }
   ```

   到这里为止，我们就实现了一个监控属性变化的observer函数。

2. 创建一个管理订阅者的类
   - 维护一个订阅者数组
   - 通知订阅者调用其update方法刷新视图

   ```javascript
   class Management {
       constructor() {
           this.subs = [];
       }
       
       add(sub) {
           this.subs.push(sub)
       }
       
       notify() {
           this.subs.forEach(sub => {
               sub.update();
           });
       }
   }
   ```

   这个类的作用就是管理和维护订阅者。只有两个简单的方法add、notify。add用来添加需要notify的订阅者到一个数组中，notify则用来调用各个订阅者的update方法。

3. 创建一个订阅者类
   - get方法：获取内存中最新的value
   - update方法：根据最新的value更改dom中的value

   ```javascript
   class Watcher {
       constructor(vm, node, name, nodeType) {
           Management.target = this;
           this.vm = vm;
           this.node = node;
           this.name = name;
           this.nodeType = nodeType;
           this.update();
       }
       
       update() {
           this.get();
           //  更新视图
           if (this.nodeType === 'text') {
               this.node.nodeValue = this.value;
           }
           if (this.nodeType === 'input') {
               this.node.value = this.value;
           }
           if(this.nodeType === 'element') {
               this.node.innerText = this.value;
           }
       }
       // 获取 data 中的属性值
       get () {
           this.value = this.vm.data[this.name]; // 触发相应属性的 get
       }
   }
   ```

4. 编译id=app的文档片段，完成后插入dom中

   - 将html中的v-bind和{{}}表达式与observer监控的属性做上关联。
   - 通过new Watcher 初始化页面（update() => get() => 刷新视图）。
   - 在defineHandle的get()方法中调用Management的add()方法添加订阅者到队列中。
   - 当有属性改变时，会依次触发set() => notify() => update() => get() => 刷新视图

5. 完整代码：

```javascript
class Vue {
    constructor(obj) {
        let id = obj.el;
        this.data = obj.data;
        this.observer(this.data);
        let dom = this.nodeToFragment(document.getElementById(id));
        //  编译完成后，将 dom 返回到 app 中
        document.getElementById(id).appendChild(dom);
    }

    //  对象的属性深度监控
    observer(obj) {
        if (typeof obj === 'object' && obj !== null) {
            for (let prop in obj) {
                this.defineHandle(obj, prop, obj[prop]);
            }
        }
    }

    defineHandle(obj, prop, val) {
        let mg = new Management();
        this.observer(val);
        Object.defineProperty(obj, prop, {
            get: function () {
                console.log('小心倍增');
                // 数组判断已有不添加
                const res = !!mg.subs.find(value => value === Management.target);
                !res && mg.add(Management.target);
                return val
            },
            set: function (newVal) {
                if (newVal === val) return;
                //  被触发后改变val 后续触发get获取val赋值给视图层节点值刷新视图
                val = newVal;
                console.log('变化了');
                mg.notify();
            }
        });
    }

    nodeToFragment(node) {
        //  创建一个新的空白的文档片段
        let flag = document.createDocumentFragment();
        while (node.firstChild) {
            this.compile(node.firstChild);
            flag.appendChild(node.firstChild); // 将子节点劫持到文档片段中
        }
        return flag;
    }

    compile(node) {
        //  如果是元素节点
        if (node.nodeType === 1) {
            let attr = [...node.attributes];
            if (node.nodeName === 'INPUT') {
                //  获取属性的集合
                attr.forEach(att => {
                    if (att.nodeName === 'v-model') {
                        //  获取 v-model 绑定的属性名
                        this.name = att.nodeValue;
                        node.addEventListener('input', e => {
                            //  给相应的 data 属性赋值，进而触发该属性的 set 方法
                            this.data[this.name] = e.target.value;
                        });
                    }
                });
                // 只用传两个参数
                new Watcher(this, node, this.name, 'input');
            } else {
                let reg = /\{\{(.*)\}\}/;
                if (reg.test(node.innerText)) {
                    let name = RegExp.$1; //  获取匹配到的字符串
                    name = name.trim();
                    new Watcher(this, node, name, 'element');
                } else {
                    attr.forEach(att => {
                        if (att.nodeName === 'v-model') {
                            //  获取 v-model 绑定的属性名
                            this.name = att.nodeValue;
                        }
                    });
                    new Watcher(this, node, this.name, 'element');
                }
            }
        }
        if (node.nodeType === 3) {
            let reg = /\{\{(.*)\}\}/;
            if (reg.test(node.nodeValue)) {
                let name = RegExp.$1; //  获取匹配到的字符串
                name = name.trim();
                new Watcher(this, node, name, 'text');
            }
        }
    }
}

//  管理订阅
class Management {
    constructor() {
        this.subs = [];
    }

    add(sub) {
        this.subs.push(sub)
    }

    notify() {
        this.subs.forEach(sub => {
            sub.update();
        });
    }
}

//  订阅者
class Watcher {
    constructor(vm, node, name, nodeType) {
        Management.target = this;
        this.vm = vm;
        this.node = node;
        this.name = name;
        this.nodeType = nodeType;
        this.update();
        //  防止this.subs数量意外增加 倍数调用update方法 造成内存溢出
        // Management.target = null;
    }

    update() {
        this.get();
        //  更新视图
        if (this.nodeType === 'text') {
            this.node.nodeValue = this.value;
        }
        if (this.nodeType === 'input') {
            this.node.value = this.value;
        }
        if (this.nodeType === 'element') {
            this.node.innerText = this.value;
        }
    }

    // 获取 data 中的属性值
    get() {
        this.value = this.vm.data[this.name]; // 触发相应属性的 get
    }
}
```

