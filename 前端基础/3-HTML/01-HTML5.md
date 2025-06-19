> [!abstract]
> HTML5 是 HTML 的第五个主要版本，于 2014 年 10 月由 W3C 完成标准制定。它不仅是 HTML 的更新，还包含了一系列相关技术的集合

## HTML5文档结构

### 基本结构
```js
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HTML5 文档</title>
</head>
<body>
    <!-- 页面内容 -->
</body>
</html>
```

文档类型声明 `<!DOCTYPE html>`

- 必须放在第一行
- 告诉浏览器这是 HTML5 文档

根元素 `html`

- 包含整个 HTML 文档
- `lang` 属性指定文档语言

头 `<head>`

- 包含元数据和链接信息
- 不会直接显示在页面上

主体 `<body>` 
包含所有可见内容

### meta

基本语法
```html
<meta name="属性名" content="属性值">

<meta http-equiv="属性名" content="属性值">

<meta charset="字符集">
```


字符集声明
定义文档的字符编码
这是现代网页中最常见的 `<meta>` 标签，应该放在 `<head>` 的最前面
```html
<meta charset="UTF-8">
```

页面描述和关键词
```js
<meta name="description" content="这是一个关于HTML meta标签的详细说明页面">
<meta name="keywords" content="HTML, meta, 元数据, 教程">
```

视窗设置
针对移动设备优化
```js
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

常用参数
- width=

## HTML5新增语义化标签

### 结构标签

```html
<header> - 定义文档或节的页眉
<footer> - 定义文档或节的页脚
<nav> - 定义导航链接
<article>` - 定义独立的自包含内容
<section> - 定义文档中的节
<aisde> - 定义
<main>
```

### 媒体标签

`<figure>` 和 `<figcaption>` - 定义图像及其标题
`<video>` - 嵌入视频
`<audio>` - 嵌入音频

### 其他语义标签

`<mark>` - 定义标记/高亮文本
`<time>` - 定义日期/时间
`<progress>` - 定义任务进度
`<meter>` - 定义度衡量


## HTML5表单增强

### 新的输入类型

```html
<input type="email"> - 电子邮件地址
<input type="url"> - URL 地址
<input type="number"> - 数值输入
<input type="range"> - 滑动条
<input type="date"> - 日期选择器
<input type="time"> - 时间选择器
<input type="datetime-local"> - 本地日期时间
<input type="month"> - 月份选择器
<input type="week"> - 周选择器
<input type="color"> - 颜色选择器
<input type="search"> - 搜索框
<input type="tel"> - 电话号码
```

### 表单新属性

```html
placeholder - 输入框提示文本
autofocus - 自动获取焦点
required - 必填字段
pattern - 正则验证
autocomplete - 自动完成
multiple - 允许多个值
min max step 数值范围限制
```

### 新的表单元素

```js
<datalist> 定义输入框的选项列表
<output> 定义计算结果
```

### 表单验证示例

```html
<form>
  <label for="email">邮箱：</label>
  <input type="email" id="email" required placeholder="输入邮箱">
  
  <label for="age">年龄：</label>
  <input type="number" id="age" min="18" max="99">
  
  <label for="website">个人网站:</label>
  <input type="url" id="website" pattern="https?://.+">
  
  <input type="submit" value="提交">
</form>
```

## HTML5多媒体

### 音频和视频

```html
<!-- 音频 -->
<audio controls>
  <source src="audio.mp3" type="audio/mpeg">
  <source src="audio.ogg" type="audio/ogg">
  您的浏览器不支持audio元素
</audio>

<!-- 视频 -->
<video width="320" height="240" controls>
  <source src="movie.mp4" type="video/mp4">
  <source src="movie.ogg" type="video/ogg">
  您的浏览器不支持 video 元素
</video>
```

```js
controls - 显示控制面板
autoplay - 自动播放
loop - 循环播放
muted - 静音
preload - 预加载
poster - 视频封面（仅视频）
width/height - 尺寸（仅视频）
```


## HTML5图形绘制

canvas

```html
<canvas id="myCanvas" width="200" height="100"></canvas>

<script>
  var canvas = document.getElementById("myCanvas");
  var ctx = canvas.getContext("2d");
  ctx.fillStyle = "#FF0000";
  ctx.fillRect(0, 0, 150, 75);
</script>
```

SVG

```html
<svg width="100" height="100">
    <circle cx="50" cy="50" r="40" stroke="green" stroke-width="4" fill="yellow" />
</svg>
```


## HTML5 Web 存储

### localStorage

```js
// 存储数据
localStorage.setItem("username", "JohnDoe")

// 获取数据
var user = localStorage.getItem("username")

// 移除数据
localStorage。removeItem("username")

// 清空所有
localStorage.clear()
```

### sessionStorage

```js
// 使用方法同 localStorage，但仅在当前会话有效
sessionStorage.setItem("token", "abc123")
```

## 离线应用

Manifest 文件

```js
<!DOCTYPE html>
<html manifest="demo.appcache">
...
</html>
```

demo.appcache 内容

```
CACHE MANIFEST
# v1.0.0

CACHE:
index.html
style.css
image.jpg
script.js

NETWORK:
*

FALLBACK:
/ offline.html
```

## API 增强

地理位置

```js
if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(
        function(position) {
            console.log("纬度: " + position.coords.latitude);
            console.log("经度: " + position.coords.longitude);
        },
        function(error) {
            console.log("错误: " + error.message);
        }
    );
}
```

Web Workers

```js
// main.js
var worker = new Worker('worker.js')

worker.postMessage('开始计算')
worker.onmessage = function(e) {
  console.log(e.data)
}

// worker.js
onmessage = function(e) {
  var result = heavyCalculation()
  postMessage(result)
}
```

WebSocket

```js
var socket = new WebSocket("ws://example.com/server")

socket.onopen = function(e) {
  socket.send('Hello Server')
}

socket.onmessage = function(e) {
  console.log('收到消息'+e.data)
}

socket.onclose = function(e) {
  console.log('连接关闭')
}
```


拖放

```html
<div id="dragme" draggable="true">拖我</div>
<div id="dropzone">放在这里</div>

<script>

</script>
```

响应式设计

```js
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```


picture

```js
<picture>
    <source media="(min-width: 650px)" srcset="img_pink_flowers.jpg">
    <source media="(min-width: 465px)" srcset="img_white_flower.jpg">
    <img src="img_orange_flowers.jpg" alt="Flowers">
</picture>
```

内容可编辑

```js
<div contenteditable="true">可以编辑这段文字</div>
```


## 兼容性与优化

- **Polyfill**：如 `html5shiv` 支持旧版 IE。
    
- **Modernizr**：检测浏览器支持特性。
    
- **性能优化**：懒加载图片、异步脚本（`async` / `defer`）、资源预加载（`<link rel="preload">`）。

## DOM 查询操作

querySelector
查询文档中的第一个匹配元素, 如果匹配到了，返回匹配到的元素，没有返回 null
```js
var element = document.querySelector('.my-class');
console.log(element);
```
querySelectorAll
该方法返回所有满足条件的元素，结果是个 nodeList 集合
```js
var elements = document.querySelectorAll('.my-class');
console.log(elements);
```

matches
