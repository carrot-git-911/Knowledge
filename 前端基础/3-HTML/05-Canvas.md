
> [!abstract] Canvas
> HTML5 Canvas 是 HTML5 提供的一个强大的绘图 API，允许开发者通过 JavaScript 在网页上动态绘制图形、动画和交互式内容。
> - Canvas 是 HTML5 新增的一个标签，可以理解为是一块"**画布**"。
> - Canvas 允许开发者通过 Javascript 在这个标签上绘制各种图案，可以将 **Javascript** 理解为是这块画布上的**画笔**。
> - Canvas 拥有多种绘制路径、矩形、圆形、字符以及图片的方法。
> - Canvas 在某些情况下可以 “代替” 图片。
> - Canvas 可用于动画、游戏、数据可视化、图片编辑器、实时视频处理等领域

## 主要特性

### 特性

**2D 绘图**：支持路径、矩形、圆形、文本等基本图形绘制
**像素操作**：可以直接操作像素数据
**动画支持**：结合 requestAnimationFrame 可实现流畅动画
**图像处理**：可以加载、绘制和操作图像
**无插件**：原生支持，不需要任何插件

### Canvas 和 SVG 的区别

Canvas
- 用 JavaScript 动态生成元素（一个 HTML 元素）
- 位图，缩放失真
- 鼠标事件只能通过 canvas 接收，其内部图形无法接收
- 数据发生变化需要重绘
- 适合图像数量较大的场景
- `IE9` 开始支持, `IE8` 以下可通过引入 `excanvas.js` 支持

SVG
- 用 `XML` 描述元素（类似 `HTML` 元素那样，可用多个元素来描述一个图形）
- 矢量图（缩放不失真）
- 支持鼠标事件，选择方便
- 不需要重绘
- 不适合图像数量较大的场景
- `IE9` 开始支持，`IE8` 以下可通过安装 `Adobe SVG Viewer` 支持
## 基础使用

**创建 Canvas 元素**
```html
<canvas id="myCanvas" width="500" height="300">
  您的浏览器不支持Canvas，请升级或更换浏览器
</canvas>
```

**获取上下文**
```js
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d'); // 获取2D绘图上下文
```

**设置宽高**
canvas 有默认宽高, 宽 300px 高 150px
`canvas` 元素提供了 `width` 和 `height` 两个属性，可设置它的宽高。
```html
<canvas id="canvas" width="300" height="200"></canvas>
```

通过 `JS` 设置宽高,不需要传入单位
```js
const canvas = document.getElementById('myCanvas');
canvas.width = "600";
canvas.height = "400";
```

**注意：不能通过 CSS 设置画布的宽高**，如果使用 `css` 设置 `canvas` 的宽高，会出现 **内容被拉伸** 的后果！！！

## 绘制基本图形

### 直线

```js
// 绘制直线
ctx.moveTo(50, 100) // 起点坐标
ctx.lineTo(200, 50) // 下一个点的坐标
ctx.stroke() // 将上面的坐标用一条线连接起来
```

**新开路径**
在绘制多条线段的同时，还要设置线段样式，通常需要开辟新路径，要不然样式之间会相互污染

- 使用 `beginPath()` 方法，重新开一个路径
- 设置新线段的样式（必须项）
### 绘制矩形

`x,y`: 矩形左上角坐标 
`width,height`: 矩形宽高

**strokeRect 描边矩形**
```js
ctx.strokeStyle = 'blue' // 设置描边颜色
ctx.lineWidth = 3 // 设置线宽
ctx.strokeRect(150, 10, 100, 80)
```

**fillRect 绘制填充矩形**
```js
ctx.fillStyle = 'red' // 设置填充颜色
ctx.fillRect(10, 10, 100, 100)
```

**rect**
rect()方法被调用后，不会立刻绘制矩形，而是需要调用 stroke()或 fill()辅助渲染
```js
ctx.rect(50, 50, 200, 100)
ctx.stroke()
ctx.fill()
```

**clearRect 清除矩形区域**
```js
ctx.clearRect(20, 20, 60, 40);
```

### 绘制路径

```js
/*
  绘制三角形路径
  1. beginPath(): 开始新路径
  2. moveTo(): 移动笔触到起点
  3. lineTo(): 绘制直线到指定点
  4. closePath(): 闭合路径（可选）
*/
ctx.beginPath();
ctx.moveTo(50, 150); // 起点
ctx.lineTo(150, 150); // 第二个点
ctx.lineTo(100, 80);  // 第三个点
ctx.closePath();      // 闭合路径（自动连接起点）
ctx.fillStyle = 'green';
ctx.fill(); // 填充路径

// 描边三角形（不填充）
ctx.beginPath();
ctx.moveTo(200, 150);
ctx.lineTo(300, 150);
ctx.lineTo(250, 80);
ctx.closePath(); 
ctx.strokeStyle = 'purple';
ctx.stroke(); // 描边路径
```

### 绘制圆形、弧形

```js
/*
  绘制完整圆形
  arc(x, y, radius, startAngle, endAngle, anticlockwise)
  x,y: 圆心坐标
  radius: 半径
  startAngle: 起始角度（弧度）
  endAngle: 结束角度
  anticlockwise: 是否逆时针（可选，默认false）
*/

ctx.beginPath();
ctx.arc(100, 250, 50, 0, Math.PI * 2); // 0到2π即为完整圆
ctx.fillStyle = 'orange';
ctx.fill();

/*
  绘制半圆
  Math.PI表示180度（π弧度）
*/
ctx.beginPath();
ctx.arc(250, 250, 50, 0, Math.PI); // 0到π即为上半圆
ctx.strokeStyle = 'brown';
ctx.lineWidth = 5;
ctx.stroke();
```

**arcTo**
```js
// cx: 两切线交点的横坐标   cy: 两切线交点的纵坐标
// x2: 结束点的横坐标  y2: 结束点的纵坐标   radius: 半径
arcTo(cx, cy, x2, y2, radius)

ctx.strokeStyle = "blue";
ctx.moveTo(40,40);
ctx.arcTo(120, 40, 120, 120, 80);
ctx.stroke();
```

### 椭圆
ellipse(x, y, radiusX, radiusY, rotation, startAngle, endAngle, anticlockwise)
起点x.起点y,半径x,半径y,旋转的角度，起始角，结果角，顺时针还是逆时针
```js
ctx.ellipse(400,400,300,200,0,0,Math.PI*2);
ctx.fillStyle="#058";
ctx.strokeStyle="#000";
ctx.fill();
ctx.stroke();
```

[HTML5 Canvas中绘制椭圆的几种方法 - 方帅 - 博客园](https://www.cnblogs.com/fangsmile/p/9923532.html)
## 样式和颜色

### 填充和描边样式

```js
// 设置填充颜色（支持CSS颜色值）
ctx.fillStyle = 'rgba(255, 0, 0, 0.5)'; // 半透明红色

// 设置描边颜色
ctx.strokeStyle = '#00FF00'; // 绿色十六进制表示

// 设置线宽（单位像素）
ctx.lineWidth = 10;

/*
  设置线头样式：
  'butt' - 平头（默认）
  'round' - 圆头
  'square' - 方头（类似round但略长）
*/
ctx.lineCap = 'round';

/*
  设置转角样式：
  'miter' - 尖角（默认）
  'round' - 圆角
  'bevel' - 斜角
*/
ctx.lineJoin = 'bevel';
```

**setLineDash() 虚线**

```js
// 第一条直线，蓝色
ctx.strokeStyle = "blue";
ctx.moveTo(40, 40);
ctx.lineTo(240, 40);
// 只传一个值，实线与空白都是4px
ctx.setLineDash([4])
ctx.stroke();

ctx.beginPath();
// 第二条直线，红色
ctx.strokeStyle = "red";
ctx.moveTo(40, 80);
ctx.lineTo(240, 80);
// 传两个值，实线是4px，空白是8px
ctx.setLineDash([4, 8])
ctx.stroke();

ctx.beginPath();
// 第三条直线，黄色
ctx.strokeStyle = "green";
ctx.moveTo(40, 120);
ctx.lineTo(240, 120);
// 传3个及以上的参数,实线与空白依次为 4px 8px 2px 4px 8px ...
ctx.setLineDash([4, 8, 2])
ctx.stroke();
```

**getLineDash** 获取虚线不重复的距离
**lineDashOffset** 设置虚线的偏移位

**非零环绕填充**
在使用 moveTo 和 lineTo 描述图形时，如果是按顺时针绘制，计数器会加1，如果是逆时针，计数器会减1，当图形所处的位置，计数结果为0，不会被填充
例：没有用 `beginPath()` 方法开辟新路径
```js
// 外层矩形
ctx.moveTo(50, 50);
ctx.lineTo(250, 50);
ctx.lineTo(250, 250);
ctx.lineTo(50, 250);
ctx.closePath();

// 内层矩形
ctx.moveTo(200, 100);
ctx.lineTo(100, 100);
ctx.lineTo(100, 200);
ctx.lineTo(200, 200);
ctx.closePath();
ctx.fillStyle = "blue";
ctx.fill();
```

### 渐变

```js
/*
  创建线性渐变
  createLinearGradient(x0, y0, x1, y1)
  (x0,y0): 渐变起点
  (x1,y1): 渐变终点
*/
const linearGradient = ctx.createLinearGradient(0, 0, 200, 0);

// 添加色标（位置0-1）
linearGradient.addColorStop(0, 'red');    // 起点红色
linearGradient.addColorStop(0.5, 'yellow'); // 中间黄色
linearGradient.addColorStop(1, 'green');  // 终点绿色

ctx.fillStyle = linearGradient;
ctx.fillRect(10, 310, 200, 100);

/*
  创建径向渐变
  createRadialGradient(x0, y0, r0, x1, y1, r1)
  (x0,y0,r0): 开始圆
  (x1,y1,r1): 结束圆
*/
const radialGradient = ctx.createRadialGradient(350, 360, 10, 350, 360, 50);
radialGradient.addColorStop(0, 'white'); // 中心白色
radialGradient.addColorStop(1, 'blue');  // 边缘蓝色

ctx.fillStyle = radialGradient;
ctx.fillRect(300, 310, 100, 100);
```

## 绘制文本 font

**设置字体样式**
语法同 CSS font 属性
```js
ctx.font = "font-style font-variant font-weight font-size/line-height font-family"

ctx.font = '30px Arial';
```

**绘制填充文本**
fillText
```js
/*
  绘制填充文本
  fillText(text, x, y, [maxWidth])
  text: 文本内容
  x,y: 文本基线起点坐标
  maxWidth: 可选，最大宽度（自动缩放）
*/

ctx.font = '30px Arial';
ctx.fillStyle = 'black';
ctx.fillText('Hello Canvas', 10, 450);
```

**绘制描边文本**
strokeText
```js
ctx.font = 'italic bold 40px Times New Roman';
ctx.strokeStyle = 'navy';
ctx.lineWidth = 2;
ctx.strokeText('Stroke Text', 10, 500);
```

**水平对齐方式**
textAlign: 水平对齐（相对于 x 坐标）
```js
ctx.textAlign = 'start'; // 默认，在指定位置的横坐标开始
ctx.textAlign = 'end' // 在指定坐标的横坐标结束
ctx.textAlign = 'left' // 左对齐
ctx.textAlign = 'right' // 右对齐
ctx.textAlign = 'center' // 居中对齐
```

**文本基线设置（垂直对齐）**

```js
ctx.textBaseline = 'alphabetic'; // 默认。文本基线是普通的字母基线
ctx.textBaseline = 'top'; // 文本基线是 `em` 方框的顶端
ctx.textBaseline = 'bottom'; // 文本基线是 `em` 方框的底端
ctx.textBaseline = 'middle'; // 文本基线是 `em` 方框的正中
ctx.textBaseline = 'hanging'; // 文本基线是悬挂基线
```

**measureText() 获取文本长度**
```js
const text = "Hello World"
ctx.fillText(text, 200, 150)
console.log(ctx.measureText(text).width)
```
## 图像操作

### 绘制图像

**js 里加载图片并渲染**

- 创建 **Image** 对象
- 引入图片
- 等待图片加载完成
- 使用 drawImage 方法渲染图片
```js
// 创建Image对象
const img = new Image();

// 设置图片源
img.src = 'example.jpg';

// 图片加载完成后执行
img.onload = function() {
  /*
    绘制原始尺寸图像
    drawImage(image, dx, dy)
    image: 图像对象
    dx,dy: 画布上的目标坐标
  */
  ctx.drawImage(img, 10, 520);
```

**把 `DOM` 里的图片拿到 `canvas` 里渲染**

```js
<!-- 1、在HTML中创建 canvas 元素 -->
<canvas id="canvas"></canvas>
<img src="https://tse3-mm.cn.bing.net/th/id/OIP-C.UmMTgQ8rtt4nprFXf8ZcYwHaKd?w=182&h=257&c=7&r=0&o=5&dpr=1.3&pid=1.7" alt="image" id="image" />
<script>
	const image = document.getElementById("image");
	window.onload = () => {
		// 绘制图片
		ctx.drawImage(image, 60, 60);
	}
</script>
```

**绘制缩放图像和切片图像**

```js
/*
	绘制缩放图像
	drawImage(image, dx, dy, dWidth, dHeight)
	dWidth,dHeight: 目标尺寸
*/
ctx.drawImage(img, 200, 520, 100, 80);
  
/*
	绘制切片图像
	drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight)
	sx,sy: 源图像切片起点
	sWidth,sHeight: 切片尺寸
*/
  ctx.drawImage(img, 50, 50, 100, 100, 350, 520, 100, 100);
};
```

### 像素操作

```js

```

## 变换和状态

### 基本变换

```js
/*
  保存当前状态（入栈）
  保存：填充/描边样式、变换矩阵、裁剪区域等
*/
ctx.save()
ctx.fillStyle = 'red';
/*
  移动原点
  translate(x, y)
  将坐标系原点移动到(x,y)
*/
ctx.translate(100, 100);
/*
  旋转坐标系
  rotate(angle)
  angle: 旋转角度（弧度）
  Math.PI = 180度
*/
ctx.rotate(Math.PI / 4); // 旋转45度
/*
  缩放坐标系
  scale(x, y)
  x: 水平缩放因子
  y: 垂直缩放因子
*/
ctx.scale(1.5, 1.5); // 水平垂直各放大1.5倍
// 绘制矩形（受当前变换影响）
ctx.fillRect(0, 0, 50, 50);
/*
  恢复之前保存的状态（出栈）
  恢复所有样式和变换
*/
ctx.restore();
```

## 动画

```js
let x = 0; // 方块x坐标

function animate() {
  /*
    清除整个画布
    如果不清除，之前绘制的图形会保留
  */
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  
  // 绘制红色方块
  ctx.fillStyle = 'red';
  ctx.fillRect(x, 100, 50, 50);
  
  // 更新位置（每次向右移动2像素）
  x += 2;
  
  // 如果超出右边界，回到左边界外
  if (x > canvas.width) x = -50;
  
  /*
    请求下一帧动画
    requestAnimationFrame比setTimeout/setInterval更适合动画
    浏览器会自动优化，通常60fps
  */
  requestAnimationFrame(animate);
}

// 启动动画
animate();
```

## 高级技巧

### 裁剪区域

```js
/*
  创建圆形路径
  这个路径将作为裁剪区域
*/
ctx.beginPath();
ctx.arc(250, 150, 80, 0, Math.PI * 2);

/*
  设置裁剪区域
  之后所有绘制内容只有在这个区域内可见
*/
ctx.clip();

// 绘制黄色矩形（只有圆形区域内部分可见）
ctx.fillStyle = 'yellow';
ctx.fillRect(150, 50, 200, 200);

/*
  注意：裁剪区域会一直有效
  如果需要取消，可以：
  1. 在设置clip前先save()
  2. clip后需要取消时restore()
*/
```

###  阴影效果

```js
// 设置阴影颜色（支持透明度）
ctx.shadowColor = 'rgba(0, 0, 0, 0.5)';

// 设置阴影模糊度（越大越模糊）
ctx.shadowBlur = 10;

// 设置阴影偏移（单位像素）
ctx.shadowOffsetX = 5;
ctx.shadowOffsetY = 5;

// 绘制白色矩形（将自动添加阴影）
ctx.fillStyle = 'white';
ctx.fillRect(300, 100, 100, 100);

/*
  重置阴影效果
  设置为透明且无偏移即可取消阴影
*/
ctx.shadowColor = 'transparent';
ctx.shadowBlur = 0;
ctx.shadowOffsetX = 0;
ctx.shadowOffsetY = 0;
```

## 性能优化
```js
// 设置阴影颜色（支持透明度）
ctx.shadowColor = 'rgba(0, 0, 0, 0.5)';

// 设置阴影模糊度（越大越模糊）
ctx.shadowBlur = 10;

// 设置阴影偏移（单位像素）
ctx.shadowOffsetX = 5;
ctx.shadowOffsetY = 5;

// 绘制白色矩形（将自动添加阴影）
ctx.fillStyle = 'white';
ctx.fillRect(300, 100, 100, 100);

/*
  重置阴影效果
  设置为透明且无偏移即可取消阴影
*/
ctx.shadowColor = 'transparent';
ctx.shadowBlur = 0;
ctx.shadowOffsetX = 0;
ctx.shadowOffsetY = 0;
```

## 时钟案例

```js
function drawClock() {
  // 获取当前时间
  const now = new Date();
  const hours = now.getHours() % 12; // 12小时制
  const minutes = now.getMinutes();
  const seconds = now.getSeconds();
  
  // 清除整个画布
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  
  // 保存当前状态
  ctx.save();
  
  // 将坐标系原点移动到画布中心
  ctx.translate(250, 250);
  
  // 绘制表盘外圆
  ctx.beginPath();
  ctx.arc(0, 0, 200, 0, Math.PI * 2);
  ctx.strokeStyle = 'black';
  ctx.lineWidth = 10;
  ctx.stroke();
  
  // 绘制12个小时刻度
  for (let i = 0; i < 12; i++) {
    ctx.save();
    // 旋转到正确位置（360°/12=30°）
    ctx.rotate(i * Math.PI / 6); // 30°转为弧度
    
    // 绘制刻度线
    ctx.beginPath();
    ctx.moveTo(180, 0);  // 起点
    ctx.lineTo(200, 0);  // 终点
    ctx.lineWidth = 5;
    ctx.stroke();
    
    ctx.restore();
  }
  
  // 绘制时针（每小时30度 + 每分钟0.5度）
  drawHand(hours * 30 + minutes * 0.5, 100, 8, 'black');
  
  // 绘制分针（每分钟6度）
  drawHand(minutes * 6, 140, 5, 'black');
  
  // 绘制秒针（每秒6度）
  drawHand(seconds * 6, 160, 2, 'red');
  
  // 绘制中心点
  ctx.beginPath();
  ctx.arc(0, 0, 10, 0, Math.PI * 2);
  ctx.fillStyle = 'red';
  ctx.fill();
  
  // 恢复之前保存的状态
  ctx.restore();
  
  // 请求下一帧动画
  requestAnimationFrame(drawClock);
}

/*
  绘制时钟指针函数
  angle: 角度（0-360）
  length: 指针长度
  width: 指针宽度
  color: 指针颜色
*/
function drawHand(angle, length, width, color) {
  ctx.save();
  
  // 转换为弧度并旋转（-90度使12点方向向上）
  ctx.rotate((angle - 90) * Math.PI / 180);
  
  // 绘制指针线
  ctx.beginPath();
  ctx.moveTo(0, 0);     // 中心点
  ctx.lineTo(0, -length); // 向上延伸
  ctx.strokeStyle = color;
  ctx.lineWidth = width;
  ctx.lineCap = 'round'; // 圆头
  ctx.stroke();
  
  ctx.restore();
}

// 启动时钟
drawClock();
```