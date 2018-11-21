1. 文档流： 就是规则，准确点说就是决定了元素的排列和定位的一套规则。

2. 流体布局：利用文档流本身的特性，实现的各类布局效果。文档流本身具有自适应性，所以流体布局也具有自适应性。

3. css3
   - src-set：根据屏幕密度现实对应尺寸的图片
     - 设备像素比：设备物理像素/设备独立像素（window.devicePixelRatio）
     - 设备独立像素：一种由程序使用并控制的虚拟像素，包含css像素
     - 设备物理像素：设备硬件本身决定的像素（有一堆单元格像素点组成）
     - 当我们进行浏览器缩放时，其实就是在改变浏览器的设备像素比。
     - 兼容性：https://caniuse.com/#search=srcset

   - object-fit

     - none: 默认

     - fill: 强制适应宽高，不保持比例
     - contain: 保持比例，并完整放下图片
     - cover: 保持比例，铺满。
     - scale-down: none和contain中表现小的那个

   - Grid

     - Grid 布局由两个核心组成部分是 **wrapper**（父元素|网格容器）和 **items**（子元素|网格项）

     - 网格容器

       - display: grid、inline-grid、subgrid
         - grid：块级网格
         - inline-grid：内联网格
         - subgrid：如果你的网格容器本身是另一个网格的网格项（即嵌套网格），你可以使用这个属性来表示。这个属性指明这个容器内部的**网格项**的行列尺寸直接**继承**其父级的**网格容器**属性。
       - grid-template-row：行划分规则  => 单位：px 、%、 fr
       - grid-template-columns：列划分规则 => 单位：px 、%、 fr
         - repeat()
         - fr: 等分剩余可用空间
         - 指定网格名称：[first] 40px [line2] 50px [line3] auto
       - grid-row-gap: 行间距  => 单位：px 
       - grid-column-gap：列间距  => 单位：px
       - grid-gap: 10px 10px || 10px  =>简写(行、列)
       - justify-items：单元格中的内容水平对齐方式
         - **start**：将内容对齐到网格区域(grid area)的左侧
         - **end**：将内容对齐到网格区域的右侧
         - **center**：将内容对齐到网格区域的中间（水平居中）
         - **stretch**：填满网格区域宽度（默认值）
       - align-items: 单元格中的内容垂直对齐方式 => 同上
       - justify-content && align-content :网格合计大小 相对于容器大小定位
         - **start**：将网格对齐到 网格容器(grid container) 的左边
         - **end**：将网格对齐到 网格容器 的右边
         - **center**：将网格对齐到 网格容器 的中间（水平居中）
         - **stretch**：调整 网格项(grid items) 的宽度，允许该网格填充满整个 网格容器 的宽度
         - **space-around**：在每个网格项之间放置一个均匀的空间，左右两端放置一半的空间
         - **space-between**：在每个网格项之间放置一个均匀的空间，左右两端没有空间
         - **space-evenly**：在每个栅格项目之间放置一个均匀的空间，左右两端放置一个均匀的空间
       - grid-auto-columns && grid-auto-rows：在你明确定位的行或列，超出定义的网格范围时，会创建宽度自适应的隐式网格项
         - 用来指定隐式网格项大小，可使用：px % fr
       - grid-auto-flow: 自动放置算法
         - **row**：告诉自动布局算法依次填充每行，根据需要添加新行
         - **column**：告诉自动布局算法依次填入每列，根据需要添加新列
         - **dense**：告诉自动布局算法在稍后出现较小的网格项时，尝试填充网格中较早的空缺
       - grid-template-areas
         - grid-area-name：由网格项的grid-area指定的网格区域名称
         - **.**（点号） ：代表一个空的网格单元
         - none：不定义网格区域

     - 网格项

       - grid-column-start: 1 =>起始位置（网格线-列）
       - grid-column-end: 4 =>结束位置（网格线-列）
       - grid-column：1/4 =>简写
       - grid-row-start && grid-row-end && grid-row 同上
       - grid-area: 指定网格区域名称
       - justify-self：沿着 行轴线(row axis) 对齐
         - **start**：将内容对齐到网格区域的左侧
         - **end**：将内容对齐到网格区域的右侧
         - **center**：将内容对齐到网格区域的中间（水平居中）
         - **stretch**：填充整个网格区域的宽度（这是默认值）
       - align-self: 沿着列轴线(column axis)对齐 属性值同上

