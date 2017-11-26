# 目录

[toc]

## 第一章 基础知识架构

>早期网页组成只有html，而布局方面大多采用table去布局。然而对于现在的我们众所周知的是table并不适合布局。于是在当时 的这种布局下，网页的源代码混乱不堪。十分难以维护，跟别提什么可阅读性了。很容易就会错删或者疏漏什么，让整个布局随时面临随时崩溃的危险。在现在提倡的标签语义化在当时来说也是毫无存在的踪影。好在后来css出现了。有了它网页再次具有了表现性，div+css的布局方式油然而生。文档有了意义，浏览器默认样式可以被覆盖。自此，网页的结构层（html）和表现层分开了，程序的可阅读性，可维护性得到了大大的提升。

### 一、设计代码的结构
#### 1. 标签的语义化  
   1. 可以通过搜索找到想要的代码区域，比如搜索nav标签，我们就可以找到导航所在的代码块；
   2. 避免不必要的代码膨胀->因为有了语义化的标签，我们可以直接通过对标签footer、aside设置样式，而不用多余的标识（id，class）；
   3. 人们可以通过标签的语义知道你这块区域是用来做什么的，实现什么功能的；
   4. 正因为容易识别，为以后的维护和修改也提供了便利。
#### 2. 后来的变化  
   正因为开发人员意识到标签语义化有这么多好处，html5中迅速出现了很多具有语义化的标签，代替以前的写法（比如：div.section被section标签取代）。id、class也随后应运而生，它们的出现也是为了让网页结构更加分明，比如一类表现相似的div用一个类名去控制他们，不但能减少多余的代码，也能提高开发的效率，而id一般针对特殊的元素或者比较大的外层容器。
#### 3. id和class的命名  
   怎样去给id和class命名呢？正确的命名姿势是根据它们的用途。一个网页某个地方的功能一般是不会变化的。而它的样式也就是它的表现是会随时时代的变化不断的更迭。所以好的命名一定是根据它的功能命名的。常见的错误是根据它的颜色、位置等去命名。这里我认为根据用途和层级结构去命名是比较合理的方式。而目前大多数合理的命名都是根据用途去定的。
#### 4. 由此引发的新问题
   id和class的出现固然是好事，但提供方便的同时却造成了各种滥用。比如在单个独特的标签上使用class或者满篇都是id，这不但对浏览器造成了一些性能上的问题，同时增加了很多无意义的代码。
#### 5. div、span、ul、li的使用  
   div可以构造出一个网页的大多数结构，但不代表整个网页都可以用它去写，html里有很多标签都是可以在一定场景下去完成一些特定的需求的。比如侧边栏用aside，导航用nav再者你还可以用ul、li去写一些本来用class才能完成的小东西，比如可以去写列表、选项等。
### 二、文档类型、Doctype及浏览器模式

#### 1. DTD  
   DTD是一套规则，规定了xml或html不同版本中该有什么，不该有什么。
#### 2. Doctype
   Doctype,中文名文档头声明。它会告诉浏览器该用哪个DTD，由此知道要使用的html版本。简单的说就是告诉浏览器该以何种规范去解析网页。Doctype当前有两种模式。严格模式和过渡模式。它们的用途也是顾名思义不需要太多解释。
#### 3. 浏览器模式
   1. 标准模式：浏览器会以当前所支持的最高标准去渲染网页。这种模式下是标准和模型。
   2. 混杂模式：浏览器会以先后兼容的方式渲染页面，模拟老式浏览器，防止老站点无法正常工作。这种模式下是ie盒模型。  
   3. 除此之外，还有一种很少见的，只有火狐和苹果浏览器才有的“几乎标准模式”。除了处理表格的一些细节方面有细微差异，其他和标准模式无异，这里不做过多深入。  
#### 4. 注意 
   如果没有写文档头声明或者文档头声明类型错误都会导致浏览器以混杂模式呈现。



## 第二章 css选择器和良好的结构体

>如果你想要寻找设定某一个或者某一类特定的元素，那么这个时候偶就需要一套规则去选中它们，而完成这项任务的规则就是css选择器。

### 一、选择器的认识 

#### 1.css选择器汇总

选择器 | 用法 | 描述 | css版本
:---:|:---:|:---:|:---:
\#id|	#idname |	选择 id="idname" 的所有元素。|	1
.class	|.classname	|选择 class="classname" 的所有元素。|	1
element	|p	|选择所有 p 元素。|	1
element,element|	div,p	|选择所有 div 元素和所有 p 元素。|	1
element element|	div p	|选择 div 元素后代元素中的所有 p 元素。|	1
:link|	a:link	|选择所有未被访问的链接。	|1
:visited	|a:visited	|选择所有已被访问的链接。|	1
:hover	|a:hover	|选择鼠标指针位于其上的链接或其他东西。	|1
:active	|a:active	|选择活动链接（鼠标点住的一瞬间）。|	1
:first-letter	|p:first-letter	|选择每个 p 元素的首字母。	|1
:first-line	|p:first-line	|选择每个 p 元素的首行。|	1
\* | * | 选择所有元素 | 2
element>element|	div>p	|选择父元素为 div 元素的所有子元素 p 。 |2
element+element|	div+p	|选择和div 元素同级的所有 p 元素（兄弟）。	|2
[attribute]	|[target]	|选择带有 target 属性所有元素。|	2
[attribute=value]	|[target=_blank] |	选择 target="_blank" 的所有元素。	|2
[attribute~=value]|	[title~=flower]	|选择 title 属性包含单词 "flower" 的所有元素。|	2
[attribute\|=value]|	[lang\|=en]|	选择 lang 属性值以 "en" 开头的所有元素。	|2
:focus	|input:focus	|选择获得焦点的 input 元素。	|2
:first-child	|p:first-child	|选择与p同级的且第一个元素为p的元素。|	2
:before	|p:before|	在每个 p 元素的内容之前插入内容。	|2
:after	|p:after|	在每个 p 元素的内容之后插入内容。	|2
:lang(language)	|p:lang(it)	|选择带有以 "it" 开头的 lang 属性值的所有 p 元素。	|2
element1~element2|	p~ul	|选中p 元素前面的 ul元素（兄弟）。|	3
[attribute^=value]|	a[src^="https"]	|选择其 src 属性值以 "https" 开头的每个 a 元素。|	3
[attribute\$=value] |	a[src$=".pdf"]|	选择其 src 属性以 ".pdf" 结尾的所有 a 元素。|	3
[attribute\*=value] | a[src*="abc"]	|选择其 src 属性中包含 "abc" 子串的每个 a 元素。|	3
:first-of-type|	p:first-of-type	|选择同级且为p元素的第一个元素。|	3
:last-of-type|	p:last-of-type	|选择同级且为p元素的最后一个元素。|	3
:only-of-type|	p:only-of-type	|选择同级且为p元素且唯一的元素。|	3
:only-child	|p:only-child	|选择同级且为p元素且唯一的元素。|	3
:nth-child(n)|	p:nth-child(2)	|选择同级且为p元素的第二个元素。	|3
:nth-last-child(n)|	p:nth-last-child(2)	|选择同级且为p元素的倒数第二个元素。|	3
:nth-of-type(n)|	p:nth-of-type(2)	|选择同级且为p元素的第二个的元素。|	3
:nth-last-of-type(n)|	p:nth-last-of-type(2)	|选择同级且为p元素的倒数第二个元素。|	3
:last-child|	p:last-child|	选择同级且为p元素的最后一个元素。|	3
:root|	:root	|选择文档的根元素。|	3
:empty|	p:empty	|选择没有子元素的所有 p 元素（包括文本节点）。|	3
:target|	#news:target	|选择当前活动的 #news 元素。|	3
:enabled|	input:enabled	|选择每个启用这个属性的 input 元素。|	3
:disabled|	input:disabled|	选择每个被禁用的 input 元素	|3
:checked|	input:checked	|选择每个被选中的 input 元素。|	3
:not(selector)|	:not(p)	|选择除 p 元素的外的所有元素。	|3
::selection|	::selection	|选择被用户选取的元素部分。	|3
:out-of-range	|:out-of-range|	匹配值在指定区间之外的input元素	|3
:in-range	|:in-range|	匹配值在指定区间之内的input元素|	3
:read-write	|:read-write|	用于匹配可读及可写的元素	|3
:read-only|	:read-only	|用于匹配设置 "readonly"（只读） 属性的元素	|3
:optional|	:optional	|用于匹配可选的输入元素	|3
:required	|:required	|用于匹配设置了 "required" 属性的元素|	3
:valid	|:valid	|用于匹配输入值为合法的元素	|3
:invalid	|:invalid	|用于匹配输入值为非法的元素|	3

#### 2.选择器兼容性汇总

##### css2.1:

浏览器  | IE6 | IE7 | IE8 + |FF 2 +|Safari 3.0|Safari 3.2+|Chrome 2+|Opera
:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
*|	YES|	YES|	YES|	YES|	YES|	YES|	YES|	YES
E > F	|NO	|YES	|YES|	YES|	YES|	YES|	YES|	YES
E:first-child	|NO	|YES	|YES	|YES	|YES	|YES	|YES	|YES
E:hover	|NO|	YES	|YES|	YES|	YES|	YES|	YES|	YES
E:focus	|NO	|NO	|YES	|YES	|YES	|YES	|YES	|YES
E + F	|NO	|YES	|YES	|YES|	YES|	YES|	YES|	YES
E[attr]	|NO	|YES	|YES	|YES	|YES	|YES	|YES	|YES
E[attr="name"]|	NO	|YES	|YES	|YES	|YES	|YES	|YES|	YES
E[attr~="name"]|	NO|	YES|	YES|	YES|	YES|	YES|	YES|	YES
E:before|	NO|	NO|	YES|	YES|	YES|	YES|	YES|	YES
E:after	|NO	|NO	|YES|	YES|	YES|	YES|	YES|	YES

##### css3:

浏览器  | IE6 | IE7 | IE8 + |IE9 +|	FF 3	|FF 3.5 +|	Safari 3.0|	Safari 3.2+	|Chrome 2	|Opera
:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
E ~ F	|NO|	YES	|YES	|YES	|YES	|YES	|YES	|YES	|YES|	YES
E[attr^="name"]|	NO|	YES	|YES|	YES	|YES|	YES	|YES	|YES	|YES|	YES
E[attr$="name"]|	NO|	YES	|YES|	YES	|YES|	YES	|YES	|YES	|YES	|YES|
E[attr*="name"]|	NO|	YES	|YES|	YES	|YES	|YES	|YES	|YES	|YES|	YES
E[attr]="name"]|	NO|	YES|	YES|	YES	|YES	|YES	|YES	|YES	|YES|	YES
E:root|	NO|	NO|	NO|	YES|	YES|	YES|	YES|	YES|	YES|	YES
E:nth-of-type|	NO|	NO|	NO|	YES	|NO	|YES	|NO	|YES	|YES	|YES
E:nth-last-of-type|	NO|	NO|	NO	|YES|	NO|	YES|	NO|	YES|	YES|	YES
E:first-of-type	|NO|	NO	|NO	|YES	|NO	|YES	|YES	|YES	|YES	|YES
E:last-of-type|	NO|	NO	|NO|	YES|	NO|	YES	|NO	|YES|	YES	|YES
E:only-of-type|NO|	NO|	NO	|YES|	NO|	YES|	NO|	YES	|YES|	YES
E:only-child|	NO|	NO|	NO|	YES|	YES|	YES|	NO|	YES	|YES|	YES
E:last-child|	NO|	NO	|NO|	YES|	YES	|YES|	NO|	YES|	YES	|YES
E:nth-child|	NO|	NO|	NO|	YES|	NO|	YES|	NO	|YES|	YES	|YES
E:nth-last-child|	NO	|NO	|NO|	YES	|NO|	YES	|NO|	YES|	YES|	YES
E:empty|	NO	|NO|	NO|	YES|	YES	|YES	|YES	|YES|	YES	|YES
E:target	|NO	|NO	|NO|	YES|	YES|	YES|	YES|	YES	|YES	|YES
E:checked|	NO	|NO|	NO|	YES|	YES|	YES|	YES|	YES|	YES|	YES
E:selection|	NO|	NO|	NO|	YES	|YES只支持-MOZ-|	YES只支持-MOZ-	|YES|	YES	|YES|	YES
E:enabled	|NO	|NO	|NO	|YES|	YES|	YES|	YES|	YES|YES|	YES
E:disabled	|NO	|NO	|NO|	YES|	YES|	YES	|YES|	YES|	YES|	YES
E:not(s)	|NO|	NO|	NO|	YES|	YES|	YES|	YES|	YES|	YES|	YES

#### 3.伪类选择器的注意点

书写顺序：
a:link-> 
a:visited-> 
a:hover->
a:focus->
a:active

### 二、层叠性和特殊性

> 即便是在不太复杂的样式表中，一个元素也可能会有不止一套规则。这时候便有了层叠性这个概念。

#### 1.层叠性的重要度排序：

>用户自定义重要声明->
编程人员重要声明->
编程人员正常声明->
用户自定义正常声明->
浏览器代理声明

#### 2.权重：


----------


选择器种类 | 对应权重
:---:|:---:
通配选择器 | 0
元素选择器、伪元素选择器 | 1
class选择器、伪类选择器、属性选择器 | 10
id选择器 | 100
行内样式 | 1000
！important|1000+


----------


>tips:绝大多数情况避免使用!important，在日后的多人开发中很容易覆盖别人写的样式。

#### 3.属性的继承：

1.不可继承的：  

```
display、margin、border、padding、background、height、min-height、max-height、width、min-width、max-width、overflow、position、left、right、top、 bottom、z-index、float、clear、table-layout、vertical-align、page-break-after、 page-bread-before、unicode-bidi。
```
  
  2.所有元素都可以继承:

```
visibility和cursor。
```

3.内联元素可继承的有：

```
letter-spacing、word-spacing、white-space、line-height、color、font、font-family、font-size、font-style、font-variant、font-weight、text- decoration、text-transform、direction。
```

4.块状元素可继承的有：

```
text-indent和text-align。
```

5.列表元素可继承的有：

```
list-style、list-style-type、list-style-position、list-style-image。
```

6.表格元素可继承的有：

```
border-collapse。
```

#### 4.规划维护样式表：

1. 设计代码的结构

>为了便于维护样式表，最好将代码按照一定的逻辑分成几大块，你也可以像下面这样去构建你的代码结构。

- 一般性样式
    - 主体样式
    - reset样式
    - 链接
    - 标题
    - 其他元素
- 辅助样式
  - 表单
  - 通知和错误
  - 一致的条目
- 页面结构
    - 标题、页脚和导航
    - 布局
    - 其他页面结构元素
- 页面组件
    - 各个页面
- 覆盖

>2. 注释的一些功能性用法

>tip：或许我们可以像下面一样，用一个样式表中用不到的特殊标识符放在注释前面，这样我们就可以根据注释的意义去直接快捷查找对应的代码区块，这对代码的重构和日后的维护都是大有帮助的。

```
<!--@page-top、@page-help、@page-section-->
```

## 第三章 可视化模型

>本章的阅读会让你对网页常用的布局手段有更深的了解，同时你也会知道一些需要注意的点。

### 一、盒模型

#### 1. 先来看看盒模型

![image](http://upload.ouliu.net/i/20171124134537bpugs.gif)

>众所周知，盒模型分为两种，标准盒模型和ie盒模型，我们来看看两者的区别。

1. 标准盒模型：

![image](http://upload.ouliu.net/i/20171124134248pxu59.jpeg)

2. ie盒模型：

![image](http://upload.ouliu.net/i/20171124134336gxl5m.jpeg)

>总结
- 平常我们对div写的width时，width=content。
- 当对div设置box-sizing时，width=content+2padding+2border。
    - height方面和width是相似的，请自行分析。

#### 2.外边距叠加问题
1. 外边距叠加
    1. 同级元素外边距叠加情况
        1. 定义：垂直布局中，当上方有设置盒子margin-bottom属性，下方盒子有设置margin-top属性时，两者的margin就会发生叠加。
        2. 叠加规则：双方实际距离变为外边距较大的一方的数值。 
        3. 图示：
        
        ![image](http://upload.ouliu.net/i/20171124140852r5yij.png)

    2. 父级元素和子级元素的叠加
        1. 定义：当一个没有边框或者内边距的父级元素有margin-top属性而其子元素也具有margin-top属性时，两者就会发生叠加。
        2. 叠加规则：marin值会保留两者中较大的一方，并且margin-top效果是在父级元素上。
        3. 个性解决方案：给父级元素加上padding或者border（不提倡）。
        4. 图示：
        
        ![image](http://upload.ouliu.net/i/20171124142340dak0a.png)
        
    3. 元素的顶外边距和底外边距叠加
        1. 定义：一个没有内边距和边框的==空元素==，它的顶外边距和底外边距也是可以发生叠加的，假设再碰到另一个有外边距的==空元素==，它们会继续叠加。
        2. 上图：
        
        ![image](http://upload.ouliu.net/i/2017112414355897n08.gif)
        
        ![image](http://upload.ouliu.net/i/20171124144004982e1.gif)
        
2. 通用的解决方案
>  这里只说一种简单的方法，还有其他方法可以自行谷歌（涉及了css2.1中的BFC规范等问题）

- 浮动元素、inline-block 元素、绝对定位元素的 margin 不会和垂直方向上其他元素的 margin 折叠（注意这里指的是上下相邻的元素）
3. 外边距叠加带来的意义
>简单来说就是形成上下段落的等距分配布局，还是看图来的直接，上图！

![image](http://upload.ouliu.net/i/20171124144838g4fv0.png)

### 二、布局方式
>这里开始会正式开始讲解布局，因为是按照原作学习时的顺序走的，我们先来接触定位。

>tips:定位虽然是最直接最有效的布局方式，但是这里我认为千万不要大量使用，定位的滥用应该会降低网页的性能。（我之前某处看到的...）
1. css中的三种定位机制
    1. 普通流
    2. 浮动流
    3. 定位流
    
2. 定位流又可以分为
    1. 绝对定位（absolute）
    2. 相对定位（relative）
    3. 固定定位（fixed）
    
>先来了解一个概念——“文档流模型”

1. 默认情况下：你所构造的所有元素都是在二维平面上的，它们在一个面上，没有高低之分，属于一个维度。而当你使用了浮动流布局，定位流布局后，情况就会不一样了。这个时候会多一个维度，高度。也就是说它们会有高低之分，可以高的覆盖低的。从屏幕上看就是在原先的x、y轴上，多了一个z轴。z轴是指向程序员的。假设默认文档流在z轴的0点处，那么浮动的元素就会在1这个位置，定位的元素就会在2。而它们的子元素会和它们高度平级，也就是被父元素拖起来。而因为实际的网络布局中情况远比现在所设想的复杂，所以会有一个z-index属性来控制相同的定位机制产生的高度一样的问题。
2. z-index区间是[-2147483xxx,2147483xxx]。xxx是因为不同浏览器的具体数值是不一样的。
3. 结合一张图片理解下文档流模型。

![image](http://upload.ouliu.net/i/20171124153245umk1a.jpeg)


#### 1.定位流

##### 1. 绝对定位：
1. 规则：以自己嵌套关系最少的父级（祖辈级）为参考点进行定位。
2. 条件：元素本身是绝对定位（absolute），父级或祖辈级元素是定位流（任意一种定位都可以）。
3. 效果：脱离默认文档流，同层的定位元素可以横向排列，不再独占一行，并且不会发生margin叠加问题。
##### 2. 相对定位：
1. 规则：以自身现在的位置为参考点进行定位（relative）。
2. 条件：设置相对定位。
3. 效果：脱离默认文档流，自己原先的位置仍然被“占有”，相当于人过来了，影子留那里占着位置...不再独占一行，并且如果不设置位置信息，就会原地浮起，位置不变。（这个特性在一些情况下十分好用）
##### 3. 固定定位：
1. 规则：以浏览器可视窗口为参考进行定位（fixed）。
2. 条件：设置fixed（ie6下无效）。
3. 效果：因为相对于浏览器窗口定位，所以浏览时位置相对不会改变。

>就像我所知道的，大量的定位流布局对性能会有影响，所以还有一种布局可以满足日常需要。
#### 2.浮动流
1. 条件：设置元素浮动。
2. 效果：脱离默认文档流，可以横向排版。
3. 问题：
    1. 引起父级容器高度塌陷
    2. 默认比定位流高度低，可能被无意中遮挡住想显示的效果。
4. 解决方案：
    1. 如果被定位流挡住的话，可是使用z-index去调整层级关系
    2. 父级容器高度塌陷，见下表。


清除浮动手段 | 引起的新问题 | 推荐指数
:---:|:---:|:---:
父级div定义高度 | 真正的需求中布局太死板，后续问题很多| 1星
结尾处加空div标签 clear:both  | html结构中增加了无意义的div，结构冗杂| 2星
父级div定义 伪类:after 和 zoom   | 无发现，较完美的手段，兼容性好| 5星
父级div定义 overflow:hidden    | 所有的子元素都不能超出父元素范围定位，不然会消失，这种情况下表现不好| 4星
父级div定义 overflow:auto | 内部元素超过父元素时会出现滚动条| 3星
父级div 也一起浮动  | 产生新的浮动 | 2星
父级div定义 display:table| 会产生各种问题，用这种古老的东西|0星
结尾处加 br标签 clear:both | 类似第二种，br现在已经很少用了|0星
## 第四章 链接应用样式

>多变的链接操作

### 一、链接的样式
#### 1. 链接的颜色
1. css提供了：link、：visited、：hover、：focus、：active，五种伪类去实现对链接颜色的控制。
2. 顺序：

```
a:link-> a:visited-> a:hover->a:focus->a:active

```

#### 2.链接的样式
1. 个性化链接可以通过伪类和背景图片满足
2. 代码：

```
a:hover {
    color:#666;
    text-decoration:none;
    background:url(img/a.jpg) repeat-x left bottom;
}
```
3. 已访问样式的设置
    1. 方法：利用：visited
    2. 原因：如果不设置已访问样式，用户会不知道自己点过哪些网站，造成大量的回溯操作。
4. 跳转到页面指定位置处
    1. 可以通过给a标签的href属性设置#id，就可以跳转到id所在的元素位置。
    2. 问题：如果网页过于复杂，用户无法第一时间找到跳转后想看到的地方。 
    3. 解决方案：使用：target
    4. 代码如下：
    
```
<!DOCTYPE html>
<html>
<head>
<style>
:target
{
border: 2px solid #D4D4D4;
background-color: #e5eecc;
}
</style>
</head>
<body>

<h1>这是标题</h1>

<p><a href="#news1">跳转至内容 1</a></p>
<p><a href="#news2">跳转至内容 2</a></p>

<p>请点击上面的链接，:target 选择器会突出显示当前活动的 HTML 锚。</p>

<p id="news1"><b>内容 1...</b></p>
<p id="news2"><b>内容 2...</b></p>

<p><b>注释：</b> Internet Explorer 8 以及更早的版本不支持 :target 选择器。</p>

</body>
</html>

```

5. 凸显不同的链接

>其实就是根据链接的网站主体的业务方向，给链接一个背景图片用以识别。

```
1.首先利用属性选择器给所有的外部链接添加一个识别图片
a[href^="http:"]{
    background:url(img/a,jpg) no repeat right bottom;
    padding-right:10px;
}
2.但是这样会选中使用绝对路径的内部链接（自己站点的链接），所以再做下面操作把内部链接的多余识别图像删除掉
a[href^="http://www.yvming.com"],a[href^="http://yvming.com"]{
    background:url(img/a,jpg) no repeat right bottom;
    padding-right:0px;
}
```

### 二、hover和其他

1. hover可以和其他元素的配合实现翻转效果
2. css精灵图
    1. 定义：将多张图片复合在一张图片上的技术。
    2. 好处：可以减少http请求次数，同时相对的请求总大小反而还会减少。
    3. 使用：配合背景图定位使用。
    
3. css工具提醒
    1. 实现：不借助javascript，通过hover控制display或者opacity等属性和定位流实现。
    2. 优势：用css实现简单方便，不需要来往于javascript和dom之间，对性能有一定的帮助。
    
## 第五章 列表和导航

>导航及css映射的的制作思路

### 一、导航条

#### 1. 制作我的导航
1. 原理：通过ul、li标签和hover就可以实现部分导航需求。
2. 步骤：
    1. 去掉ul标签的默认项目符号；
    2. 根据水平或者垂直需求选择浮动或者不浮动;(inline-block也是可以的，不过我记着这个属性在一些浏览器下会因为代码间的空格对网页效果产生一个默认的空隙)；
    3. ul，li都不要设置宽度，这样更灵活，li的面积用padding撑起来，可以保证每个选项都看起来比例合理；
    4. 项目标识：不推荐使用默认的项目符号，太单一了，而且不好控制。可以使用背景图定位。具体点就是先用padding留出位置，再用背景属性；
    5. 效果：配合hover去写就好了，效果变化可以十分灵活，看你怎么写咯。
#### 2. 下拉菜单的思路
1. 原理：如果我告诉你hover的效果是可以冒泡的，你信吗。其实当我们对于父级元素设置hover效果后，它的子元素也会有同样的效果，这也就为子菜单的实现提供了基础。
2. 实现：
    1. 首先我们得需要一个横向菜单，里面的每一项li都是子菜单的父级；
    2. 子菜单做成垂直菜单，配合hover就可以实现。
    
tips：我觉得这已经很够了，相信不是小白的看一下思想都能知道大概怎么做。

### 二、css图像映射
1. 解释：将li定位到图像规定地区，你可以通过点击图片到对应的网站。
2. 要点：其实就是div和插入的图片大小要定的一致。
3. 实现：父级relative定位，然后再分别定位li，可以通过透明度设为0去实现。
4. 个人方法：（javascript）
    1. 首先给父级定位；
    2. 插入和父级大小一致的图像；
    3. 通过console.log配合e.clientX和e.clientY找出各个需要跳转的图像位置区间；
    4. 通过javascript和e.clientX和e.clientY进行判断，根据区间配合window.open("http://www.nicai.com");实现指定页面的跳转。
    5. 优点：我觉得不会有很多不合理的，位置被定的乱七八糟的li。

>个人认为这种功能用的不太多，好像地图之类的图像上出现的概率大点。

## 第六章 布局

>常见的布局和应用

### 一、基础布局

>在进行布局之前，我们首先要进行布局思考，将网页划为几个区域同时思考它们的重复性。

#### 1. 居中布局
  1. 定义：一般指水平居中的布局
  2. 实现
        1. 设置具体宽度，然后margin： 0 auto；
        2. 定位1（详情见代码）；
        3. 定位2（详情见代码）。
        4. 借助flex居中，父级div设置display：flex；（一些浏览器需要做兼容）子级居中div设置justify-content：center；


```
定位1：
#box {
    position：absolute；
    left：50%；
    margin-left：-1/2容器宽度
}
```


```
定位2：
#box {
    position：absolute；
    left：50%；
    transform:transition(-50%);
}
```
#### 2. 多列布局

>借助浮动就可以实现

#### 3. 流式布局：
1. 定义：根据页面大小调整页面各部分比例；
2. 实现：每个具体数值的地方都用百分比去设置；说起来容易实际挺困难，需要非常精准的计算。
3. 缺点：很难精确地按照设计图纸固定每部分位置，用的很少（最多的还是固定宽度）。

#### 4. 圣杯布局
1. 优点：允许主要内容先行加载
2. 实现：一个外围容器，先中间后两边都左浮动；margin负值+容器padding+相对定位负值；
#### 5. 双飞翼布局
1. 优点：允许主要内容先行加载
2. 实现：一个外围容器，先中间后两边都左浮动；margin负值+中间加内容容器+内容容器margin；

### 二、高级布局简介

#### 1. flex布局

>就是利用css3的flex属性就行布局，优点特别灵活，缺点对部分浏览器不兼容

#### 2. 响应式布局

>@media 可以针对不同的屏幕尺寸设置不同的样式，特别是如果你需要设置设计响应式的页面，@media 是非常有用的。
当你重置浏览器大小的过程中，页面也会根据浏览器的宽度和高度重新渲染页面。


## 第七章 bug相关

>css是一门语法简单的语言，而其难点更多在于老式浏览器带去的显示差异。很多情况下，编写css时bug并不是那么多，很多来源于编程人员对css规范认识不够深刻和正确。而如何判断bug产生的正确来源和如何去正确的解决bug，便成了一个要点...

### 一、常见的css问题
#### 1.输入错误及语法错误

>顾名思义，多发生在程序员自己敲错了代码或者语法

#### 2.特殊性和分类次序

1. 比如选择器过多的嵌套（这里指嵌套层数>3的，一般不超过三层是合适的做法）造成了更特殊的覆盖了原有的导致的效果异常。
2. 书写顺序错误，比如典型的：link和：visited顺序
3. 解决方法：firebug或者谷歌等浏览器的调试工具。这些工具可以看出来是那些规则导致现在样式的，又是有哪些规则被覆盖了。

#### 3.外边距叠加

>具体的可以参考第三章

### 二、捕捉bug

#### 1. 初步判断bug
1. 检查html，css语法（这个现代ide都会有的，相对容易做到）
2. 通过浏览器自带调试工具
3. 使用更符合w3c标准的浏览器开发（谷歌就不错，不过现在个人更青睐火狐）
4. 从开始就避免bug（少用花哨的技术，不要写多余没用的嵌套结构）

#### 2. 精确追踪bug

1. 隔离问题

>单独测试bug所在区域，可以尝试大幅修改一些属性，看看反应。

2. 提取bug

>用少量html，css重现bug，然后进行对症分析，判断是整体结构其他属性影响，还是本身问题，还是不同浏览器内核造成的问题。

3. 要实际解决问题，而不是解决表面现象。（比如位置计算不对，然后一直负margin达到效果一致，但事实上这种做法可能只是在你这个特有的电脑分辨率上，你这个品牌浏览器的这个版本的中效果ok）

4. 如果经过很多筛查，还是没办法找到问题，可以去相关社区，论坛等寻求帮助。


### 三、了解“布局”

1. 定义：ie6为什么有那么多bug？这是因为ie显示引擎使用一个称为布局的内部概念。ie通过使用布局控制元素的尺寸和位置。如果一个元素没有布局，那么它的大小和位置由最近的，具有布局的祖父类元素决定。

2. 默认拥有布局的元素。
- html（标准模式中）
- table
- tr、td
- img
- hr
- input、select、textarea、button
- iframe、embed、object、applet
- marquee

3. 设置下面属性会自动拥有布局。
- float：left or right
- display：inline-block
- width：任何值
- height：任何值
- zoom：任何值（Microsoft属性——不能通过过验证）
- writing-mode：td-rl（Microsoft属性——不能通过过验证）

>ie7中，下面的属性也会触发拥有布局

- overflow：hidden、scroll、auto
- min-width：任何值
- max-width：除none外任何值
























