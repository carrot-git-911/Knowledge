Dataview 的查询字段 Field 就是我们最后想要显示的内容组成的列表

- 字面常量 Literals；
- 查询的文件的元数据；
- 查询的文件的元数据和字面常量组合；
- 使用加减号将查询的文件的元数据和一些描述词拼接组合；

## 字面常量
dataview
table date(now)

## 文件的元数据

dataview
table file.name
limit 10

## 元数据和字面常量组合

dataview
table date(now) - file.ctime
limit 10

## 文件的元数据和一些描述词组合

`AS` 可以为属性重命名（查询创建天数最长的前十个文件）

dataview
table round((date(now) - file.ctime).day) AS "已经创建了（天）"
sort file.ctime
limit 10 

与 markdown 语法搭配

dataview
TABLE 
	"_" + publisher + "_" AS Publisher,
	"**" + developer + "**" AS Developer,
    "==" + price + "==" AS Price
FROM "10 Example Data/games"

这样我们就分别为三个属性增加了斜体、加粗和高亮

与 html 语法搭配

embed()  可以把链接嵌入查询结果中

这里也可以用 html 的语法来实现该功能（Cover 不是文件的隐式字段，是我们添加在 frontmatter 中的一个含有图片路径的属性，可以是本地图片的路径，也可以是在线链接）
```
dataview
table "<img src=\"" + cover + "\"/>" as Cover
from ...
```

还可以利用 Flatten 操作符来更好的实现以上操作

因为 Flatten 是将结果集扁平化，所以如果我们给输入值不是原本文件里的值时，不会对我们的结果集造成什么影响。他就可以作为一种中间值构造一些描述词；

为属性添加颜色（利用 Flatten 构造了三个描述词 greenStyle, styleEnd 和 rightAlignStyle）

```
dataview
TABLE greenStyle + author + styleEnd AS Author, 
	genres, 
	rightAlignStyle + totalPages + styleEnd AS "Total Pages"
FROM "10 Example Data/books"
FLATTEN "<span style='color: lightgreen;'>" AS greenStyle
FLATTEN "<span style='display:flex; justify-content: right;'>" AS rightAlignStyle
FLATTEN "</span>" AS styleEnd
```