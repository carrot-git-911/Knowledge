> [!abstract] SVG 简介
> SVG (Scalable Vector Graphics) 是一种用于描述二维矢量图形的 XML 标记语言。与位图不同，SVG 图形在放大或缩小的情况下不会失真。

特点
- 基于 XML 标准
- 矢量图形，无限缩放不失真
- 支持动画和交互
- 可通过 CSS 和 JavaScript 控制

## 基本 SVG 元素

### SVG 容器
```html
<svg width="200" height="200" viewBox="0 0 200 200">
  <!-- SVG 内容 -->
  <rect x="50" y="50" width="100" height="100" fill="blue" />
</svg>
```

- `width` 和 `height` 定义 SVG 画布的尺寸
- `viewBox` 定义可见区域和坐标系 (min-x, min-y, width, height)

### viewBox
```html
<svg viewBox="0 0 100 100" width="200" height="200">
  <circle cx="50" cy="50" r="50" fill="purple"/>
</svg>
```

- **效果**：图形自动缩放适配 200x200 画布，保持比例。

### 基本形状

**矩形**

```html
<rect x="10" y="10" width="100" height="80" fill="blue" stroke="black" stroke-width="2"/>
```
- `x`, `y`: 左上角坐标
- `width`, `height`: 宽度和高度
- `fill`: 填充颜色
- `stroke`: 描边颜色
- `stroke-width`: 描边宽度

**圆形**

```html
<circle cx="50" cy="50" r="40" fill="red" stroke="black" stroke-width="3"/>
```
- `cx`, `cy`: 圆心坐标
- `r`: 半径

**椭圆**

```html
<ellipse cx="100" cy="50" rx="80" ry="30" fill="green" opacity="0.7"/>
```

- `cx`, `cy`: 中心点坐标
- `rx`, `ry`: x轴和y轴半径
- `opacity`: 透明度 (0-1)

**直线**

```html
<line x1="100" y1="200" x2="400" y2="200" stroke="black" stroke-width="5"/>
```

- `x1`, `y1`: 起点坐标
- `x2`, `y2`: 终点坐标

**折线**

```html
<polyline points="500,200 550,250 600,200 650,250" fill="none" stroke="black" stroke-width="1"/>
```

- `points`: 一系列坐标点 (x1,y1 x2,y2 ...)

**多边形**

```html
<polygon points="100,10 40,198 190,78 10,78 160,198" fill="yellow" stroke="red" stroke-width="1">
```

- `points`: 定义多边形顶点的坐标

## 路径

```html
<path d="M10 80 Q 95 10 180 80 T 350 80" fill="none" stroke="black" stroke-width="2"/>

<path d="M10 10 H 90 V 90 H 10 L 10 10" fill="transparent" stroke="black"/>
```

- `M x y`: 移动到 (Move to)
- `L x y`: 画线到 (Line to)
- `H x`: 水平线到
- `V y`: 垂直线到
- `C x1 y1, x2 y2, x y`: 三次贝塞尔曲线
- `Q x1 y1, x y`: 二次贝塞尔曲线
- `T` 自动生成对称控制点
- `A rx ry x-axis-rotation large-arc-flag sweep-flag x y`: 椭圆弧
- `Z`: 闭合路径

## 文本
```html
<text x="400" y="100" font-family="Arial" font-size="20" fill="blue">
  Hello, SVG!
</text>
```

- `x`, `y`: 文本位置
- `font-family`: 字体
- `font-size`: 字号
- `fill`: 文本颜色
- `text-anchor`: 文本对齐 (start|middle|end)

## 渐变

线性渐变
```html
<defs>
  <linearGradient id="grad1" x1="0%" y1="0%" x2="100%" y2="0%">
    <stop offset="0%" style="stop-color:rgb(255,0,0);stop-opacity:1" />
    <stop offset="100%" style="stop-color:rgb(0,0,255);stop-opacity:1" />
  </linearGradient>
</defs>

<rect x="10" y="10" width="180" height="80" fill="url(#grad1)" />
```

径向渐变
```html
<defs>
  <radialGradient id="grad2" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">
    <stop offset="0%" style="stop-color:rgb(255,255,0);stop-opacity:1" />
    <stop offset="100%" style="stop-color:rgb(255,0,0);stop-opacity:1" />
  </radialGradient>
</defs>

<circle cx="100" cy="100" r="80" fill="url(#grad2)" />
```


## 滤镜

```html
<defs>
  <filter id="blur" x="0" y="0">
    <feGaussianBlur in="SourceGraphic" stdDeviation="5" />
  </filter>
</defs>

<rect x="20" y="20" width="160" height="160" fill="blue" filter="url(#blur)" />
```

- `feGaussianBlur`: 高斯模糊
- `feColorMatrix`: 颜色变换
- `feComposite`: 合成操作
- `feDropShadow`: 阴影效果

## 动画

```html
<circle cx="50" cy="50" r="20" fill="blue">
  <animate attributeName="cx" from="50" to="250" dur="3s" repeatCount="indefinite" />
</circle>
```


## 交互性

js 交互
```js
<svg width="200" height="200">
  <circle id="interactiveCircle" cx="100" cy="100" r="40" fill="green" />
</svg>

<script>
  document.getElementById('interactiveCircle').addEventListener('click', function() {
    this.setAttribute('fill', 'red');
    this.setAttribute('r', '50');
  });
</script>
```

鼠标悬停
```html
<style>
  #hoverRect:hover {
    fill: orange;
    stroke-width: 5;
  }
</style>

<rect id="hoverRect" x="50" y="50" width="100" height="100" fill="yellow" stroke="black" stroke-width="2" />
```


## SVG 与 HTML 集成

内联SVG
```html
<div>
  <svg width="100" height="100">
    <circle cx="50" cy="50" r="40" fill="purple" />
  </svg>
</div>
```

作为背景图像
```css
div {
  width: 200px;
  height: 200px;
  background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="200" height="200"><rect width="200" height="200" fill="lightblue"/></svg>');
}
```


1. **优化 SVG 代码**：使用工具如 SVGOMG 压缩 SVG
2. **重用元素**：使用 `<defs>` 和 `<use>` 定义和重用图形
3. **响应式设计**：使用 viewBox 和百分比宽度使 SVG 自适应
4. **可访问性**：为图形添加 `<title>` 和 `<desc>` 元素
5. **性能考虑**：复杂 SVG 可能会影响性能，适度使用