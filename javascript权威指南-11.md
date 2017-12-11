#### 1. DOM概述
文档对象模型(DOM)是表示和操作HTML和XML文档内容的基础API。HTML文档的树状结构包含表示HTML标签或元素（如<body>、<p>）和表示文本字符串的节点，它也可以包含表示HTML注释的节点。

```
<html>
         <head>
                   <title>SampleDocument</title>
         </head>
         <body>
                   <h1>AnHTML Document</h1>
                   <p>Thisis a <i>simple</i> document.</p>
         </body>
</html>
```
#### 2. 选取文档元素

- 用指定的id属性
- 用指定的name属性
- 用指定的标签名字
- 用指定的css类
- 匹配指定的css选择器

##### 2-1. 通过ID选取元素

>任何HTML元素可以有一个id属性，在文档中该值必须唯一，即同一个文档中的两个元素不能有相同的ID。可以用Document对象的getElementById()方法选取一个基于唯一ID的元素。


```
var section1 = document.getElementById(“section1”);
```


##### 2-2. 通过名字选取元素

>基于name属性的值选取HTML元素，可以使用Document对象的getElementsByName()方法。

```
var rabiobuttons =document.getElementsByName(“favorite_color”);
```

>它返回一个NodeList对象，后者的行为类似一个包含若干Element对象的只读数组。
有些元素可以作为Document属性仅通过名字来选取：（最好不用）


```
//针对<formname=”shipping_address”>元素，得到Element对象
Var form = document.shipping_address；
```

##### 2-3. 通过标签名选取元素

>Document对象的getElementsByTagName()方法可用来选取指定类型（标签名）的所有HTML或XMl元素，返回一个NodeList对象。


```
var spans =document.getElementsByTagName(“span”);
```

 
>选取文档中的第一个<p>元素：


```
var firstpara =document.getElementsByTagName(“p”)[0];
```

 
>Element类也定义了getElementsByTagName()方法，但是它只选取调用该方法的元素的后代元素。
 
>节点列表和HTML集合
getElementsByName()和getElementsByTagName()都返回NodeList对象，而类似document.images和documents.forms的属性为HTMlCollection对象。
这些对象都是只读的类数组对象。有length属性，也可以像真正的数组一样索引。


```
for(var i = 0; I <document.images.length; i++)  //循环所有的图片
        document.images[i].style.display =“none”;  //……隐藏它们
```
##### 2-4. 通过CSS类选取元素
>getElementsByClassName()方法，基于其class属性值中的标识符来选取成组的文档元素。
返回值是一个实时的NodeList对象，包含文档或元素所有匹配的后代节点。只需要一个参数，但是该字符串可以有多个空格隔开的标识符组成。只有当元素的class属性值包含所有指定的标识符时才匹配，但是标识符的顺序是无关紧要的。


```
// 查找其class属性值中包含“warning”的所有元素
var warnings =document.getElementsByClassName(“warning”);
//查找以”log”命名并且有“error”和“fatal”类的元素的所有后代
var log = document.getElementById(“log”);
var fatal = log.getElementsByClassName(“fatalerror”);
```
##### 2-5. 通过css选择器选取元素

>CSS样式表有一种非常强大的语法，选择器，用来描述文档中的若干或多组元素。
- 例子：元素可以用ID、便签名或类来描述：

```
#nav//id=”nav”的元素
div//所有<div>元素
.warning//所有在class属性值中包含了”warning”的元素
```
>更一般地，元素可以基于属性值来选取：

```
p[lang=”fr”]   //所有使用法语的段落，如：<plang=”fr”>
*[name=”x”]   //所有包含name=”x”属性的元素
```

>这些基本的选择器可以组合使用：


```
span.fatal.error  //其class中包含“fatal”和“error”的所有<span>元素
span[lang=”fr”].warning  //所有使用法语的且其class中包含“warning”的<span>元素
```
>选择器可以指定文档结构：

```
#log span //id=”log”元素的后代元素中的所有的<span>元素
#log>span  //id=”log”元素的子元素中的所有<span>元素
body>h1:first-child  //<body>的子元素中的第一个<h1>元素
```

>选择器可以组合起来选取多个或多组元素：

```
div,#log   //所有<div>元素，以及id=”log”的元素
```

>方法querySelectorAll()接受包含一个css选择器的字符串参数，返回一个表示文档中匹配选择器的所有元素的NodeList对象。

>方法querySelector()方法，返回第一个匹配的元素。

#### 3. 文档的结构和遍历

##### 3-1. 作为节点树的文档

>Document对象，它的Element对象和文档中表示文本的Text对象都是Node对象。Node定义了以下重要的属性：
- parentNode:该节点的父节点
- childNodes:该节点的子节点的实时表示，是只读的类数组对象。
- firstChild,lashChild:该节点的子节点中的第一个和最后一个。
- nextSibling,previorsSibling:该节点的兄弟节点中的前一个和下一个。
- nodeType:该节点的类型
- nodeValue:Text节点或Comment节点的文本内容
- nodeName:元素的标签名，以大写形式表示

##### 3-2. 作为元素树的文档

>基于元素的文档遍历API的第二部分是Element属性，后者类似Node对象的子属性和兄弟属性：
- firstElementChild
- lastElementChild:
- nextElementSibling
- previousElementSibling:
- childElementCount:

#### 4. 属性

##### 4-1. html属性作为element的属性

>表示HTML文档元素的HTMLElement对象定义了读/写属性，它们反映了元素的HTML属性。HTMLElement定义了通用的HTTP属性（如id、标题lang和dir）的属性，以及时间处理程序属性（如onclick）。

```
var image =document.getElementById(“myimage”);
var imgurl = image.src;      //src属性是图片的URL
image.id === “myimage”    // 判断要查找图片的id
```
##### 4-2. 获取和设置非标准的html属性 

>Element类型还定义了getAttribute()和setAttribute()方法来查询和设置非标准的HTML属性，也可用来查询和设置XML文档中元素上的属性。

```
var image = document.images[0];
var width =parseInt(image.getAttribute(“WIDTH”));
image.setAttribute(“class”,”thumbnail”);
```

>Element类型还定义了相关的方法，hasAttribute()和removeAttribute(),它们用来检测命名属性是否存在和完全删除属性。

>如果操作包含来自其他命名空间中属性的XML文档，可以使用这4个方法的命名空间版本：getAttributeNS()、setAttributeNs()、hasAttributeNS()和removeAttributeNS().

##### 4-3. 数据集属性

>可以使用getAttribute()和setAttribute()来读和写非标准属性的值。
HTML5提供了一个解决方案：任意以“data-”为前缀的小写的属性名字都是合法的。
HTML5还在Element对象上定义了dataset属性。该属性指代了一个对象，它的各个属性对应于去掉前缀的data-属性。因此dataset.x应该保存data-x熟悉的值。

##### 4-4. 作为Attr节点的属性
>Node类型定义了attribute属性。对于Element对象，attribute属性是只读的类数组对象，它代表元素的所有属性。

```
document.body.attributes0]   //<body> 元素的第一个属性
document.body.attributes.bgcolor  //<body>元素的bgcolor属性
document.body.attributes[“ONLOAD”]//<body>元素的onload属性
```
#### 5. 元素的内容
##### 5-1. 作为HTML的元素内容
读取Element的innerHTML属性作为字符串标记返回那个元素的内容。
当查询outerHTML时，返回的HTML或XML标记的字符串包含被查询元素的开头和结尾标签。
insertAdjacentHTML()方法，将任意的HTML标记字符串插入到指定的元素“相邻”的位置。标记是该方法的第二个参数，并且“相邻”的精确含义依赖于第一个参数的值。第一个参数为具有以下值之一的字符串：“beforebegin”、“afterbegin”、“beforeend”和“afterend”。

##### 5-2. 作为纯文本的元素内容
>查询纯文本形式的元素内容，或者在文档中插入纯文本。标准方法是用Node的textContent属性来实现：

```
var para = document.getElementsByTagName("p")[0]; //文档中第一个<p>
var text = para.textContent; //文本是“This is a simple document.”
para.textContent = "Hello World";  //修改段落内容
在IE中，可以用Elemen的innerText属性来代替。
textContent属性就是将指定元素的所有后代Text节点简单地串联在一起。
```
##### 5-3. 作为Text节点的元素内容
>处理元素的内容来是当做一个子节点列表，每个子节点可能有它自己的一组子节点。当考虑元素的内容时，通常感兴趣的是它的Text节点。在XML文档中，你也必须准备好处理CDATASection节点——它是Text的子类型，代表了CDATA端的内容。

#### 6. 创建、插入和删除节点
##### 6-1. 创建节点
>创建新的Element节点可以使用Document对象的createElement()方法。

Text节点的创建用createTextNode("...");
Comment节点的创建用createComment()。
另一种创建新文档节点的方法是复制已经存在的节点。每个节点有一个cloneNode()方法来返回该节点的一个全新副本。给方法传递参数true也能够递归地复制所有的后代节点，或传递参数false只是执行一个浅复制。Document对象还定义了一个类似的方法叫importNode()。如果给它传递另一个文档的一个节点，它将返回一个适合本文档插入的节点的副本。传递true作为第二个参数，该方法将递归地导入所有的后代节点。

##### 6-2. 插入节点
>可以用Node的方法appendChild()或insertBefore()将它插入到文档中。如果调用appendChild()或insertBefore()将已存在文档中的一个节点再次插入，那个节点自动从它当前的位置删除并在新的位置重新插入：没有必要显式删除该节点。

##### 6.3 删除和替换节点
removeChild()方法是从文档树中删除一个节点。该方法不是在待删除的节点上调用，在其父节点上调用。
n.parentNode.removeChild(n);
replaceChild()方法删除一个子节点并用一个新的节点取而代之。第一个参数是新节点，第二个参数是需要代替的节点。
n.parentNode.replaceChild(document.createTextNode("[REDACTED]"),n);

##### 6.4 DocumentFragment
>DocumentFragment是一种特殊的Node,它作为其他节点的一个临时容器。创建一个DocumentFragment:

```
var frag = document.createDocumentFragment();
```

>DocumentFragment的特殊之处在于它使得一组节点被当做一个节点看待。

#### 7. 文档和元素的几何形状和滚动
##### 7-1. 文档坐标和视口坐标
元素的位置是以像素来度量的，向右代表X坐标的增加，向下代表Y坐标的增加。但是有两个不同的点作为坐标系的原点：
元素的X和Y坐标可以相对于文档的左上角或者相对于在其中显示文档的视口的左上角。
判定浏览器窗口的滚动条的位置：Window对象的pageXOffset和pageYOffset属性在所有浏览器中提供这些值。

##### 7-2. 查询元素的几何尺寸
判断一个元素的尺寸和位置最简单的方法是调用它的getBoundingClientRect()方法。不需要参数，返回一个有left、right、top和bottom属性的对象。left和top属性表示元素的左上角的X和Y坐标，right和bottom属性表示元素的右下角的X和Y坐标。视口坐标中的位置。
getBoundingClientRect()返回的对象还包含width和height属性。
如果想查询内联元素每个独立的矩形，调用getClientRects()方法来获得一个只读的类数组对象，它的每个元素类似于getBoundingClientRect()返回的矩形对象。

##### 7-3. 判定元素在某点
>判定在视口中的制定位置上有什么元素。这可以用Document对象的elementFromPoint()方法来判定。传递X和Y坐标，该方法返回在指定位置的一个元素。

##### 7-4. 滚动
>Window对象的ScrollTop()(和其同义词scroll())方法接受一个点的X和Y坐标，并作为滚动条的偏移量设置它们。

>Window的scrollBy()方法和scroll()和scrollTo()类似，但是它的参数的相对的，并在当前滚动条的偏移量上增加。

#### 8.  HTML表单
##### 8-1. 选取表单和表单元素
>有name或id属性的<form> 元素能够通过很多方法来选取。name="address"属性的<form>可以用以下任何方法来选取：

- window.address  //不可靠：不要使用
- document.address //仅当表单有name属性时可用
- document.forms.address  // 显示访问有name或id的表单
- document.form[n]   //不可靠：n是表单的序号。
- Form对象本身的行为类似于多个表单元素组成的HTMLCollection集合，也可以通过name或数字序号来索引。如果名为“address”的表单的第一个元素的name是“street”，可以使用以下任何一种表达式来引用该元素：
- document.forms.address[0]
- document.forms.address.street
- document.address.street  //当有name="address"，而不是只有id="address"
如果要明确地选取一个表单元素，可以索引表单对象的elements属性：
- document.forms.address.elements[0]
- document.forms.address.elements.street

##### 8-2. 表单和元素的属性

>JavaScript的Form对象支持两个方法：submit()和reset(),submit()方法来提交表单，reset()方法来重置表单元素的值。

##### 8-3. 表单和元素的事件处理程序

每个Form元素都有一个onsubmit事件处理程序来侦查表单提交，还有一个onreset事件处理程序来侦查表单重置。表单提交前调用onsubmit程序；它通过返回false能够取消提交动作。onsubmit事件处理程序只能通过单击“提交按钮来触发”。直接调用表单的submit()方法不触发onsubmit事件处理程序。
onreset事件处理程序和onsubmit是类似的。它在表单重置之前调用，通过返回false能够阻止表单元素被重置。

```
<form… onreset=”return confirm(‘Reallyerase All input and start over?’)”>
         <buttontype=”reset”>Clear and Start</button>
</form>
```

##### 8-4. 开关按钮

>单选和复选框元素都定义了checked属性。该属性是可读/写的布尔值，它指定了元素当前是否选中。defaultChecked属性也是布尔值，它是HTML属性checked的值；它指定了元素在第一次加载页面时是否选中。
15.9.6 文本域

##### 8-5. 选择框和选项元素
         Select元素size属性值大于1时，它将显示为列表中的选项。Select元素能以两种不同的方式运行，这取决于它的type属性值是如何设置的。如果<select>元素有multiple属性，也就是Select对象的type属性值为“ select-multiple”,那么允许用户选取多个选项。否则，只能选取单个选项，它的type属性值为”select-one”。
#### 9. 其他文档特性
##### 9-1. Document的属性

>Document的属性有body、documentElement和forms等这些特殊的文档元素。

- cookie：允许JavaScript程序读、写HTTPcookie的特殊的属性。
- domain：该属性允许当Web页面之间交互时，相同域名下互相信任的Web服务器之间写作放宽同源策略安全限制。
- lastModified：包含文档修改时间的字符串。
- location：与Window对象的location属性引用同一个Location对象。
- referrer:如果有，它表示浏览器导航到当前连接的上一个文档。该属性值和HTTP的Referer头信息的内容相同，只是拼写上有连个r.
- title:文档的<title>和</title>标签之间的内容。
- URL：文档的URL，只读字符串而不是Location对象。该属性值与location.href的初始值相同，只是不包含Location对象的动态变化。

##### 9-2. document.write()方法

>document.write()会将其字符串参数连接起来，然后将结果字符串插入到文档中调用它的脚本元素的位置。当脚步执行结束，浏览器解析生成的输出并显示它。例如，如下代码使用write()动态把信息输出到一个静态的HTML文档中：

```
<script>
         document.write(“<p>Documenttitle:”+document.title);
         document.write(“<br>URL:”+document.URL);
         document.write(“<br>Referredby:”+document.referrer);
         document.write(“<br>Modifiedon:”+document.lastModified);
         document.write(“<br>Accessedon:”+new Date());
</script>
```

>只有在解析文档时才能使用write()方法输出HTML到当前文档中。

##### 9-3. 查询选取的文本

>标准的window .getSelection()方法返回一个Selection对象，后者描述了当前选取的一系列一个或多个Range对象。

##### 9-4. 可编辑的内容

>有两种方法来启用编辑功能。
- 其一：设置任何标签的HTML contenteditable属性.
- 其二:设置对应元素的JavaScript contenteditable属性。

> 如下代码，一个HTML元素创建了一个可编辑的区域：

```
<div id = "editor" contenteditable>
Click to edit
</div>
```
