CSS(层叠样式表)是一种指定HTML文档视觉的表现的标准。CSS本来是让视觉设计师来使用的：它允许设计师精确的对文档元素的字体 ，颜色，外边距，缩进，边框甚至是定位。不过，客户端javascript程序员对CSS感兴趣的是因为样式可以通过脚本编程。校本化css启用了一系列有趣的视觉效果。例如：可以创建动画让文档从右侧“滑入”；也能创建一个轮廓伸缩的列表。在利民用户自己控制显示的信息量。首次推出校本化的视觉效果是革命性的。创造这些效果的javascript和css技术在以前统称为动态HTML(DHTML).而现在，这个技术术语已经不流行了。

CSS是个复杂的标准。CSS本身就可以写一本书。为了理解CSS校本化，我们必须CSS的基础和最常用的样式属性。本节开头讲解CSS概述，接着解释了一些关键样式，它们是最适合校本化了的。第3节阐述了怎样实现CSS脚本化，本节介绍最常用和最重要的技术，利用HTML的style属性值，更改那行应用在单个文档元素的样式。元素的style属性可以用来设置样式，但是它不适合用来查询样式。第4节阐述如何查询元素的“计算样式”。第5节阐述如何通过修改元素的style属性来一次修改元素的多个样式。直接操作样式表也是可能的，但不常见。

#### 1.CSS概述

>HTML的视觉显示包含很多变量：字体，颜色、间距等。css标准列举了这些变量。我们成为样式属性。css定义了这些属性的字体，颜色，外边距，边框，背景图片，文本对齐方式，元素的尺寸和元素的位置。为了规定这些CSS属性，这些css是属性跟着冒号和值。例如：

- font-weight:bold
为了全面的描述一个元素的视觉效果，通常指定的不止一个属性。当需要多个名/值时，它们之间使用分号隔开;
- margin-left:1%; /* 左外边距是页面宽度的1% */
- text-indent:1px; /* 1像素的缩进 */
- font-size:12px; /* 字体尺寸为12px */

>两种方式将一组定义视觉表现的CSS属性和对于的HTML元素关联在一起。第一种是通过给每个单独的HTML元素设置style属性的方式，称为内联样式：
       
```javascript
 <p style="margin:20px;border:2px red solid;">
            samll letter
 </p>
```

尽管如此，通常将单独的HTML元素和CSS样式表分开，并把他们定义在一个样式表（stylesheet）中会更有用，样式表通过选择器将一组样式属性和使用选择器（selector）描述的一组HTML元素关联在一起。一个选择器基于ID，类名或标签或更多条件的指定（或“选择”）一个或多个文档中的元素。

CSS样式表的基本元素是样式规则，它们由选择器和包裹在一对{}中的css属性和值所组成。每个样式表可以包含任意数量的样式规则

##### 1-1. 层叠

>回想下，在CSS的“C”代表了“层叠”、该书序指定了应用文档中任何给指定元素的样式规则是各个“来源”的“层叠”效果：

web浏览器的样式表
文档的样式表
每个独立的HTML元素的style属性
当然，style属性的样式表覆盖了样式表中的样式，并且文档的样式表中的样式覆盖了浏览器的默认样式。为了显示元素，web浏览器“必须”组成元素的style属性。包括来自样式表索引匹配的选择器的样式表。计算结果是一组实际用于显示元素的样式属性和值。这组值就是元素的“计算样式”（computed style）。

##### 1-2. CSS历史

CSS历史是一个相对较老的标准，CSS1在1996年12月被采纳，它定义了具体的颜色，字体，外边距，边框和其它的旗本样式。类似Netscape4和IE4这样的老师浏览器支持css1.该标准的第二版css2在1998年被采纳，定义了很多高级特性，最著名的就是元素的绝对定位。css2.1澄清和更正了css2，并且它删除了浏览器供应商从未实现的功能。现在的浏览器基本上都完全支持css2.1,但是低于IE8的IE还有一些遗漏问题。

在css后续的工作中，征对版本3，CSS规范意见拆分成各种各样的专门化模块，分别来通过标准化进程。可以通过[它](http://www.w3.org/Style/CSS/current-work)找到css规范和工作草案。

##### 1-3. 复合属性

某些进程在一起使用的样式表属性可以组合起来使用一个页数的复合属性。例如font-family、font-size、font-weight属性可以用font的复合属性一次性设置：

font:blod italic 24px helvetica
另外还有border,margin和padding等复合属性，例如border-top，可以分别指定border-top-color,border-top-style,boder-top-width等属性。

##### 1-4. 非标准属性
当浏览器厂商实现非标准CSS属性时，他们将属性名钱加一个厂商前缀。Firefox使用-moz-，Chrome使用-wibkit-,而IE则使用-ms-，他们甚至用这种方式来显示将来会标准化的属性。有个例子是border-radius属性，他们指定元素的圆角。在firefox3和safari4实验中使用了前缀。一旦标准充分成熟。Firefox4和Safari5就取消和移除了前缀。直接使用border-radius.(chrome和opera已经支持没有前缀的border-radius很长的时间了，IE9也支持了没有前缀的border-radius.但在 IE8中使用前缀也没有支持。)
在不同的浏览器中不同名字的CSS属性一起工作，你可以能发现一个属性定义一个类的方式比较好

```javascript
.radius10{
border-radius:10px; /*征对现代浏览器*/
-moz-border-radius:10px; /*征对firefox 3.x*/
-webkit-border-radius:10px; /*征对safari 3.2和4*/
}
```

>前沿的CSS：目前，css正常进行一场变革，现代的浏览器厂商正在实现一些强大的新样式属性：border-radius、text-shadow、box-shadow、column-count。还有一个革命性的css新特征是web字体。利用css的@font-face规则可以下载并使用自己定义的字体。另外还有css动画过渡，css筛选器都值得关注。

#### 2. 重要的css属性

对于客户端程序员来说，最重要的css特性是那些指定文档中每个元素的可见性、尺寸和精确定位的属性。其它css属性允许指定堆叠的次序、透明度、裁剪区域、外边距、内边距、边框、颜色。为了脚本化css。理解这些样式属性的工作原理是非常重要的。下面的表做了总结。在本节一下内容中做详细的阐述。

>重要的css属性

属性|	描述
---|---
position|	指定元素的定位类型
top,left|	指定元素上，左边缘的位置
bottom，right|	指定元素的下，右边缘的位置
width，height|	元素的宽和高尺寸
z-index|	指定元素相对于其他重叠元素的“堆叠次序”，定义了元素定位的第三个维度
display	|指定元素是否以及如何显示
visibility	|指定元素是否可见
clip|	定义元素的“裁剪区域”，只显示在区域内的部分（唯一合法的形状值是：rect (top, right, bottom, left)）
overflow|	指定元素比分配空间要大的处理方式
margin、boder、padding|	指定元素的空白和边框
background|	指定背景图片或颜色
opacity	|指定元素的不透明度，它是CSS3属性，有些浏览器支持，ie中另有他法
##### 2-1. 用css定位元素

CSS的position指定了应用到元素上的定位类型，如下是4个可能出现的属性值
- static:默认属性.指定元素按照常规的文档内容流。静态定位不能使用top,left和类似其它的属性定位。如果想对该文档元素使用css定位技术，必须将position属性值设置为除此之外的其它3个属性值。

- absolute:该值指定元素是相对于包含的元素进行定位。相对于所有其它的元素，绝对定位的元素是独立定位的。它不静态定位的元素中文档流的一部分。它的定位要么是相对于最近定位祖先元素，要么是相对于文档本身。

- fixed:该值的定位元素是相对于浏览器窗口进行定位的。固定的定位的元素始终显示在哪儿。固定定位的元素和其它元素是独立的。不是文档流的一部分。除了ie6不支持外 ，其它现代的浏览器都支持它。

- relative:当position属性设置为relative，元素会按照常规的文档流进行布局，它的定位相对于文档流中的位置进行调整。系统保留这元素种草文档流中的空间。不会因为要填充空间将其各边合拢。也不会将新的元素从新的位置“推开”。

>一旦设置了元素的position属性为除了static以外的值，就可以通过元素的left,top,right,bottom属性的一些组合指定元素的位置。最常用的是left和top

##### 2-2. CSS盒模型和定位细节

>边框盒模型和box-sizing属性

>标准CSS盒模型规定width和height样式属性给定内容区域尺寸，而且不包含内边距和边框。可以称此为“内容盒模型”。

在老版的IE和新版的CSS都有一些例外，在IE6之前和当IE6-8在怪异模式下，显示一个页面（页面缺少<!DOCTYPE>或有一个不严格的doctype时），width和height属性缺少是包含内边距和边框宽度的。IE的行为是一个bug，但是IE的非标准和模型通常也很有用。认识到这一点，CSS3引进了box-sizing属性，默认值是content-box,它指定执行页面的标准盒模型，如果替换为box-sizing:border-box,浏览器将会为那个元素应用IE的盒模型，即：width和height包含边框和内边框。当想以百分比形式为元素设置总体尺寸，又想以像素指定单位边框和内边距时，边框盒模型特别有用：

      
```javascript
  <div style="box-sizing:border-box;width: 50%;padding: 10px;border: 2px solid red;"></div>
```

box-sizing属性在当今的浏览器中都支持，但是还没通用实现。比如为兼容标准未成熟的box-sizing属性，可以在chrome和safari中使用-webikit-box-sizing，在firefox中，使用-moz-box-sizing。在IE后等其他浏览器更高的版本中，可以使用不带前缀的box-sizing。


```javascript
<div style="width: calc(50%-12px);padding:10px;border: solid red 2px;"></div><!--请注意表达式方式-->
```

>在IE9中支持使用calc()计算css的值。在Firefox4中为-moz-calc()。

##### 2-3. 元素的显示和可见性

两个CSS的属性影响了文档元素的可见性：visibility和display。visibility属性很简单。当其值设置为hidden时，该元素不显示。当其值设置为visible时，该元素显示。display属性更加通用。它用来接收它的容器指定元素显示的类型。它指定元素是块级元素、内联元素、列表项等。但当display设置为none，受影响的元素将不显示，甚至根本没有布局。

visibility和display属性之间的差别可以从他们对使用静态或相当定位元素的影响中看到。对于一个常规布局流中的元素，设置visibility属性为hidden使得元素不可见，但在文档布局中保留了它的空间。类似可以充实的隐藏和显示而不改变文档布局。但是，当display属性设置为none，在文档布局中不给它分配位置。使得各边元素会靠拢，就当不存在。例如在创建和展开折叠的效果时display属性就很有用。

visibility和display属性对绝对和固定定位的元素影响是等价的。因为这些元素都不是文档布局的一部分。然而，在隐藏和显示定位元素时一般首选visibility属性。

##### 2-4. 颜色、透明度和半透明度

>CSS3也为RGBA色彩空间（红、绿、蓝色加上指定颜色透明度的alpha值）中定义了颜色语法。所有的现代浏览器（除了IE）都支持RGBA,在IE9中也能支持。css3也定义了对HSL（色相-饱和度-值）和HSLA颜色规范的支持。他们在FIrefox、Safari、Chrome中都支持，除了IE。

>CSS允许指定元素的确切位置，尺寸，背景颜色和边框颜色。因为能绘制矩形和（减少高度和宽度时）水平、垂直线条它有了基本的图形能力。但本书中<canvas>元素扩展将成为校本化图形内容。

>关于背景颜色，如果没有元素指定背景颜色或图象，它的背景通常透明，理解这点非常重要。默认情况下不是所有元素都是透明的，例如元素<button>有默认的背景颜色。用background-color属性可以覆盖默认颜色，如果强烈要求可以将其设置为"transpanrent"。

>CSS3的opacity属性处理元素的透明，该属性值为0-1之间的数字、opacity属性在当今所有的浏览器都支持。除了IE，IE提供可选方式filter。例如让元素设置为75%不透明，可以使用以下代码：

            
```javascript
opacity:0.75
filter:alpha(opacity=75);
```

##### 2-5. 部分可见：overflow和clip

>visibility属性可以让文档元素完全隐藏，而overflow和clip属性允许只显示元素的一部分。overflow属性指定内容超出元素的大小（例如：用width和 height样式属性指定）时如何显示。该属性的值和含义如下所示：

- visible :默认值。如果需要，内容可以溢出并绘制在元素边框的外面

- hidden:裁剪掉隐藏溢出的部分元素。

- scroll:元素一直显示水平和垂直滚动条。

- auto:滚动条只在内容超出元素的尺寸时显示，而非一直显示。

- clip:属性的值指定了元素的裁剪区域，在css2中，裁剪区域是矩形的，不过clip属性的语法预留了开放的可能性，该标准在将来的版本可能将支持更多形状的裁剪。它的语法是

>rect(top right bottom left)使用例子

    
```javascript
style="clip:rect(0px 100px 100px 0);"
style = "clip:rect(auto 100px auto auto);"
```

#### 3. 脚本化内联样式

脚本化css最直接了当的方法就是更改单独的文档元素的style属性，但是大多数HTML属性，style也是元素对象的属性。它可以在javascript操作，但是style属性不同寻常：它的值不是字符串，而是一个CSSStyleDeclaration对象。让style对象的javascript属性代表了HTML代码中通过的指定的css属性。例如让元素e的文本变大号、加粗和蓝色，可以使用如下代码设置font-size,font-weight和color样式属性对于的javascript属性。

```javascript
 var e = document.getElementById("bb");
 e.style.fontSize = "24px";
 e.style.fontWeight = "bold";
 e.style.color = "#007F9F";
 //<div id="bb">校本化内联样式</div>
 //<div id="bb" style="font-size: 24px; font-weight: bold; color: rgb(0, 127, 159);">校本化内联样式</div>
```

>使用CSSStyleDeclaration对象的style属性时，记住所有值都应该是字符串。在样式表（HTML）style属性中，可以如下书写


```javascript
position:absolute;font-family: sans-serif;background-color:#FFFFFF;
```


>在javascript为元素e完成同样的事情，需要将值放在引号中

```javascript
e.style.position = "absolute";
e.style.fontFamily = "sans-serif";
e.style.backgroundColor = "#FFFFFF";
```

>而且，javascript设置样式属性需要包含单位，因此，设置left属性应该像下面：

```javascript
e.style.left = "300px";
```

>如果需要计算值来设置left属性，需要保证在后面加上单位：

```javascript
e.style.left = (x0 + left_margin + left_border + left_padding) + "px";
```

>回想一下,一些css属性（如margin）是margin-top/margin-right/margin-bottom/margin-left)的复合属性。CSSStyleDeclaration对象也有与之对于的复合属性，例如。也能设置设置magin属性

```javascript
 e.style.margin = topMargin + "px" + rightMargin + "px" + bootomMargin + "px" + leftMargin + "px";
```
               
>独立设置4个margin属性值更加便捷：

```javascript
e.style.marginTop = topMargin + "px";
e.style.marginRight = rightMargin + "px";
...
```

                
HTML元素的style属性是它的内联样式，它覆盖在样式表中的任何样式什么。内联样式一般在设置样式值时非常有用，就像上面所说的一样。CSSStyleDeclaration对象的属性可以理解为代表内联样式，但是它的返回有意义的值：javascript代码已经设置过值或者HTML元素显式的设置了想要的内联样式的值。

读取元素的内联样式特别困难，对style属性来说必须包含单位，对复合属性来说，在真正使用这些值的时候，代码不得不包含非同寻常的css解析能力。总之，元素的呢哦连样式只有在设置样式的时候有用，但如果需要查询元素的样式，就要使用计算式，这将在本章4节讨论。

>有时，发现单个字符串值来设置或查询元素的内联样式反比作为CSSStyleDeclaration对象更加简单。为此，可以使用元素的getAttribute()和setAttribute()方法或CSSStyleDeclaration对象的cssText属性来实现


```javascript
  //两者都可以设置e的样式属性为字符串s
  e.setAttribute("style", s);
  s = e.style.cssText;
  //两者都可以查询元素的内联样式
  s = e.getAttribute("style");
  s = e.style.cssText;
```
           
>CSS动画

脚本化的css最常见的用途之一就是产生视觉动画，使用setTimeout()或setTinterval()(12章1节)，重复调用修改的元素的内联样式达到目的。下面的例子用shake()和fadeOut()来举例说明。shake()将元素从一边快速移动到令一边震动。例如当输入无效数据时，会吸引用户注意力。fadeOut()通过制定时间（默认500毫秒）降低元素不透明度，使得元素淡出和消失。
```javascript
             //将e转化为相对定位的元素，使之左右“震动”
             //第一个参数可以是圆度对象或者元素的id
             //如果第二个参数是函数，以e为参数，将在动画结束时调用
             //第四个参数指定震动多久，默认500毫秒
            function shake(e, oncomplete, distance, time) {
                    //句柄参数
                    if (typeof e === "string") e = document.getElementById(e);
                    if (!time) time = 500;
                    if (!distance) distance = 5;
                    
                    var originalStyle = e.style.cssText; //保存e的原始style
                    e.style.position = "relative"; //使e相对定位
                    var start = (new Date()).getTime(); //注意，动画的开始时间
                    animate(); //动画开始
                    //函数检查消耗时间，并更新e的位置
                    //如果动画完成，它将e还原为原始状态
                    //否则，更新e的位置，安排它自身从新运行
                    function animate() {
                        var now = (new Date()).getTime(); //得到当前时间
                        var elapsed = now - start; //从开始以来消耗了多长时间
                        //是总时间的几分之几
                        var fraction = elapsed / time;
                        if (fraction < 1) { //如果动画未完成
                            //作为动画完成的比例函数，计算e的x位置
                            //使用正弦函数将完成的比例乘以4pi
                            //所以，它来回往复两次
                            var x = distance * Math.sin(fraction * 4 * Math.PI);
                            e.style.left = x + "px";
                            //在25毫秒之后或在总时间最后尝试再次运行函数
                            //目的是为了产生每秒40帧的动画
                            setTimeout(animate, Math.min(25, time - elapsed));
                        } else { //否则动画完成
                            e.style.cssText = originalStyle //恢复原始样式
                            if (oncomplete) oncomplete(e); //调用完成后回调函数
                        }
                    }
                }
                //以毫秒级时间将e从完全不透明到透明
                //在调用函数时假设e是完全不透明的
                //oncomplate是一个可选函数，以e为参数，在动画结束调用
                //如果不指定time.默认500
                //本函数ie中不能正常构造
                //除了opacity，ie使用非标准的filter属性
                function fadeOut(e,oncomplete,time){
                    if(typeof e === "string") e = document.getElementById(e);
                    if(!time) time =500;
                    
                    //使用Math.sqrt作为一个简单的缓动函数来创建动画
                    //精巧的非线性：一开始淡的比较快，然后慢一些
                    var ease = Math.sqrt;
                    
                    var start = (new Date()).getTime(); //注意动画开始的实际
                    animate();//动画开始
                    
                    function animate(){
                        var elapsed = (new Date()).getTime() - start ;//消耗时间
                         //总时间的几分之几
                        var fraction = elapsed/time;
                        if(fraction < 1){//动画未完成
                            var opacity = 1 - ease(fraction);//计算元素不透明
                            e.style.opacity =String(opacity); //设置在e上
                            setTimeout(animate,Math.min(25,time-elapsed));
                        }
                        else{
                            e.style.opacity = "0";
                            if(oncomplete) oncomplete(e); //调用完成后回调函数
                        }
                    }
                }
```

>shake()和fadeOut()都能接受可选的回调函数做为第二个参数，如果指定了，当动画结束时将被调用。该动画元素将作为回调函数的参数传递进去。下面的代码创建了一个按钮，单击时，作用震动并弹出。

```javascript
 <button onclick="shake(this,fadeOut)">点击我</button>
```

注意，shake()和fadeOut()示例函数之间非常相似，都能作为类似css属性动画的模板。客户端库，如jQury通常支持预定义的视觉效果，因此，除非创建特别复杂的视觉效果，实际上不用写类似shake()动画函数。scriptaculous是早期一个值得关注的类库，它是为prototype框架设计的http://scripty2.com/

 >为了避免使用任何脚本，CSS3的过渡函数模块定义了再样式表中指定动画效果的方式。例如，替代了类似fadeOut()这样的函数，可以使用如下的css:

```javascript
.fadeable{transition:opacity 5s ease-in}
```
    
#### 4. 脚本化CSS类

>通过内联style属性校本化CSS样式的一个可选方案是校本化HTML的clss属性值。改变了元素的class就改变了应用与元素的一组样式表选择器，它能在同一时刻改变多个CSS属性。

>例如，假设想让用户对文档中的单独段落（或其它元素）引起注意。首先，为任意元素定义一个名为"attention"的类

```javascript
.attention{/*吸引用户注意*/
            background-color:yellow;
            font-weight: bold;
            border: solid black 2px;
            }
```
            
>标识符class在javascript中是保留字，所以HTML属性class在javascript代码中可以用于十月calssName的javascript代码。如下的代码设置和清除元素的className属性来为元素添加和移除"attention"类：

```javascript
 function grabAttention(e){e.className = "attention";}
 function releaseAttention(e) {e.className = "";}
```

HTML元素可以有多个CSS类名，class属性保存了一个用空格隔开的类名列表。className属性是一个容易误解的名字：classNames可能更好。上面的函数假设className属性只指定零个或一个类名，如果有多个类名就无法工作了。如果元素已经有一个类，调用grabAttention将覆盖已经存在的类。

HTML5为了解决这个问题，为每个元素定义了classList属性。该属性的值是DOMTokenList对象：一个制度的类数组对象，它保安韩元素的单独类名。但是，和数组元素相比，DOMTokenList定义的方法更加重要。add()和remove()从元素的class属性中添加和清除一个类名。toggle()表示如果不存在的类名就添加一个；否则，删除它。最后，contains()方法检测class属性中是否包含一个指定的类名。

类似DOM集合类型，DOMTokenList对象“实时的”代表了类名集合。而非是在查询classList属性时类名的一个静态快照。如果从元素的classList属性中获得了一个DOMTokenList对象，然后元素的calssName属性改变了，这些变化在标识列表中及时可见。统一，改变标识列表，在ClassName属性中及时可见。

>不是所有的浏览器都支持classList属性。但是这个重要的功能容易近似实现。如下代码或使用类似的代码，把class属性当做一个类名的集合。是的需要校本化的css类工作更加简单。

 
```javascript
             /***classList()：将className当做一个CSS类集合***/
            /**
             *如果e有classList属性则返回它。否则，模拟一个为e模型DOMTokenList API对象
             * 返回的对象有contains(),add(),remove(),toggle()和toString()等方法
             * 来检测和修改元素e的类集合，如果classList属性是原生支持的
             * 返回的类数组对象有length和数组索引属性。模拟的DOMTOkenList不是类数组对象
             * 但是它有一个toArray()方法来返回一个含元素类名的一个纯数组快照
             **/
            function classList(e) {
                    if (e.classList) return e.classList; //如果e.classList存在，则返回它
                    else return new CSSClassList(e); //否则就伪造一个
                }
            
            //CSSSlassList是一个模拟DOMTokenList的javascript类
            function CSSClassList(e) {this.e = e;}
            
            //如果e.className包含类名c，则返回true,否则返回false
            CSSClassList.prototype.contains = function(c) {
                //检测c是否为合法的类名
                if (c.length === 0  c.indexOf(" ") != -1)
                    throw new Error("Invalid calss name:'" + c + "'");
                //首先是常规检查
                var classes = this.e.className;
                if (!classes) return false; //不含类名
                if (classes === c) return true; //e有一个完全匹配的类名
                //否则，把c自身看做一个单词，利用正则表达式搜索c
                // \b在正则表达式里代表单词的边界
                return classes.search("\\b" + c + "\\b") != -1;
            };
             //如果c不存在，将c添加到e.className中
            CSSClassList.prototype.add = function(c) {
                if (this.contains(c)) return; //如果存在，什么都不做
                var classes = this.e.className;
                if (classes && classes[classes.length - 1] != " ")
                    c = " " + c; //如果需要，添加一个空格
                this.e.className += c; //将c添加到className中
            };
             //将在e.className中出现的c都删除
            CSSClassList.prototype.remove = function(c) {
                //检查c是否是合法的类名
                if (c.length === 0  c.indexOf(" ") != -1)
                    throw new Error("Invalid class name:" + c + "'");
                //将所有作为单词的c和多余的尾随空格全部删除
                var pattern = new RegExp("\\b" + c + "\\b\\s*", "g");
                this.e.className = this.e.className.replace(pattern, "");
            };
             //如果c不存在，将c添加到e.className中，并返回true
             //否则，将在e.className中出现所有的c都删除，并返回false
            CSSClassList.prototype.toggle = function(c) {
                if (this.contains(c)) { //如果e.className包含c
                    this.remove(c); //删除它
                    return false;
                } else {
                    this.add(c); //添加它
                    return true;
                }
            };
             //返回 e.className本身
            CSSClassList.prototype.toString = function() {
                return this.e.className;
            };
             //返回在e.className中的类名
            CSSClassList.prototype.toArray = function() {
                return this.e.className.match(/\b\w+\b/g)  [];
            };
```

#### 5. 校本化样式表

>到目前为止，我们已经看到如何设置和查询CSS样式和单个元素的类名。校本化样式表当然是也是可能的。虽然不经常这么做，但偶尔缺非常有用。本节概述改技术。

在脚本话样式表时，将会碰到两类需要使用的对象。第一类是元素对象，由<style>和<link>元素表示，两种元素包含或引用样式表。这些是常规的文档元素，如果他们又id属性值，可以使用document.getElementById()函数来选择它们。第二类是CSSStyleSheet对象，它表示样式表本身。document.styleSheets属性是一个只读的类数组对象，它包含CSSStyleSheet对象，表示与文档关联在一起的样式表。如果为定义或引用了样式表的<style>或<link>元素设置title属性值，该title作为对应CSSStyleSheet对象的title属性就可以。

>以下几节阐述了利用这些样式、链接元素和样式表对象可以做什么。

##### 5-1. 开启和关闭样式表

最简单的校本化样式表的技术特是最便捷和健壮的。<style>、<link>元素和CSSStyleSheet对象都定义了一个在javascript中可以设置和查询的disabled属性。顾名思义，如果disabled属性为true，样式表就被浏览器关闭并忽略。

>以下disableStyleSheet()函数就说明了这一点。如果传递一个数字 。函数将其当做document.styleSheet数组中的一个索引，如果传递一个字符串。函数就将其当做CSS选择器并传递给document.querySeleCtorAll()，然后设置所有返回元素的disabled属性：

```javascript
            function disableStyleSheeet(ss) {
                if (typeof ss === "number")
                    document.styleSheets[ss].disabled = true;
                else {
                    var sheet = document.querySelectorAll(ss);
                    for (var i = 0; i < sheet.length; i++)
                        sheet[i].disabled = true;
                }
            }
```

##### 5-2. 查询、插入与删除样式表规则

>除了样式表的开启和关闭以外，CSSStyleSheet对象也定义了用来查询、插入和删除样式表的规则API。IE8及更早版本实现的API和其它浏览器实现的标准API之间有一些轻微的区别。

直接操作样式表通常没什么意义。典型地，相对编辑样式表或增加新规则而言，让样式表保存静态并对元素className属性编程更好。另一方面，如果允许用户完全控制页面上的样式，了能需要动态操作样式表。

>document.styleSheets[]数组的元素是CSSStyleSheet对象。CSSStyleSheet对象有一个cssRules[]数组，它包含所有样式表规则：

```javascript
var firstRule = document.styleSheets[0].cssRules[0];
```

            
>IE使用不同的属性名rules代替cssRules。

cssRules[]或rules[]数组元素为CSSRule对象。在标准的API中，CSSRule对象代表所有的CSS规则，包含如@import和@page等指令。但是在IE中，rules[]数组只包含样式表中实际存在的样式规则。

CSSRule对象有两个属性可以便捷的使用。（在标准API中，非样式规则没有定义这些属性，当遍历样式表时希望跳过去它。）selectText是规则的CSS选择器，它引用一个描述与选择器相关联的样式的可写CSSStyleDeclaration对象。回想一个，CSSStyleDeclaration是用来表示内联和计算样式的相同类型。可以利用它来查询规则的样式值或设置新样式。通常，当遍历样式表时。你对规则的文本比它解析后的表示形式更感兴趣。此时，使用CSSStyleDeclaration对象的cssText属性来获得规则的文本表示形式。

>除了查询和修改样式表中已存在的规则以外，也能向样式表添加和从中删除规则。标准的API接口定义了insertRule()和deleteRule()方法来添加和删除规则。

```javascript
 document.styleSheets[0].insertRule("H1 {text-weight:bold}",0);
```

IE不支持insertRule()和deleteRule()，但定义了大致等效的函数addRule()和removeRule()。（除了名字以外）仅有的不同是addRule()希望选择器文本和样式文本作为两个参数。

>以下代码遍历样式表样式表的规则，举例说明了用API对样式表进行一些可以的修改：

```javascript
            var ss = document.styleSheets[0]; //得到一个样式表
            var rules = ss.cssRules?cssRules:ss.rules; //得到样式表规则
            
            for(var i = 0; i< rules.length; i++){ //遍历这些规则
                var rule = rule[i]; 
                if(!rule.selectorText) continue; // 跳过@import和费样式规则
                
                var selector = rule.selectorText; //选择器
                var ruleText = rule.style.style.cssText; //文本形式的样式
                
                //如果规则应用在h1元素上，也将其应用到h2元素上
                //注意：精当选择器在字面上为"h1"时这才起作用
                
                if(selector == "h1"){
                    if(ss.insertRule) ss.insertRule("h2 {"+ ruleText +"}" , rules.length);
                    else if(ss.addRule) ss.addRule("h2",ruleText,rules.length);
                }
                
                //如果规则设置了text-decoration属性，则将其删除
                if(rule.style.textDecoration){
                    if(ss.deleteRule) ss.deleteRule(i);
                    else if(ss.removeRule) ss.removeRule(i);
                    i--;//调整循环索引，因为以上的规则i+1现在即为规则i
                }
            }
```
            
##### 5-3. 创建新的样式表

最后，创建整个新样式表并将其添加到文档是中可能的。在大多数浏览器中，可以用标准的DOM技术:只要创建一个新的<style>元素，将其插入到文档的头部,然后用其innerHTML属性来设置样式表内容。但是在IE8以及更早的版本中，CSSStyleSheet对象通过非标准方法document.createStyleSheet()来创建，其样式文本用cssText属性值来指定。请看下面的例子。

```javascript
             /**创建一个新的样式表**/
             //对文档添加一个样式表，用指定的样式填充它
             //style参数可能是字符组成或对象。如果它是字符串，就将它作为样式表的文本。
             //如果它是对象，将每个定义样式规则的每个属性加到样式表中
             //属性名即为选择器，器值即为对应的样式
            function addStyles(styles) {
                //首先，创建一个新的样式表
                var styleElt, styleSheet;
                if (document.createStyleSheet) { //如果定义了IE的API,即可使用它
                    styleSheet = document.createStyleSheet();
                } 
                else {
                    var head = document.getElementsByTagName("head")[0];
                    styleElt = document.createElement("style"); //新的style元素
                    head.appendChild(styleElt);
                    //现在新的样式表应该是最后一个
                    styleSheet = document.styleSheets[document.styleSheets.length - 1]
                }
                //现在向其插入样式
                if (typeof styles === "string") {
                    //参数是样式表文本
                    if (styleElt) styleElt.innerHTML = styles;
                    else styleSheet.cssText = styles; //IE API
                } else{
                    //参数是待插入的单独的规则的对象
                    var i = 0;
                    for (selector in styles) {
                        if (styleSheet.insertRule) {
                            var rule = selector + "{" + styles[selector] + "}";
                            styleSheet.insertRule(rule, i++);
                        } else {
                            styleSheet.addRule(selector, style[selector], i++);
                        }
                    }
                }
            }
```            
