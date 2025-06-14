[CSS入门教程 - C语言网](https://www.dotcpp.com/course/css/)
## 长文本处理

### overflow 值

```css
/* 超出部分溢出显示 */
.visible {
  overflow: visible;
}
/* 超出部分被隐藏 */
.hidden {
  overflow: hidden;
}
/* 水平垂直都出现滚动条，可以滚动显示*/
.scroll {
  overflow: scroll;
}
/* 超出部分出现滚动条，未超出部分可以正常显示 */
.auto {
  overflow: auto;
}
```

**默认-字符太长溢出容器**

### 换行

使用 br 元素

`line-break`

对于非CJK（中文、日文、韩文）文本，可以通过 `line-break` 属性控制换行的行为。例如，使用 `line-break: anywhere;` 可以允许在任何字符后换行，但这在大多数场景下不是必需的，因为默认行为通常已足够


`word-wrap` 

- normal 只在允许的断字点换行（浏览器保持默认处理）
- break-word 在`长单词或 URL` 地址内部进行换行

```html
<style>
.ellipsis {
  width: 150px;
  border: solid 1px;
  word-word: break-word;
}
</style>

<div class="ellipsis">
be or not to be that is the question question, qwertyuiopoiuytrdddd whether it is nobler in the mind to suffer, the slings and arrows of outrageous fortune, or to take arms against a sea of troubles
</div>
```

![[file-pasted-20241207144329406.png]]

`word-break` 属性可以控制单词在换行时的断开方式

- normal（默认值）：不强制断行，尽可能保持单词完整性。
- break-all：允许在单词内部断行，例如超出容器宽度时会将单词拆分为多行显示。
- keep-all：尽量保持多字母语言的连续性，适用于东亚语言。

```css
.ellipsis {
  width: 150px;
  border: solid 1px;
  word-break: break-all;
}

html 同上
```

![[file-pasted-20241207144553825.png]]

`white-space` 属性可以控制元素中文本的换行方式
- normal（默认值）：文本自动换行，默认情况下会根据容器的大小自动换行。
- nowrap：文本不进行换行，超过容器宽度时会溢出。
- pre：保留原始的空白符（空格和换行符），文本按照源码中的格式显示。
- pre-wrap：保留原始的空白符，文本在遇到边界时会自动换行。
- pre-line：合并连续的空白符，文本在遇到边界时会自动换行。
单词不换行，只文本换行，单词超长会溢出盒子

`overflow-wrap` 控制元素内文本的换行方式，该属性受`word-wrap`属性的影响
字符超出部分换行
```css
.wrap {
  overflow-wrap: break-word;
}
```

字符超出部分使用连字符
```css
.hyphens {
	hyphens: auto;
}
```
![[file-pasted-20241207145747342.png]]
### 省略

> [!info] 单行文本超出省略
> 单行文本溢出省略通常用于标题等文本显示，可以通过设置 white-space 和 text-overflow 属性实现。

```css
.ellipsis {
  width: 100px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellopsis;
}
```

> [!info] 多行文本超出省略
> 多行省略主要是用来实现在固定高度的容器中，将超出容器高度的文本省略掉
>  display 属性：用来设置容器的 display 属性为-webkit-box, 使其变成一个块级盒子
> -webkit-line-clamp 属性：用来限制显示的行数。
> -webkit-box-orient 属性： 用来设置块级盒子的排列方向为垂直方向

```css
.line-clamp {
  width: 100px;
  overflow : hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2
  -webkit-box-orient: vertical;
}
```

```css
<style>
.ellipsis {
  width: 100px;
  height: 50px;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  line-height: 25px;
}
</style>
<div class="ellipsis">这是一段需要省略的多行文本内容，如果文本过长会出现省略号</div>
```
`height` `line-height` 不是必须的

通过伪元素实现，需要调整样式，不太好用
```css
<style>
  .ellipsis::after {
    content: "...";
    position: absolute;
    bottom: 0;
    right: 0;
    padding-left: 10px;
    background: white;
  }
  .ellipsis {
    position: relative;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 2;
    line-height: 25px;
    height: 50px;
  }
</style>
<div class="ellipsis">这是一段需要省略的多行文本内容，如果文本过长会出现省略号</div>
```

## 消除浏览器默认样式

为什么要初始化 CSS 样式

因为浏览器的兼容问题，不同浏览器对标签的默认值是不同的，如果没有对浏览器的 CSS 初始化，会造成相同页面在不同浏览器的显示存在差异。
## display 的值
| 属性值          | 作用                                                                                                  |
| :----------- | --------------------------------------------------------------------------------------------------- |
| none         | 元素不显示，并且会从文档流中移除                                                                                    |
| block        | 会独占一行，多个元素会另起一行，可以设置 width、height、margin 和 padding 属性                                               |
| inline       | 默认宽度为内容宽度,不可设置宽高,同行显示，但可以设置水平方向的 margin 和 padding 属性，不能设置垂直方向的 padding 和 margin；                    |
| inline-block | 将对象设置为 inline 对象，但对象的内容作为 block 对象呈现(可设置宽高)，之后的内联对象会被排列在同一行内,设置, 设置 padding-top margin-top 整个一行都会位移 |
| list-item    | 像块类型元素一样显示,并添加样式列表标记                                                                                |
| table        | 此元素会作为块级表格来显示，子元素 display: table-cell                                                               |
| inherit      | 规定应该从父元素继承 display 属性的值                                                                             |
## position

使用 `position` 的时候，需要记住**子绝父相**

| 属性值      | 作用                                                                                   |
| -------- | :----------------------------------------------------------------------------------- |
| relative | 生成相对定位的元素，定位原点是元素本身所在的位置                                                             |
| absolute | 生成绝对定位的元素，定位原点是离自己这一级元素最近的一级 `position` 设置为 `absolute` 或者 `relative` 的父元素的左上角为原点的。   |
| fixed    | 生成绝对定位的元素,指定元素相对于屏幕视口(viewport)的位置来指定元素位置。元素的位置在屏幕滚动时不会改变,比如回到顶部的按钮一般都是用此定位方式。       |
| static   | 默认值没有定位，元素出现在正常的文档流中,会忽略 top,bottom,left,right 或者 z-index 声明，块级元素从上往下纵向排布，行级元素从左向右排列 |
| inherit  | 规定从父元素继承 `position` 属性的值                                                             |
| sticky   | 新增元素，目前兼容性可能不是那么的好，可以设置 position:sticky 同时给一个top,bottom,right,left之一即可。              |

> [!info] 对 sticky 定位的理解
> sticky 英文字面意思是粘贴，所以可以把它称之为粘性定位。语法：**position: sticky;** 基于用户的滚动位置来定位。
> 粘性定位的元素是依赖于用户的滚动的，在 **position:relative** 与 **position:fixed** 定位之间切换。
> 
> 它的行为就像 **position:relative;** 而当页面滚动超出目标区域时，它的表现就像 **position:fixed;**，它会固定在目标位置。元素定位表现为在跨越特定阈值前为相对定位，之后为固定定位。
> 
> 这个特定阈值指的是 top, right, bottom 或 left 之一，换言之，指定 top, right, bottom 或 left 四个阈值其中之一，才可使粘性定位生效。否则其行为与相对定位相同。

> [!warning] 注意
> 使用`sticky`时，必须指定top、bottom、left、right4个值之一，不然只会处于相对定位
> 
> `sticky` 只在其父元素内有效果，且保证父元素的高度要高于 `sticky` 的高度；
> 
> 父元素不能 `overflow:hidden` 或者 `overflow:auto` 等属性。

## 单冒号 和 双冒号

单冒号 `:` 用于 CSS3伪类
双冒号 `::` 用于 CSS3伪元素

> [!question] ::before 和 :after中双冒号和单冒号有什么区别
> `::before`就是以一个子元素的存在，定义在元素主体内容之前的一个伪元素。并不存在于`dom`之中，只存在在页面之中。
> 
> **注意：** `:before` 和 `:after` 这两个伪元素，是在`CSS2.1`里新出现的。起初，伪元素的前缀使用的是单冒号语法，但随着`Web`的进化，在`CSS3`的规范里，伪元素的语法被修改成使用双冒号，成为`::before ::after`

## display:inline-block 什么时候会显示间隙

在 HTML 中，元素之间的 **换行符** 或 **空格** 会被浏览器当作 **空白字符** 渲染，这在 **行内元素**（如 `span`、`a`、`inline-block` 元素等）之间产生了一个可见的间隙。这是因为 HTML 标签本身并不会直接控制这些空白字符，浏览器会根据这些字符的位置来决定是否渲染间隙。

```html
<style>
.box {
    width: 400px;
    height: 200px;
    border: solid 1px;
  }
 .inner {
    width: 50px;
    height: 50px;
    background-color: blue;
    display: inline-block;
  }
  .inner2 {
    width: 50px;
    height: 50px;
    background-color: red;
    display: inline-block;
  }
</style>
<div class="box">
  <div class="inner">123</div>
  <div class="inner2">234</div>
</div>
```

效果
![[file-pasted-20241207224124290.png]]

修改如下

删除换行符
```html
<div class="inner">123</div><div class="inner2">234</div>
```

使用注释，注释掉空白字符
```html
<div class="inner">123</div><!--
--><div class="inner2">234</div>
```

margin 使用负值解决，不好维护
 ```css
 .inner2 {
   width: 50px;
   height: 50px;
   background-color: red;
   display: inline-block;
   margin-left: -5px;
 }
 ```

使用font-size时，可通过设置 `font-size:0`、`letter-spacing`、`word-spacing` 解决
```css
.box {
  width: 400px;
  height: 200px;
  border: solid 1px;
  font-size: 0;
}

或
.box {
  letter-spacing: -5px;
}
.inner {
  letter-spacing: 0; // 去除掉父元素设置letter-spacing的影响
}
.inner2 {
  letter-spacing: 0;
}

或
.box {
  word-spacing: -5px;
}
.inner {
  word-spacing: 0;
}
.inner2 {
  word-spacing: 0;
}



```

使用 flex 布局
## 图片格式

`png` 便携式网络图片，是一种无损数据压缩位图文件格式，优点是压缩比高，色彩好，大多数地方都可以用

`jpg` 是一种针对相片使用的一种失真压缩方法，是一种破坏性压缩，在色调及颜色平滑变化做的不错，在 `www` 上 被用来存储和传输照片的格式

`gif` 是一种位图文件格式，以8位色重现真色彩的图像。可以实现动画效果

`bmp` 优点： 高质量图片；缺点： 体积太大； 适用场景： `windows` 桌面壁纸；

`webp` 格式是谷歌在2010年推出的图片格式，压缩率只有 `jpg` 的2/3，大小比 `png` 小了45%。缺点是压缩的时间更久了，兼容性不好，目前谷歌和 `opera` 支持
## line-height

line-height 指的是一行字的高度，包含了字间距，实际上是下一行基线到上一行基线的距离
如果一个标签没有定义 height 属性，那么其最终表现的高度是由 `line-height` 决定的。
一个容器没有设置高度，那么撑开容器的高度的是 `line-height`,而不是容器内部的文字内容。
把 `line-height` 值设置为 `height` 一样大小的值可以实现单行文字的垂直居中。
`line-height`和`height`都能撑开一个高度，`height`会触发`haslayout`，而`line-height`不会。

 **line-height 的赋值方式：**
- 带单位：px 是固定值，而 em 会参考父元素 font-size 值计算自身的行高
- 纯数字：会把比例传递给后代。例如，父级行高为 1.5，子元素字体为 18px，则子元素行高为 1.5 * 18 = 27px
- 百分比：将计算后的值传递给后代
## 隐藏元素的方法

`display: none` 渲染树不会包含该渲染对象，因此该元素不会在页面中占据位置，也不会响应绑定的监听事件

`visibility: hidden` 元素在页面中仍占据空间，但是不会响应绑定的监听事件。

`opacity: 0` 将元素的透明度设置为 0，。元素在页面中仍然占据空间，并且能够响应元素绑定的监听事件。

`position: absolute` 通过使用绝对定位将元素移除可视区域内，以此来实现元素的隐藏

`z-index` 来使其他元素遮盖住该元素，以此来实现隐藏。

`transform: scale(0,0)` 将元素缩放为 0，来实现元素的隐藏。这种方法下，元素仍在页面中占据位置，但是不会响应绑定的监听事件

`<div hidden="hidden">` `HTML5` 属性,效果和 `display:none;` 相同，但这个属性用于记录一个元素的状态；

`height: 0` 将元素高度设为 0 ，并消除边框；

`filter: blur(0)` CSS3属性，括号内的数值越大，图像高斯模糊的程度越大，到达一定程度可使图像消失

## 分析比较 opacity: 0、visibility: hidden、display: none 优劣和适用场景

结构
display:none: 会让元素完全从渲染树中消失，渲染的时候不占据任何空间, 不能点击， 
visibility: hidden:不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，不能点击 
opacity: 0: 不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，可以点击

继承
display: none 和 opacity: 0：是非继承属性，子孙节点消失由于元素从渲染树消失造成，通过修改子孙节点属性无法显示。 
visibility: hidden：是继承属性，子孙节点消失由于继承了 hidden，通过设置 visibility: visible;可以让子孙节点显式。

性能
displaynone : 修改元素会造成文档回流,读屏器不会读取 display: none 元素内容，性能消耗较大
visibility:hidden: 修改元素只会造成本元素的重绘,性能消耗较少读屏器读取 visibility: hidden 元素内容 
opacity: 0 ： 修改元素会造成重绘，性能消耗较少

## css hack

原理： 利用不同浏览器对`CSS`的支持和解析结果不一样编写针对特定浏览器的样式。
常见的`hack`有： **属性hack**、**选择器hack**、**IE条件注释**。

## link 与 @import 的区别？

`link` 是 `HTML` 提供的标签，不仅可以加载 css 文件，还能定义 RSS、rel 连接属性等。而 `@import` 是 `CSS` 中的语法规则

`link` 最大限度支持并行下载，`@import` 过多嵌套导致串行下载，出现 `FOUC`

浏览器对 `link` 支持早于 `@import` ，可以使用 `@import` 对老浏览器隐藏样式；

`@import`必须在样式规则之前，可以在css文件中引用其他文件；

## FOUC

flash of unstyle content

当使用 `@import` 导入 `CSS` 时，会导致某些页面在 `IE` 出现奇怪的现象： 没有样式的页面内容显示瞬间闪烁，这种现象被称为“文档样式暂时失效”，简称 `FOUC`。

产生原因： 当样式表晚于结构性html加载时，加载到此样式表时，页面将会停止之前的渲染。等待此样式表被下载和解析后，再重新渲染页面，期间导致短暂的花屏现象。

解决办法： 只要在`<head>`之间加入一个`<link>`或者`<script>``</script>`元素即可。

## 浏览器是怎样解析 CSS 选择器的
待查

## 元素竖向的百分比设定是相对于容器的高度吗

一般来说，子元素的百分比单位都是以父元素为依据。但是`margin`和`padding`例外。元素的`height`是相对于容器的高度，但是元素的`margin`和`padding`是相对于容器的宽度。

## css sprites

CSS 精灵图，把一堆小的图片整合到一张大的图片上，利用 `CSS` 的 `“background-image”`，`“background- repeat”``，“background-position”` 的组合进行背景定位

`background-position` 可以用数字能精确的定位出背景图片的位置，减轻服务器对图片的请求数量。

**优点：**
- 利用`CSS Sprites`能很好地减少网页的http请求，从而大大提高了页面的性能，这也是`CSS Sprites`最大的优点；
- `CSS Sprites`能减少图片的字节，曾经多次比较过，把3张图片合并成1张图片的字节总是小于这3张图片的字节总和。

**缺点：**

- 在图片合并时，要把多张图片有序的、合理的合并成一张图片，还要留好足够的空间，防止板块内出现不必要的背景。在宽屏及高分辨率下的自适应页面，如果背景不够宽，很容易出现背景断裂；

- `CSSSprites`在开发的时候相对来说有点麻烦，需要借助`photoshop`或其他工具来对每个背景单元测量其准确的位置。

- 维护方面：`CSS Sprites`在维护的时候比较麻烦，页面背景有少许改动时，就要改这张合并的图片，无需改的地方尽量不要动，这样避免改动更多的`CSS`，如果在原来的地方放不下，又只能（最好）往下加图片，这样图片的字节就增加了，还要改动`CSS`。

## 简述什么是内容与表现分离

把网站理解成一个人，`html`就是构成人体的‘骨架’，`css`就是人体的‘装饰’，比如衣服，饰品等；而`javascript`就相当于人做出的‘动作’，这样就通俗易懂了。

对于内容和表现分离，小编的理解是：尽量不要再`html`中插入行内样式，尽量将css抽成一个独立的模块，实现`html`‘骨架’和样式的分离，利于搜索引擎的同时，也便于后期维护。

##  :link、:visited、:hover、:active 的执行顺序是怎么样的？

`L-V-H-A`，`l(link)ov(visited)e h(hover)a(active)te`，即用喜欢和讨厌两个词来概括。

## 为什么要语义化以及对于标签语义化的理解

原因： **为了在没有css的情况下，页面也能呈现出很好的内筒结构和代码架构（可以理解为为了裸奔时好看哈哈哈）**。

理解：

- 去掉或者丢失样式的时候能够让页面呈现清晰的结构；
- 有利于`SEO`，可以和搜索引擎建立良好的沟通，有助于爬虫抓取更多的有效信息（爬虫依赖于标签来确定上下文和各个关键字的权重）；
- 方便其他设备解析（如屏幕阅读器，盲人阅读器，移动设备等），以意义的方式来渲染网页；
- 便于团队的开发和维护，语义化更具有可读性，遵循`W3C`标准的团队都遵循这个标准，可以减少代码差异化；


## style 标签写在 body 后与 body 前有什么区别？
## position:fixed;在手机端无效怎么处理？



## border:none;与 border:0

## 什么是 critical CSS

`Critical CSS` 是一种提取首屏中 `CSS` 的技术，以便尽快将内容呈现给用户。这是快速加载网页首屏的好方法。
核心思路：

（1）、抽取出首页的`CSS`；

（2）、用行内css样式，加载这部分的`css(critical CSS)`;

（3）、等到页面加载完之后，再加载整个 `css`，会有一部分 `css` 与 `critical css` 重叠；


background
object fit

自定义属性

动画

## clip-path

[css中clip属性 - 浅笑· - 博客园](https://www.cnblogs.com/qianxiaox/p/13761346.html)

## 如何判断元素是否到达可视区域

`window.innerHeight` 浏览器可视区域高度
`document.body.scrollTop || document.documentElement.scrollTop` 浏览器滚动过的距离
`img.offsetTop` 元素顶部距离文档顶部的高度
内容达到显示区域，img.offsetTop < window.innerHeight + document.body.scrollTop

![[Pasted image 20230814223407.png|602]]


## 重绘与重排(回流)的区别
**重排:** 部分渲染树（或者整个渲染树）需要重新分析并且节点尺寸需要重新计算，表现为重新生成布局，重新排列元素
**重绘:** 由于节点的几何属性发生改变或者由于样式发生改变，例如改变元素背景色时，屏幕上的部分内容需要更新，表现为某些元素的外观被改变

单单改变元素的外观，肯定不会引起网页重新生成布局，但当浏览器完成重排之后，将会重新绘制受到此次重排影响的部分

重排和重绘代价是高昂的，它们会破坏用户体验，并且让 UI 展示非常迟缓，而相比之下重排的性能影响更大，在两者无法避免的情况下，一般我们宁可选择代价更小的重绘。

『重绘』不一定会出现『重排』，『重排』必然会出现『重绘』。
**导致重排**
1. 改变窗口大小
2. 添加或者删除 DOM 元素
3. 修改 DOM 元素的位置、尺寸、边距等
4. 改变元素的字体大小
5. 显示或隐藏一个 DOM 元素
6. 改变元素的 class 属性
**导致重绘**
1. 修改 DOM 元素的背景、颜色、字体等属性
2. 改变元素的文本内容
3. 修改元素的边框、圆角等属性
**一些优化方案**
1. 避免逐项更改样式，使用 class 类对样式进行统一更改，减少回流。
2. 避免循环操作 DOM。
3. 尽量避免多次获取 offsetXXX、scrollXXX、clientXXX 等属性，如果不能避免则用变量保存来尽量减少回流。
4. 动画效果应用于 position 为 absolute 或 fixed 的元素上，动画因为脱离文档流，减少回流与重绘。
5. 为动画开启 GPU 加速，开启 css3动画加速的本质是渲染元素图层在 GPU 中 transform 属性不会触发重绘。所以尽量使用 transform: translate() 代替 left 与 top 进行动画

## 浏览器解析页面主要分为以下的流程：

1. 解析 HTML，形成 HTML DOM 树

2. 解析 CSS，生成 CSS 规则树

3. 将 HTML DOM 树与 CSS 规则树结合（attachment），生成 Render 树

4. 布局 Render 树（layout/reflow），负责各元素大小、位置的计算

5. 绘制 Render 树（painting），绘制页面像素信息

6. 浏览器将各层信息发送给 GPU，GPU 将各层合成，显示在屏幕上