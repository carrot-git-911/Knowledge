---
日期: 2024-11-24T20:22:00
---

### 什么是 Markdown

1. Markdown 是一款轻量级笔记语言，不同于 HTML (**Hypertext Markup Language**),Markdown 语法非常简单
2. **Markdown**以 **纯文本格式**编写文档，依赖键盘而非鼠标，专注于**写作本身**，感受**书写**的魅力
3. **Markdown**的通过添加一些简单的**标识符**，让文本具有**恰到好处**的格式
4. **Markdown**核心特征就是**简扼**+**精炼**

### 标题

```
# 这是一级标题
## 这是二级标题
### 这是三级标题
#### 这是四级标题
##### 这是五级标题
###### 这是六级标题
```

### 段落

要创建段落，请使用空白行将一行或多行文本进行分隔。 不要用空格（spaces）或制表符（ tabs）缩进段落。

```
I really like using Markdown.

I think I'll use it to format all of my documents from now on.
```

> [!info]
> 首行缩进两个字符有个历史原因，由于以前打印纸张很贵，首行缩进两个字符可以清晰的分段。而现在通过空一行的方式，是一种更优雅的分段方式。而 Markdown 就采取的这种方式

段落换行：几乎每个 Markdown 应用程序都支持两个或多个空格进行换行，称为 `结尾空格（trailing whitespace)` 的方式，但这是有争议的，因为很难在编辑器中直接看到空格，并且很多人在每个句子后面都会有意或无意地添加两个空格。由于这个原因，你可能要使用除结尾空格以外的其它方式来换行。幸运的是，几乎每个 Markdown 应用程序都支持另一种换行方式：HTML 的 `<br>` 标签。

为了兼容性，请在行尾添加“结尾空格”或 HTML 的  `<br>`  标签来实现换行。最佳实践是，**段落内不换行**。

### 文字样式

#### 加粗
I just love **bold text**.
I just love __bold text__.
Love **is** bold
快捷键通常为：Ctrl + B

#### 斜体
Italicized text is the *cat's meow*.
Italicized text is the _cat's meow_.
A *cat* meow
快捷键通常为：Ctrl + I

### 引用

#### 创建块引用

要创建块引用，请在段落前添加一个 `>` 符号。
**>**+文本内容 （**不需要空格**)

> Dorothy followed her through many of the beautiful rooms in her castle.

#### 多个段落的块引用
块引用可以包含多个段落。为段落之间的空白行添加一个 `>` 符号。

> Dorothy followed her through many of the beautiful rooms in her castle.
>
> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

#### 嵌套块引用
块引用可以嵌套。在要嵌套的段落前添加一个  `>>`  符号。

> Dorothy followed her through many of the beautiful rooms in her castle.
>
>> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.


### 列表

列表可嵌套其它元素，包括代码块，图片等

#### 有序列表
要创建有序列表，请在每个列表项前添加数字并紧跟一个英文句点。数字不必按数学顺序排列，但是列表应当以数字 1 起始。
```
1. First item
2. Second item
3. Third item
4. Fourth item

1. First item
1. Second item
1. Third item
1. Fourth ite

1. First item
8. Second item
3. Third item
5. Fourth item

1. First item
2. Second item
3. Third item
    1. Indented item
    2. Indented item
4. Fourth item
```



#### 无序列表
要创建无序列表，请在每个列表项前面添加破折号 (-)、星号 (`*`) 或加号 (+) 。缩进一个或多个列表项可创建嵌套列表。

```
- First item
- Second item
- Third item
- Fourth item

* First item
* Second item
* Third item
* Fourth item

+ First item
+ Second item
+ Third item
+ Fourth item

- First item
- Second item
- Third item
    - Indented item
    - Indented item
- Fourth item
```

### 代码及代码块

Use `code` in your Markdown file.

```
示例
```

### 分割线删除线

`---`
`***`
`___`
~~世界是平坦的。~~ 我们现在知道世界是圆的。

### 链接

#### 链接书写

链接文本放在中括号内，链接地址放在后面的括号中，链接 title 可选。
超链接 Markdown 语法代码：`[超链接显示名](超链接地址 "超链接title")`
对应的 HTML 代码：`<a href="超链接地址" title="超链接title">超链接显示名</a>`
这是一个链接 [Markdown语法](https://markdown.com.cn)。

#### 链接的title

链接 title 是当鼠标悬停在链接上时会出现的文字，这个 title 是可选的，它放在圆括号中链接地址后面，跟链接地址之间以空格分隔。

```
这是一个链接 [Markdown语法](https://markdown.com.cn "最好的markdown教程")。
```

这是一个链接 [Markdown语法]( https://markdown.com.cn "最好的 markdown 教程")。

#### 网址和 Email 地址

使用尖括号可以很方便地把 URL 或者 email 地址变成可点击的链接

```
<https://markdown.com.cn>
<fake@example.com>
```

<https://markdown.com.cn>
<fake@example.com>

#### 带格式的链接

强调链接, 在链接语法前后增加星号。 要将链接表示为代码，请在方括号中添加反引号。

```
I love supporting the **[EFF](https://eff.org)**.
This is the *[Markdown Guide](https://www.markdownguide.org)*.
See the section on [`code`](#code).
```

渲染效果：

I love supporting the **[EFF](https://eff.org)**.
This is the *[Markdown Guide](https://www.markdownguide.org)*.
See the section on [`code`](#code).

### 图片

要添加图片，请使用感叹号 (`!`), 然后在方括号增加替代文本，图片链接放在圆括号里，括号里的链接后可以增加一个可选的图片标题文本。

插入图片 Markdown 语法代码：`![图片alt](图片链接 "图片title")`。

对应的 HTML 代码：`<img src="图片链接" alt="图片alt" title="图片title">`

```
![这是图片](/assets/img/philly-magic-garden.jpg "Magic Gardens")
```


iframe 方式

### 任务列表

任务列表使您可以创建带有复选框的项目列表。在支持任务列表的 Markdown 应用程序中，复选框将显示在内容旁边。要创建任务列表，请在任务列表项之前添加破折号 - 和方括号 [ ]，并在 [ ] 前面加上空格。要选择一个复选框，请在方括号 [x] 之间添加 x 。

```
- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media
```

- [x] Write the press release
- [x] Update the website  [completion:: 2024-12-30]
- [x] Contact the media  [completion:: 2024-12-30]

- **任务列表也是可以缩进 + 退格的，操作跟 无序列表、有序列表一样**

### 表格

#### 创建表格

要添加表，请使用三个或多个连字符（`---`）创建每列的标题，并使用管道（`|`）分隔每列。您可以选择在表的任一端添加管道。

```
| 行/列 | 列名2 | 列明3 |
| ----- | ----- | ----- |
| 行名1 |       |       |
| 行名2 |       |       |
| 行名3 |       |       |
```

| 行/列 | 列名2 | 列明3 |
| --- | --- | --- |
| 行名1 |     |     |
| 行名2 |     |     |
| 行名3 |     |     |

单元格宽度可以变化，如下所示。呈现的输出将看起来相同。
```
| Syntax | Description |
| --- | ----------- |
| Header | Title |
| Paragraph | Text |
```

| Syntax    | Description |
| --------- | ----------- |
| Header    | Title       |
| Paragraph | Text        |

#### 表格内容对齐

您可以通过在标题行中的连字符的左侧，右侧或两侧添加冒号（`:`），将列中的文本对齐到左侧，右侧或中心。

```
| Syntax      | Description | Test Text     |
| :---        |    :----:   |          ---: |
| Header      | Title       | Here's this   |
| Paragraph   | Text        | And more      |
```

| Syntax    | Description |   Test Text |
| :-------- | :---------: | ----------: |
| Header    |    Title    | Here's this |
| Paragraph |    Text     |    And more |


### HTML

几乎所有支持 Markdown 的地方都支持 HTML，HTML 可以理解为 Markdown 的超集，你可以做出任何炫酷的样式和排版。常用的包括在 Markdwon 中实现：

- 颜色：`<font color="red">红色文本</font>`
- 文本对齐： `<p style="text-align: right">右对齐文本</p>`
- 上下标：`10<sup>-6</sup>`，`H<sub>2</sub>O`
- 嵌入视频：`<iframe src="视频地址"/>`
- 第三方 api 嵌入：`<img src="https://contrib.rocks/image?repo=PKM-er/Pkmer-Docs"/>`
- 可合并的表格
- ...

### 实体字符

在 Markdown 中，字符  `<`、`>`、`"`、`'`  和反引号是特殊字符。它们是 Markdown 语法自身的一部分，那么你如何将这些字符包含进你的文本中呢? 一种方法是转义，即加斜杠 `\<`，另一种办法是使用实体字符即字符引用。

我们必须使用字符引用 —— 表示字符的特殊编码，它们可以在那些情况下使用。每个字符引用以符号&开始，以分号 (;) 结束。

| 原义字符          | 等价字符引用   |
| ------------- | -------- |
| <             | `&lt;`   |
| >             | `&gt;`   |
| "             | `&quot;` |
| '             | `&apos`  |
| &             | `&amp;`  |
| 版权符号，有问题展示不出来 | `&copy;` |
