## 基础元数据

### 字符编码声明

```html
<meta charset="UTF-8">
```

- 定义文档的字符编码
- 放在 head 的最前面

视口设置（响应式必备）

```html
<meta name="viewport" content="width=device-width initial-scale=1.0">
```

`width` 控制视口的宽度
- `width=device-width`：视口宽度等于设备宽度
- `width=600`：设置固定宽度为600像素

`initial-scale` 初始缩放比例
- `initial-scale=1.0` 不缩放，1:1显示
- `initial-scale=2.0` 初始放大2倍

`minimum-scale` 允许的最小缩放比例
- `minimum-scale=0.5`：最小可缩小至50%

`maximum-scale` 允许的最大缩放比例
- `maximum-scale=2.0`：最大可放大至200%

`user-scalable` 是否允许用户缩放
- `user-scalable=yes`：允许缩放（默认）
- `user-scalable=no`：禁止缩放

`viewport-fit` 控制全屏显示行为（iOS特有）

- `viewport-fit=cover`：内容延伸到整个屏幕
- `viewport-fit=contain`：内容适应屏幕

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=2.0, user-scalable=yes">
```


## SEO 优化

页面描述

- 提供网页内容的简短描述
- 搜索引擎常在搜索结果中显示此描述

```html
<meta name="description" content="这是一个关于HTML meta标签的详细指南">
```


关键词

- 为搜索引擎提供关键词
- 现代搜索引擎对此权重已降低

```html
<meta name="keywords" content="HTML, meta标签, 前端开发, SEO">
```


作者信息和版权信息

```html
<meta name="author" content="张三">
<meta name="copyright" content="© 2023 某某公司">
```

搜索引擎索引控制（robots）

控制搜索引擎爬虫行为

```html
<meta name="robots" content="noindex, nofollow"> <!-- 禁止收录和跟踪链接 -->
```

针对特定的搜索引擎
```html
<meta name="googlebot" content="指令1,指令2">  <!-- 仅对Google有效 -->
<meta name="bingbot" content="指令1,指令2">    <!-- 仅对Bing有效 -->
```

`all`：文件将被检索，且页面上的链接可以被查询；
`none`：文件将不被检索，且页面上的链接不可以被查询；

`index`: 允许搜索引擎索引此页面（默认值）
`noindex`: 阻止搜索引擎索引此页面

`follow` 允许搜索引擎跟踪此页面上的链接
`nofollow` 阻止搜索引擎跟踪此页面上的链接

`imageindex` 允许索引页面上的图片
`noimageindex` 阻止索引页面上的图片

`max-image-preview:[setting]`
- 控制搜索结果中图片预览的显示方式
- 可选值：`none`, `standard`, `large`

`max-video-preview:[n]`
- 设置视频预览的最大秒数
## 移动端优化

禁止自动识别
防止电话号码/邮箱被自动识别为链接

```html
<meta name="format-detection" content="telephone=no, email=no">
```

ios WebApp 设置
全屏模式

```html
<meta name="apple-mobile-web-app-capable" content="yes">
```

状态栏样式
```html
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
```

主题颜色

```html
<meta name="theme-color" content="#4285f4">
```


## 浏览器兼容与行为

IE 渲染模式
强制使用最新引擎
```html
<meta http-equiv="X-UA-Comatible" content="IE=edge">
```

HTTP 缓存控制
禁用缓存（优先通过服务器设置）
```html
<meta http-equiv="Cache-Control" content="no-cache">
```

自动刷新/重定向

```html
<meta http-equiv="refresh" content="5; url=https://example.com">
```


## 社交媒体优化


Facebook/OpenGraph 协议
控制分享时的标题、描述、图片等（Facebook 等平台）
```html
<meta property="og:title" content="页面标题">
<meta property="og:description" content="页面描述">
<meta property="og:type" content="website">
<meta property="og:url" content="https://example.com">
<meta property="og:image" content="https://example.com/image.jpg">
```

Twitter 卡片
优化 Twitter 分享显示
```html
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="页面标题">
<meta name="twitter:description" content="页面描述">
<meta name="twitter:image" content="https://example.com/image.jpg">
```


## 示例

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="description" content="学习HTML meta标签的完整指南">
    <meta name="keywords" content="HTML, meta标签, 网页开发">
    <meta name="author" content="李四">
    <meta name="robots" content="index,follow">
    
    <!-- Open Graph -->
    <meta property="og:title" content="HTML meta标签详解">
    <meta property="og:description" content="学习HTML meta标签的完整指南">
    <meta property="og:image" content="https://example.com/image.jpg">
    <meta property="og:url" content="https://example.com/meta-tags">
    <meta property="og:type" content="article">
    
    <title>HTML meta标签详解</title>
</head>
<body>
    <!-- 页面内容 -->
</body>
</html>
```