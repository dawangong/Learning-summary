1. 前置概念:

   - rem: 相对于根元素(html)的字体大小的单位, 例如html font-size: 14px 则 1rem = 14px。
   - vw: 当前视窗(指浏览器的可视区域)的宽度为100vw, 1vw指当前视窗宽度的百分之一。
   - 物理像素: 一个物理像素是显示器(手机屏幕)上最小的物理显示单元。
   - 设备独立像素: 设备独立像素(也叫密度无关像素)，可以认为是计算机坐标系统中得一个点，这个点代表一个可以由程序使用的虚拟像素 **(前端中可理解为 => css像素)**。
   - 设备像素比(dpr): 设备像素比 = 物理像素 / css像素, 例如 iphone6 dpr: 2。

2. rem布局:  **(以iphone6为例： 设备宽高为375×667)**

   - 设计稿使用的是物理像素 **(假设使用x1设计稿)**;

   - 资源图片使用2x图  **(iphone6 dpr: 2. 保证清晰可用x3, 保证性能可判断dpr 选择性加载)** ;

     ```javascript
     const dpr = window.devicePixelRatio || 1;
     ```

   - js获取屏幕宽度 **(css像素)**:

     ```javascript
     const clientWidth = document.documentElement.clientWidth
     ```

   - js获取dpr,设置meta:

     ```javascript
     // 进行缩放 按照物理像素显示;
     const scale = 1 / dpr;
     const metaEl = doc.createElement('meta');
     metaEl.setAttribute('name', 'viewport');
     metaEl.setAttribute('content', `width=device-width,user-scalable=no,initial-scale=${scale},maximum-scale=${scale},minimum-scale=${scale}`);
     document.head.appendChild(metaEl);
     ```

   - js设置html元素的font-size:

     ```javascript
     // 默认font-size 100px 为了计算方便 (设计稿375)
     const fontSize = 1rem = 100px;
     // 等比计算
     const scale = 375 / 100 = 3.75;
     // 设置 font-size
     document.getElementsByTagName('html')[0].style.fontSize = clientWidth / 3.75;
     ```

   - 区分pc端和电脑端: **(如果是两套代码 这步省略)**

     ```scss
     // 移动端 (使用rem function)
     @mixin respond($breakpoint) {
       @if $breakpoint == "mobile" {
         @media (max-width: 767px) {
           @content;
         }
       }
     // pc端 (使用px)
       @else if $breakpoint == "pc" {
         @media (min-width: 768px) {
           @content;
         }
       }
     }
     ```

   - 设置scss:

     ```scss
     // px换算rem
     @function rem($pixels) {
       @return ($pixels / 100) * 1rem;
     }
     ```

   - 使用示例:

     ```scss
     // 假设设计稿测出元素100px 则:
     div {
       width: rem(100);
     }
     ```

   - 优缺点: 

     | 优点                    | 缺点                |
     | ----------------------- | ------------------- |
     | 可以解决屏幕等比适配    | 前置知识点多,门槛高 |
     | 可以解决图片高清问题    | 需要借助js          |
     | 可以解决border: 1px问题 |                     |

3. vw+rem 布局:

   - 设计稿使用的是物理像素**(假设使用x1设计稿)**;

   - 设置html元素的font-size:

     ```scss
     // 默认font-size 100px 为了计算方便 (设计稿375)
     // 1rem = 100px
     // scale = 375px / 100vw(屏幕宽度)
     // 100vw / scale = 26.666vw
     html {
     	font-size: 26.666vw
     }
     ```

   - 区分pc端和电脑端: **(同上)**

   - 设置scss: **(同上)**

   - 使用示例: **(同上)**

   - 优缺点: 

     | 优点                              | 缺点       |
     | --------------------------------- | ---------- |
     | 使用vw 进行屏幕等比适配, 不需要js | 兼容性略差 |
     | 可解决图片高清, border: 1px问题   |            |
     | 前置知识少, 门槛低                |            |