> [!abstract] leaflet
> - 轻量级开源JavaScript库（约42KB），兼容主流浏览器（包括移动端）。
> - 简单、高效并且易用
> - 拥有大量的扩展插件，源码可读性好

## 相关网站

[Leaflet](https://leafletjs.cn/index.html)
[Turf.js中文网](https://turfjs.fenxianglu.cn/docs/api/area)
[地图技术知识：leafLet使用高德、百度、天地图的方式\_l.tilelayer.chinaprovider-CSDN博客](https://blog.csdn.net/weixin_45031595/article/details/121751742)
[LeafLet 简单使用 - DarJeely - 博客园](https://www.cnblogs.com/Jeely/p/11132192.html)
[基于vue3+ts的leaflet基本使用: 主要是学习leaflet，基于vue3+ts的leaflet基本使用](https://gitee.com/tianyu0-0/leaflet-vue3)
[产品小姐姐：地图（谷歌）选点，我还不能自己点？💡 背景 🎬 场景设定：选房子 某天产品说：“用户能搜地址，也能点地图 - 掘金](https://juejin.cn/post/7501649258279845939)
[使用Leaflet 搭建一个前端地图项目，实现类似原神、黑神话悟空的标点互动地图效果\_leaflet项目-CSDN博客](https://blog.csdn.net/Beatingworldline/article/details/145510367)

github
[GitHub - vue-leaflet/vue-leaflet: vue-leaflet compatible with vue3](https://github.com/vue-leaflet/vue-leaflet)
[wukong-map: 仿游民星空地图项目：leaflet+vue+ejs](https://gitee.com/jumping-world-line/wukong-map)

## 安装与初始化

安装依赖
```js
npm i leaflet
```

引入
```js
import L from 'leaflet'
import 'leaflet/dist/leaflet.css';
```

创建地图实例
```js
// 使用 id 为 map 的 div 容器初始化地图，同时指定地图的中心点和缩放级别
var map = L.map('map', {
  center: [51.505, -0.09],
  zoom: 13
})
```

```js
// 在一个指定id的div元素中初始化地图并设置相关参数
L.map(<String> id, <Map options> options?)
// 在一个 div 实例中初始化地图并设置相关参数。
L.map(<HTMLElement>el, <Map options> options?)
```

## L.map options

**attributionControl** 默认情况下,是否将 attribution 版权控件添加到地图中,
**zoomControl** 默认情况下,是否将 zoom 缩放控件添加到地图中。
**dragging** 地图是否可以通过 mouse/touch 进行拖动。
**center** 地图初始化时的中心点位置
**zoom** 地图初始化时的缩放等级
**layers** 默认添加到地图上的图层组
**keyboard** 地图是否获得焦点，并且允许用户通过键盘和 +/- 来进行浏览地图。

## UI 图层
### Marker 标记
L.Marker 用于在地图上显示可点击/可拖动的图标

L.marker(latlng,options?)
```js
const marker = L.marker([39.91714508041264, 116.39718532562257]).addTo(map)
```

### Popup 弹出窗口

用于在地图的某些位置打开弹出窗口

L.popup(options?,source?)

```js
marker.bindPopup('<b>Hello world!</b><br>I am a popup.').openPopup()
```

```js
const popup = L.popup()
.setLatLng([39.91714508041264, 116.39718532562257])
.setContent('I am a standalone popup.')
.openOn(map)
```

### Tooltip 工具提示

用于在地图图层顶部显示小文本。

```js
marker.bindTooltip("my tooltip text").openTooltip();
```

```js
const tooltip = L.tooltip({
  direction: 'top',
  offset: [0, 0],
  permanent: true, // 一直显示
  opacity: 0.7,
  className:'my-tooltip'
})
.setLatLng([40.91714508041264, 116.39718532562257])
.setContent('我是一个工具提示').openOn(map)

marker.bindTooltip(tooltip).openTooltip()
```


## 栅格图层
### TileLayer
用于在地图上加载和显示瓦片图层。大多数tile服务器都需要属性

```js
const Layer = L.tileLayer('https://webst01.is.autonavi.com/appmaptile?style=6&x={x}&y={y}&z={z}', {
  maxZoom: 20,
  minZoom: 3,
  attribution: 'lxb',
}).addTo(map);
```

#### url 模板
```js
https://{s}.somedomain.com/{foo}/{z}/{x}/{y}/{r}.png
```

{s}是指可用的子域之一
{z}缩放级别
{x}{y} 瓦片坐标
{r}可以用来在 url 中添加“@2x”以加载视网膜瓦片

#### options
minZoom/maxZoom: 此图层要显示的最大最小缩放级别
errorTileUrl 显示瓦片图像的 URL，以代替加载失败的瓦片。

继承自 GridLayer
tileSize 网格中瓦片的宽度和高度
opacity 瓦片不透明度
zIndex 瓦片图层的显性 zIndex
className 为瓦片图层指定的自定义类名。默认是空的。

继承自 Layer 图层的选项
attribution：归属控制中要显示的字符串，例如 "© OpenStreetMap 贡献者"。 它描述了图层数据，通常是对版权所有者和瓦片提供者的法律义务。

### TileLayer.WMS
```js
const wmsLayer = L.tileLayer.wms("http://mesonet.agron.iastate.edu/cgi-bin/wms/nexrad/n0r.cgi", {
  layers: 'nexrad-n0r-900913',
  format: 'image/png',
  transparent: true,
  attribution: "Weather data © 2012 IEM Nexrad"
});
```

###  ImageOverlay
用于在地图的特定边界上加载和显示单个图像

## 矢量图层

### polyline 折线
一个用于在地图上绘制折线覆盖物的类

```js
const latlngs = [
  [39.91714508041264, 116.49718532562257],
  [39.98714508041264, 116.39718532562257],
  [39.91714508041264, 116.39718532562257],
  [39.91714508041264, 116.49718532562257]
]
const polyline = L.polyline(latlngs, {
  color: 'red',
  weight: 3,
  opacity: 0.5,
  smoothFactor: 1 // 平滑度
}).addTo(map)
```

### Polygon 多边形

一个用于在地图上绘制多边形覆盖物的类

```js
const latlngs = [
  [39.91714508041264, 116.49718532562257],
  [39.98714508041264, 116.39718532562257],
  [39.91714508041264, 116.39718532562257],
  [39.91714508041264, 116.49718532562257]
]
const polygon = L.polygon(latlngs, {
  color: 'red',
  weight: 3, // 线宽
  opacity: 0.5, // 透明度
  fill: true, // 是否填充
  fillColor: '#f03', // 填充颜色
  fillOpacity: 0.2, // 填充透明度
}).addTo(map)
```

### Rectangle 矩形

一个用于在地图上绘制矩形覆盖物的类
```js
const bounds = [
  [39.91714508041264, 116.49718532562257],
  [39.98714508041264, 116.39718532562257]
]
const rectangle = L.rectangle(bounds, {
  color: '#f03',
  weight: 3,
  opacity: 0.5,
  fill: true,
  fillColor: '#f03',
  fillOpacity: 0.2,
  clickable: true, // 可点击
}).addTo(map)
```


### Circle 圆形
一个用于在地图上绘制圆形覆盖物的类
```js
const circle = L.circle([39.91714508041264, 116.49718532562257], {
  radius: 500,
  color: '#f03',
  weight: 3,
  opacity: 0.5,
  fill: true,
  fillColor: '#f03',
  fillOpacity: 0.2,
  clickable: true, // 可点击
}).addTo(map)
```

### CircleMarker 圆形标记
```js
// CircleMarker 圆形标记
const circleMarker = L.circleMarker([39.91714508041264, 116.49718532562257], {
  radius: 50,
  color: '#f03',
  weight: 3,
  opacity: 0.5,
  fill: true,
  fillColor: '#f03',
  fillOpacity: 0.2,
  clickable: true, // 可点击
}).addTo(map)
```


```js
// SVG 矢量渲染器
const center = [39.91714508041264, 116.49718532562257];
const coordinates = [
  [39.91714508041264, 116.49718532562257],
  [39.98714508041264, 116.39718532562257]
]
const myRenderer = L.svg({ padding: 5 }); // 自定义渲染器
const line = L.polyline( coordinates, { renderer: myRenderer }).addTo(map);
const circle = L.circle( center, {
  renderer: myRenderer,
  radius: 1000,
  color: '#f03',
  weight: 3,
  opacity: 0.5,
  fill: true,
  fillColor: '#f03',
  fillOpacity: 0.2,
} ).addTo(map);
```


## 基本类型

### LatLng
```js
var latlng = L.latLng(50.5, 30.5);
```

所有接受 LatLng 对象的 Leaflet 方法也接受它们的简单数组形式和简单对象形式（除非另有说明），所以这些行是等价的

```js
map.panTo([50, 30]);
map.panTo({lng: 30, lat: 50});
map.panTo({lat: 50, lng: 30});
map.panTo(L.latLng(50, 30));
```

### LatLngBounds 经纬度边界

```js
const corner1 = L.latLng(40.712, -74.227),
corner2 = L.latLng(40.774, -74.125),
bounds = L.latLngBounds(corner1, corner2);
```

### point

代表一个点，其 `x` 和 `y` 坐标为像素。
```js
var point = L.point(200, 300);
```

创建的是一个 像素坐标点 ，而不是地理坐标点。这个点表示的是：
- x 坐标：200像素（从左边缘向右200像素）
- y 坐标：300像素（从上边缘向下300像素）


### bounds

```js
// 创建Bounds对象
const point1 = L.point(100, 200); // 左上角
const point2 = L.point(300, 400); // 右下角
const bounds = L.bounds(point1, point2);
```

- 使用 L.Bounds 处理像素坐标的矩形区域
- 使用 L.LatLngBounds 处理地理坐标的矩形区域
- 两者都支持扩展、包含检查等操作，但坐标系不同

### Icon 图标

```js
const icon = L.icon({
  iconUrl: '/leaflet/images/marker-icon.png',
  iconRetinaUrl: '/leaflet/images/marker-icon-2x.png',
  iconSize: [25, 41],
  iconAnchor: [12, 41],
  popupAnchor: [1, -34],
  shadowUrl: '/leaflet/images/marker-shadow.png',
  shadowSize: [50, 50]
})
const marker = L.marker([39.91714508041264, 116.39718532562257], { icon }).addTo(map)
```

### divicon

L.DivIcon 是 Leaflet 中用于创建自定义 HTML 标记图标的类。它允许你使用 HTML 和 CSS 来创建完全自定义的标记图标

```js
const myIcon = L.divIcon({
  className: 'custom-div-icon', // 自定义 CSS 类
  html: '<div style="background-color: #f03; width: 30px; height: 30px; border-radius: 50%; text-align: center; line-height: 30px; color: white;">1</div>',
  iconSize: [30, 30],          // 图标大小
  iconAnchor: [15, 15],        // 图标锚点
  popupAnchor: [0, -15]        // 弹出窗口锚点
});

// 使用自定义图标创建标记
const marker = L.marker([39.917145, 116.397185], { icon: myIcon }).addTo(map);

// 添加 CSS 样式
const style = document.createElement('style');
style.innerHTML = `
.custom-div-icon {
  background: transparent;
  border: none;
}
`;
document.head.appendChild(style);
```


## 控件

### zoom 缩放
L.control.zoom 是 Leaflet 中用于添加缩放控件的类。默认情况下，Leaflet 会自动添加缩放控件，但你可以自定义它的位置和样式

```js
// 在初始化地图后添加自定义缩放控件
const zoomControl = L.control.zoom({
  position: 'bottomright', // 控件位置
  zoomInText: '➕',         // 放大按钮文本
  zoomOutText: '➖',        // 缩小按钮文本
  zoomInTitle: '放大',      // 放大按钮提示
  zoomOutTitle: '缩小'      // 缩小按钮提示
}).addTo(map);
```

如果你想移除默认的缩放控件，可以在初始化地图时设置

```js
const map = L.map('carrot-map', {
  zoomControl: false  // 禁用默认缩放控件
}).setView([39.91714508041264, 116.39718532562257], 14);
```

### attributton
L.control.attribution 是 Leaflet 中用于添加地图版权信息的控件。默认情况下，Leaflet 会自动添加版权信息，但你可以自定义它的内容和位置

```js
// 在初始化地图后添加自定义版权信息控件
const attributionControl = L.control.attribution({
  position: 'bottomleft', // 控件位置
  prefix: '地图数据 © '      // 前缀文本
}).addTo(map);

// 添加版权信息
attributionControl.addAttribution('高德地图');
attributionControl.addAttribution('OpenStreetMap');
```

移除默认的版权信息控件

```js
const map = L.map('carrot-map', {
  attributionControl: false  // 禁用默认版权信息控件
}).setView([39.91714508041264, 116.39718532562257], 14);
```
### layers 图层

L.control.layers 是 Leaflet 中用于添加图层切换控件的类。它允许用户在地图的不同图层之间进行切换。

```js
// 定义基础图层
const baseLayers = {
  '卫星图': Layer,
  '地名路网图': layer1,
  '组合': L.layerGroup([Layer, layer1]),
};

// 定义叠加图层（可选）
const overlays = {
  '标记': marker,
  '圆形': circle
};

// 添加图层切换控件
L.control.layers(
  baseLayers,  // 基础图层
  overlays,    // 叠加图层
  {
    collapsed: false,  // 控件是否折叠
    position: 'topright'  // 控件位置
  }
).addTo(map);
```

### scale
L.control.scale() 是 Leaflet 中用于添加比例尺控件的类。它可以帮助用户直观地了解地图上的距离。

```js
// 添加比例尺控件
L.control.scale({
  position: 'bottomright',  // 控件位置
  maxWidth: 200,            // 最大宽度
  metric: true,             // 是否显示公制单位
  imperial: false,          // 是否显示英制单位
  updateWhenIdle: true      // 是否在缩放结束后更新
}).addTo(map);
```

## 常用方法
### setView
用指定的动画选项设置地图的视图（地理中心和缩放）。
```js
// map为id名字,setView参数1: 地图中心坐标位置  参数2: 地图加载级别(数字越大,地图加载越近) 
const map = L.map('carrot-map').setView([39.91714508041264, 116.39718532562257], 14)
```

### setZoom

```js
map.setZoom(14)
```

### fitBounds
在 Leaflet 中， fitBounds 方法用于将地图视图调整到包含指定边界的最佳缩放级别。这个方法非常适合当你有一组坐标点，想要让地图自动调整到能够显示所有这些点的最佳视图。
```js
const options = {
  // 边界
  padding: [0, 0],
  // 最大层级
  maxZoom: 10,
  // 启用动画
  animate: true
}
const bounds = [[24.5, 125.7], [26.1, 126.8]]
map.fitBounds(bounds, options)
```

padding 参数用于在边界周围添加额外的空间，单位是像素。 `[150, 150]` 表示在水平和垂直方向各添加 150 像素的 padding

### panTo

用于平滑地将地图平移到指定的中心点,与 setView 不同， panto 会以动画的方式移动地图，而不是直接跳转到目标位置。

```js
// 使用 panto 平滑移动到指定位置
const targetPosition = [39.91714508041264, 116.39718532562257]; // 目标经纬度
map.panTo(targetPosition);
```
### locate
locate 方法用于获取用户的当前位置，并将地图视图定位到该位置

```js
// 使用 locate 方法定位用户位置
map.locate({ 
  setView: true, // 自动将地图视图定位到用户位置
  maxZoom: 14,   // 最大缩放级别
  enableHighAccuracy: true // 提高定位精度
});

// 监听定位成功事件
map.on('locationfound', function(e) {
  console.log('找到位置:', e.latlng);
  // 在用户位置添加标记
  L.marker(e.latlng).addTo(map)
    .bindPopup("您的位置").openPopup();
});

// 监听定位失败事件
map.on('locationerror', function(e) {
  console.error('定位失败:', e.message);
  alert('无法获取您的位置: ' + e.message);
});
```

addLayer 添加图层到地图上

addTo 将图层添加到指定的地图或图层组（LayerGroup）。

### 清除图层方法

removeLayer 用于从地图上移除指定的图层
```js
map.removeLayer(layer);
```

clearLayers 用于清除图层组中的所有图层

```js
layerGroup.clearLayers();
```

eachLayer + removeLayer
```js
// 遍历并移除所有图层
map.eachLayer(function(layer) {
  map.removeLayer(layer);
});
```

移除所有图层并保留底图

```js
// ... existing code ...

// 移除所有图层并保留底图
map.eachLayer(function(layer) {
  if (!layer._url) { // 底图通常有 _url 属性
    map.removeLayer(layer);
  }
});

// ... existing code ...
```