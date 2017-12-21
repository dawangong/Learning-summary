>异步事件驱动编程模型

事件类型只是一个字符串如：‘mouseover’，‘keydown’之类的，事件处理程序是处理或响应事件的程序。事件对象是与特定事件相关且包含有关该事件详细的对象。所有事件对象都有'type属性'和'target属性'比如：键盘事件的相关对象会包含按下的键和辅助键的详细信息，鼠标事件会包含鼠标指针的坐标。事件传播是浏览器决定那个对象触发器事件处理程序的过程。冒泡和捕获。取消事件事件处理程序可以通过返回一个适当的值，调用事件对象的某个方法或设置事件对象的某个属性来阻止默认操作的发生。

>事件分类：依赖于设备的输入事件，独立于设备的输入事件，用户界面事件，状态变化事件，特定API事件，计时器和错误处理程序。

#### 1. 事件类型
- 3级DOM事件规范，经过长期停滞之后，在w3c的主持下又开始换发生机。
- HTML5规范及相关衍生规范的大量新API定义了新事件，比如历史管理，拖放，跨文档通信，以及视频音频的播放。
- 基于触摸和支持javascript的移动设备的出现，它们需要重新定义新的触摸和手势事件。

##### 1-1. 传统事件类型
- 表单事件
    - <form>元素分别会触发submit事件和reset事件
    - 按钮交互：触发click事件
    - 输入文字，选择选项或者选择复选框触发change事件
    - 文本输入域：只有用户和表单元素完成交互并通过tab键或单击的方式移动焦点到其他元素上是会触发change事件。
    - 相应通过键盘改变焦点的表单元素再得到失去焦点的时候分别触发focus和blur事件不会冒泡（IE中用focusin和focusout事件代替冒泡）

- window事件
    - load事件
    - unload事件
    - resize事件（他的事件对象没有调整大小的详细信息属性）
    -scroll事件 （他的事件对象没有滚动的详细信息属性）
- 鼠标事件
    - 点击事件：鼠标事件在所对应的最深嵌套的元素上触发，但他们会冒泡直到文档的最顶层。传递给鼠标事件处理程序的事件对象有属性，==当事件发生时鼠标的位置和按键状态，当时是否有辅助键按下，clientX和clientY属性指定了鼠标在窗口坐标中的位置，button和which属性指定了按下的鼠标键是哪个，click事件的detail属性指定了是单机还是双击三击==
    - mousemove事件：用户移动或拖动鼠标时会触发。
    - mousedown和mouseup事件,在这两个事件队列之后，会自动触发click事件
    - dblclick事件：用户在相当短的时间内连续两次单击鼠标按键，跟在第二个click时间之后是dbclick事件。
    - contextmenu事件：单击鼠标右键会显示上下文菜单，取消这个事件可以取消菜单的显示，这个事件也是或的鼠标右击通知的简单方法。
    - mouseover和mouseleave事件：用户移动指针从而使他悬停到新元素上时和鼠标移动指针使他不再悬停在某个元素上时触发。（会冒泡）事件对象有relateTarget属性来指明这个过程中涉及到的其他元素。很不方便，因为要需要检查鼠标是否真的离开目标元素还是仅仅是从这个元素的一个子元素移动到另一个子元素。IE提供了这些事件的不冒泡版本，mouseenter和mouseleave事件。
    - mousewheel事件：传递的对象属性指定滚动转动的大小和方向
- 键盘事件
    - 传递的键盘事件处理程序的事件对象有keyCode字段，他指定按下和释放的键是哪一个。 键盘按下时altKey/ctrlKey/metaKey/shiftKey设置为true。
    - keydown和keyup是低级键盘事件，再两个事件之间或触发keypress事件。keypress是高级文本事件，其事件对象指定产生的字符而非按下的字符。

##### 1-2.  DOM事件

##### 1-3.  HTML5事件

>广泛推广的html5特性之一是加入了用于播放的<audio>和<video>元素。这些元素有长长的事件列表，它们触发各种关于网络事件、数据缓冲状态和播放状态的通知


cols1 | cols 2 | cols 3 | cols 4
---|--- |--- |---
canplay | loadeddata | playing | stalled
canplaythrought | loadedmetadata | progress | suspend
duartionchange | loadstart | ratechange | timeupdate
emptied | pause | seeked | volumechange
ended | play | seeking | waiting

>html5的拖放API允许javascript应用参与基于操作系统的拖放操作，实现web和原生应用间的数据传输，该API定义了如下七个事件类型

- dragstart
- drag
- dragend
- dragenter
- dragover
- dragleave
- drop

>html5标准还定义了大量其他事件来通知应用下载进度和应用缓存更新

cols1 | cols 2 | cols 3 | cols 4
---|--- |--- |---
cached | checking | downloading | error
noupdate | obsolete | progress | updateready

#### 2. 注册事件处理程序
##### 2-1. 设置JavaScript对象属性为事件处理程序


```javascript
window.onload=funciton(){
    //code
}
```javascript

##### 2-2. 设置HTML标签属性为事件处理程序

```javascript
<button onclick="alert('hello');"></button>
```javascript

cols1 | cols 2 | cols 3 | cols 4
---|--- |--- |---
onafterprint | onfocus | ononline | onresize
onbeforeprint | onhashchange | onpagehide | onstorage
onbeforeunload | onload | onpageshow | onundo
onblur | onoffline | onredo | 

>当指定一串JavaScript代码作为HTML事件处理程序属性时，浏览器会把代码串转换为类似如下的函数中：


```javascript
funciton(event){
    with(document){
        with(this.form || {}){
            with(this){
                code...
            }
        }
    }
}
```javascript

##### 2-3. addEventListener()

- 参数一：要注册处理程序的时间类型（不需要前面加on） 
- 参数二：当指定类型的事件发生时应该调用的函数。 
- 参数三：该参数是一个布尔值，一般情况下，会给这个参数传递false。如果true，那么函数注册为捕获事件处理程序。


```javascript
document.getElementById("id").addEventListener("click", handMouseMove,false);
```javascript


##### 2-4. removeEventListener()

>它同样有三个参数，从对象中删除事件处理程序函数而非添加，它常用于临时注册事件处理程序。


```javascript
document.getElementById("id").removeEventListener("click", handMouseMove,false);
```javascript

##### 2-5. attachEvent()

>如果IE不支持addEventListener()和removeEventListener()，那么就是用attachEvent()和detachEvent()。

>这两种操作的区别：


```javascript
//因为IE不支持事件捕获，所有这两个方法只有两个参数。
//这两个方法的第一个参数是用带“on”前缀的时间。
atttachEvent允许相同的事件处理程序注册多次。
var b = document.getElementById("myButton");
var handler = function(){code...};
if (b.addEventListener){
    b.addEventListener("click",handler,false);
    b.removeEventListner("click",handler,false);
}
else{
    b.attachEvent("onclick",handler);
    b.detachEvent("onclick",handler);
    }
```javascript

#### 3. 事件处理程序的调用

##### 3-1. 事件处理程序的参数

>通常调用事件处理程序时把事件对象作为它们的第一个参数。

>在IE中，当调用它们事件处理函数时并未传递事件对象。取而代之，通过全局对象window.event来获取事件对象。


```javascript
function(event){
    event = event || window.event;
}
```javascript

##### 3-2. 事件处理程序的运行环境

>当使用addEventListener()注册时，调用的处理程序使用事件目标作为他们的this值。但是，对于attachEvent()来讲这是不对的。


```javascript
function addEvent(target, type, handler){
    if (target.addEventListner)
        target.addEventListner(type,handler,false);
    else
        target.attachEvent("on"+type,function(event){
            handler.call(target,event);
        });
}
```javascript

##### 3-3. 事件处理程序的返回值

>通常情况下，返回值false就是告诉浏览器不要执行这个事件相关的默认操作。

使用addEventListener()或attachEvent()注册事件处理程序转而必须调用preventDefault()方法或设置事件对象的returnValue属性。

##### 3-4. 调用顺序

通过设置对象属性或HTML的处理程序优先调用
使用addEventListener()注册处理程序按照它们的注册顺序调用
使用attachEvent()注册的处理程序可能按照任何顺序调用

##### 3-5. 事件传播

大部分事件会“冒泡”到DOM树根。调用目标的父元素的事件处理程序，然后调用在目标的祖父元素上注册的事件处理程序。这会一直到Document对象，最后到达Window对象。

事件冒泡是事件传播的第三个“阶段”。目标对象本身的事件处理程序调用是第二个阶段。第一个阶段甚至发生在目标出现程序调用之前，称为“捕获”阶段。

##### 3-6. 事件取消

用属性注册的事件处理程序的返回值能用于取消事件的浏览器默认操作。在支持addEventListener()浏览器中，也能通过preventDefault()方法取消事件的默认操作。在IE9之前的IE中，可以通过设置事件对象的returnValue属性为false来达到同样的效果。

```javascript
function cancelHandler(event){
    var event = event || window.event;
    if (event.preventDefault)
        event.preventDefault();
    if (event.returnValue
        event.returnValue = false;
    return false;
}
```javascript

#### 4. 文档加载事件

>在支持addEventListener()的浏览器中，可以调用事件对象的stopProgation()方法以阻止事件的传播。

大部分Web应用都需要Web浏览器通知他们文档加载完毕和为操作准备就绪的时间。Window对象的load事件就是为了这个目的。load事件直到文档和所有图片加载完毕时才发生。然而，在文档完全解析之后但在所有图片全部加载完毕之前开始运行脚本通常是安全的，所以如果基于“load”发生之前的事件触发脚本会提升Web应用的启动时间。
当文档加载解析完毕且所有延迟（deferred）脚本都执行完毕时会触发DOMContentLoaded事件，此时图片和异步（async）脚本可以依旧在加载，但是文档已经为操作准备就绪了。Firefox引入了这个事件，然后塔被包括Microsoft的IE9在内的所有其他浏览器采用。尽管其名字中有“DOM”，并属于3级DOM事件标准的一部分，但HTML5标准化了它。

>下面定义了whenReady()函数。当文档为操作准备就绪时，传递给whenReady()的函数将会作为Document对象的方法调用。和之前的onLoad()函数不同，whenReady()监听DOMContentLoaded和readystatechange事件，而使用load事件仅仅是为了兼容那些不支持之前事件的较老的浏览器。


```javascript
/* 
 * 传递函数给whenReady()，当文档解析完毕时且为操作准备就绪时， 
 * 函数将作为文档对象的方法调用 
 * DOMContentLoaded、readystatechange或load事件发生时会触发注册函数 
 * 一旦文档准备就绪，所有函数都将被调用，任何传递给whenReady()的函数都将立即调用 
 */  
var whenReady = (function(){  
    var funcs = []; // 当获得事件时，要运行的函数  
    var ready = false; // 当触发事件处理程序时，切换到true  
  
    // 当文档准备就绪时，调用事件处理程序  
    function handler(e) {  
        // 如果已经运行过一次，只需要返回  
        if (ready) return;  
  
        // 如果发生readystatechange事件，  
        // 但其状态不是“complete”的话，那么文档尚未准备好  
        if (e.type == "readystatechange" && document.readystate !="complete")  
            return;  
  
        // 运行所有注册函数  
        // 注意每次都要计算fucs.length,  
        // 以防这些函数的调用会导致注册更多的函数  
        for (var i = 0; i < funcs.length; i++) {  
            funcs[i].call(document);  
        };  
  
        // 现在设置ready标识为true，并移除所有函数  
        ready = true;  
        funcs = null;  
  
    }  
  
    // 为接受到的任何事件注册处理程序  
    if (document.addEventListener) {  
        document.addEventListener("DOMContentLoaded", handler, false);  
        document.addEventListener("readystatechange", handler, false);  
        window.addEventListener("load", handler, false);  
    }  
    else if (document.attachEvent) {  
        document.attachEvent("onreadystatechange", handler);  
        window.attachEvent("onload", handler);  
    };  
  
    // 返回whenReady函数  
    return function whenReady(f) {  
        if (ready) f.call(document);  
        else funcs.push(f);  
    }  
}());  
```javascript
#### 5. 鼠标事件


类型 | 说明
---|---
click | 鼠标点击时触发
contextmenu | 可以取消的事件，当上下文即将出现时触发
dbclick | 鼠标双击时触发
mousedown | 鼠标按键按下时触发
mouseup | 鼠标按键释放时触发
mousemove | 鼠标移动时触发
mouseover | 鼠标进入元素时触发
mouseout | 鼠标离开元素时触发
mouseenter | 类似mouseover 但是不冒泡
mouseleave | 类似mouseout 但是不冒泡

#### 6. 鼠标滚轮事件
>除了火狐都支持mousewheel事件。但火狐用DOMMouseScroll代替

具体见javascript权威指南p465

#### 7. 拖放事件
>用于实现拖放的API总是很复杂：

- 它们必须和底层OS结合，使它们可以在不相关的应用间工作
- 它们必须适用于“移动”、“复制”和“链接”数据传输操作允许拖放源和拖放目标通过设置限制允许的操作，然后让用户选择许可设置
- 它们必须为拖放源提供一种方式指定待拖动的图标或图像
- 它们必须为拖放源和拖放目标的DnD交互过程提供基于事件的通知

#### 8. 文本事件
1. 浏览器有3个传统的键盘输入事件。keydown和keyup是低级事件。keypress是较高级事件，它表示产生了一个可打印字符。3级dom事件规范草案定义了一个更通用的textinput事件，不管来源，无论何时用户输入文本时都会触发它。webkit浏览器支持一个非常相似的textInput事件。
2. 可以通过取消textunput、textInput和keypress事件来组织字符输入，这意味着可以使用这些事件来过滤输入。

#### 9. 键盘事件
类似鼠标对象事件，键盘事件对象有altKey、ctrlKey和shiftKey属性，当事件触发时，如果对应的辅助键被按下，那么它们会被设置为true。
>当按下按键时，知道的只有keyCode，可以根据这个识别按下了那个键位。