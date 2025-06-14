| 分类           | 标签/属性              | 说明                    | 示例/备注                                       |
| ------------ | ------------------ | --------------------- | ------------------------------------------- |
| **基础结构**     | `<table>`          | 定义表格容器                | 所有表格内容必须包含在此标签内                             |
|              | `<tr>`             | 定义表格行（Table Row）      | 每行可包含多个单元格                                  |
|              | `<td>`             | 定义标准单元格（Table Data）   | 默认左对齐，常规内容容器                                |
|              | `<th>`             | 定义表头单元格（Table Header） | **加粗居中**，常用于首行/首列                           |
| **高级结构**     | `<thead>`          | 定义表头区域                | 包含标题行（`<th>`），可打印时重复出现                      |
|              | `<tbody>`          | 定义表格主体                | 包含主要数据（`<td>`）                              |
|              | `<tfoot>`          | 定义表脚区域                | 常用于汇总行                                      |
|              | `<caption>`        | 表格标题                  | 显示在表格上方，描述表格内容                              |
| **布局属性**     | `colspan`          | 单元格横向合并列数             | `<td colspan="2">占两列</td>`                  |
|              | `rowspan`          | 单元格纵向合并行数             | `<td rowspan="3">占三行</td>`                  |
| **样式属性**     | `border`           | 表格边框粗细                | `border="1"`（已过时，建议用CSS替代）                  |
|              | `width` / `height` | 设置宽高                  | `width="100%"`（建议用CSS控制）                    |
|              | `cellpadding`      | 单元格内边距                | `cellpadding="10"`                          |
|              | `cellspacing`      | 单元格间距                 | `cellspacing="5"`                           |
| **语义化**      | `scope`            | 定义表头关联范围（提升可访问性）      | `scope="col"`（关联列） / `scope="row"`（关联行）     |
|              | `headers`          | 关联单元格到指定表头（复杂表格）      | `<td headers="name">...</td>`               |
| **CSS 关键样式** | `border-collapse`  | 合并边框（推荐）              | `border-collapse: collapse;`（消除双边框）         |
|              | `:nth-child()`     | 斑马纹效果                 | `tr:nth-child(even) {background: #f2f2f2;}` |
|              | `text-align`       | 内容对齐                  | `td { text-align: center; }`                |
|              | `vertical-align`   | 垂直对齐                  | `th { vertical-align: middle; }`            |

```html
<table border="1" style="width: 100%; border-collapse: collapse;">
  <caption>员工信息表</caption>
  <thead>
    <tr>
      <th>ID</th>
      <th>姓名</th>
      <th>部门</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>101</td>
      <td>张三</td>
      <td rowspan="2">技术部</td>
    </tr>
    <tr>
      <td>102</td>
      <td>李四</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="2">总人数</td>
      <td>2</td>
    </tr>
  </tfoot>
</table>
```

```css
table { overflow-x: auto; } /* 小屏幕横向滚动 */
```