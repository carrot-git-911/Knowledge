> [!tip] String 

## 创建字符串

```js
const s1 = 'primitive';          // 字面量
const s2 = String(123);          // "123"
const s3 = new String('object'); // String 对象（不推荐）

// ES6 模板字符串
const name = 'Alice';
const greeting = `Hello ${name}!`; 
```

### 字符串原始值和字符串对象

**自动装箱(Auto-Boxing)机制**
当对原始值调用方法时，JS 引擎会**临时创建包装对象**：

```js
const primitive = 'abc';
primitive.toUpperCase(); // 背后等价于：
// 1. 创建临时对象：new String(primitive)
// 2. 调用方法：tempObject.toUpperCase()
// 3. 销毁临时对象
```

**显式转换方法**
原始值 → 对象
```js
const primitive = 'text';
const obj = new String(primitive); // 显式转换
// 或 Object(primitive) 
```

对象 → 原始值
```js
const obj = new String('text');
const primitive = obj.valueOf(); // "text"（返回原始值）
// 或隐式转换：obj + "" → "text"
```
### String () 构造函数

String() 构造函数将创建 String 对象，当作为函数调用时，返回 String 类型的原始值
```js
const a = new String("Hello world"); // a === "Hello world" 为 false
const b = String("Hello world"); // b === "Hello world" 为 true
a instanceof String; // 为 true
b instanceof String; // 为 false
typeof a; // "object"
typeof b; // "string"
```

使用 String() 将 Symbol 转换为字符串
```js
const sym = Symbol("示例");
`${sym}`; // TypeError: Cannot convert a Symbol value to a string
"" + sym; // TypeError: Cannot convert a Symbol value to a string
"".concat(sym); // TypeError: Cannot convert a Symbol value to a string

const sym = Symbol("示例");
String(sym); // "Symbol(示例)"
```

## 访问字符

使用 chartAt
```js
"cat".charAt(1); // gives value "a"
```

将字符串视为类数组对象
```js
"cat"[1]; // gives value "a"
```

当使用方括号表示法进行字符串访问时，尝试删除或为其赋值的行为将不成功。涉及的属性既不可写（writable）也不可配置（configurable）

## 比较字符串

使用大于小于运算符比较

```js
const a = "a";
const b = "b";
if (a < b) {
  console.log('a<b')
}
```

注意，所有的比较运算符在比较字符串时都区分大小写。不区分大小写地比较字符串的常见方式是在比较它们之前将它们转为相同的大小写（大写或者小写）。

```js
function areEqualCaseInsensitive(str1, str2) {
  return str1.toUpperCase() === str2.toUpperCase();
}
```

## 实例属性

`String.prototype.length`

```js
'hello'.length // 5
```

## 实例方法

### 查询与访问

**`charAt(index)`**
返回指定索引的字符，索引超出范围时返回空字符串
```js
'JavaScript'.charAt(3); // "a"（索引从0开始）
'Test'.charAt(10);      // ""（越界返回空字符串）
```

**`charCodeAt(index)`**
返回指定索引字符的 Unicode 编码（UTF-16 码元）
```js
'A'.charCodeAt(0);      // 65（ASCII码）
'😀'.charCodeAt(0);     // 55357（UTF-16高位代理）
```

**`codePointAt(index)`**
返回指定索引字符的 Unicode 码点（支持代理对）
```js
'😀'.codePointAt(0);    // 128512（正确获取Unicode码点）
'a'.codePointAt(0);     // 97
```

**`indexOf(searchStr, fromIndex)`**
返回子字符串首次出现的索引，未找到返回 `-1`
```js
'apple'.indexOf('p');       // 1（首次出现位置）
'apple'.indexOf('p', 2);    // 2（从索引2开始查找）
'apple'.indexOf('z');       // -1（未找到）
```

**`lastIndexOf(searchStr, fromIndex)`**
返回子字符串最后一次出现的索引。
```js
'apple'.lastIndexOf('p');    // 2（最后出现位置）
'apple'.lastIndexOf('p', 1); // 1（在索引1之前查找）
```

### 截取与拼接

**`slice(start, end)`**
截取子字符串，支持负数索引（从末尾计算）
```js
'abcdef'.slice(2);     // "cdef"（从2到结尾）
'abcdef'.slice(2, 4);  // "cd"（包含2，不包含4）
'abcdef'.slice(-3);    // "def"（负数从末尾计算）
```

**`substring(start, end)`**
类似 `slice`，但负数参数视为 `0`，且自动交换参数顺序
```js
'abcdef'.substring(2, 4);  // "cd"（同slice）
'abcdef'.substring(4, 2);  // "cd"（自动交换参数）
'abcdef'.substring(-3);    // "abcdef"（负数视为0）
```

**`substr(start, length)`**（已废弃）
```js
'abcdef'.substr(2, 3);    // "cde"（从2开始取3个字符）
'abcdef'.substr(-3);      // "def"（负数从末尾计算）
```

**`concat(str1, str2, ...)`**
拼接多个字符串，等同于 `+` 操作符
```js
'Hello'.concat(' ', 'World');  // "Hello World"
// 等同于 'Hello' + ' ' + 'World'
```

### 大小写格式处理

**`toUpperCase()`**
转大写字母
```js
'Hello World'.toUpperCase();  // "HELLO WORLD"
'ß'.toUpperCase();            // "SS"（德语特殊处理）
```

**`toLowerCase()`**
转小写字母
```js
'HELLO WORLD'.toLowerCase();  // "hello world"
'İ'.toLowerCase();            // "i̇"（土耳其语特殊处理）
```

**`trim()`**
去除字符串两端的空白字符
```js
'  text  '.trim();          // "text"
'\t\n text \r'.trim();      // "text"
```

**`trimStart()` / `trimLeft()`**
去除开头的空白字符
```js
'  text  '.trimStart();     // "text  "
'\ttext'.trimLeft();        // "text"
```

**`trimEnd()` / `trimRight()`**
去除结尾的空白字符
```js
'  text  '.trimEnd();       // "  text"
'text\n'.trimRight();       // "text"
```

**`padStart(targetLength, padString)`**
在开头填充字符串至目标长度
```js
'5'.padStart(3, '0');       // "005"
'hi'.padStart(5, 'ab');     // "abahi"
```

**`padEnd(targetLength, padString)`**
在结尾填充字符串至目标长度
```js
'5'.padEnd(3, '0');        // "500"
'hi'.padEnd(5, 'ab');      // "hiaba"
```

### 包含性判断
**`includes(searchStr, position)`**
判断是否包含子字符串，返回布尔值
```js
'JavaScript'.includes('Script');  // true
'Hello'.includes('ello', 1);      // true（从位置1开始检查）
```

**`startsWith(searchStr, position)`**
判断是否以子字符串开头
```js
'Hello World'.startsWith('Hello');   // true
'Hello'.startsWith('ello', 1);       // true（从位置1开始检查）
```

**`endsWith(searchStr, position)`**
判断是否以子字符串结尾。
```js
'Hello World'.endsWith('World');    // true
'Hello'.endsWith('lo', 5);          // true（前5个字符结尾）
```
### 正则表达式相关
**`match(regexp)`**
返回正则表达式匹配的结果数组（无匹配返回 `null`）
```js
'2023-08-15'.match(/\d+/g);       // ["2023", "08", "15"]
'Hello'.match(/world/i);           // null（未匹配）
```

**`matchAll(regexp)`**
返回所有匹配的迭代器（正则需带 `g` 标志）
```js
const matches = [...'a1b2'.matchAll(/\d/g)];
matches.map(m => m[0]);            // ["1", "2"]
```

**`search(regexp)`**
返回首个匹配的索引，无匹配返回 `-1`
```js
'JavaScript'.search(/Script/);     // 4（匹配开始位置）
'Hello'.search(/world/);           // -1
```

**`replace(regexp|substr, newSubstr|function)`**
替换首个匹配的子字符串或正则匹配项
```js
'2023-08'.replace(/-/, '.');       // "2023.08"
'price: 99'.replace(/\d+/, n => +n+1); // "price: 100"
```

**`replaceAll(regexp|substr, newSubstr|function)`**
替换所有匹配的子字符串（使用字符串时需全局正则）
```js
'a-b-c'.replaceAll('-', '');       // "abc"
'1a2b3c'.replaceAll(/\d/g, '#');   // "#a#b#c"
```

### 分割与重复
**`split(separator, limit)`**
按分隔符分割字符串为数组
```js
'a,b,c'.split(',');          // ["a", "b", "c"]
'2023-08-15'.split(/-/, 2);  // ["2023", "08"]（限制返回数量）
```

**`repeat(count)`**
重复字符串指定次数。
```js
'a'.repeat(3);      // "aaa"
'ab'.repeat(2);     // "abab"
```

### 本地化处理
**`localeCompare(that, locales, options)`**
按本地排序规则比较字符串顺序，返回数值（负、0、正）。
```js
'ä'.localeCompare('z', 'de');    // -1（德语中 ä 排在 z 前）
'ä'.localeCompare('z', 'en');    // 1（英语中 ä 视为特殊字符）
```

### 其他方法
**`valueOf()`**
返回原始字符串值（对原始字符串无实际意义）
```js
const strObj = new String('test');
strObj.valueOf();   // "test"（返回原始值）
```
**`toString()`**
返回字符串本身，原始字符串调用时直接返回
```js
const strObj = new String('test');
strObj.toString();  // "test"（转换为原始字符串）
```

### 关键注意事项

1. **不可变性**：所有方法返回新字符串，原字符串不变。
2. **参数处理**：如 `slice` 支持负数，`substring` 自动交换参数。
3. **正则标志**：`matchAll` 和 `replaceAll` 需正则带 `g` 标志。
4. **兼容性**：`replaceAll` 和 `trimStart`/`trimEnd` 需 ES6+ 支持。
5. **性能优化**：避免在循环中频繁调用方法（如 `split`、`replace`）。

### 类型判断陷阱

```js
const objStr = new String('test')

console.log(typeof objStr) // "object"
console.log(objStr instanceof String);  // true
console.log(objStr instanceof Object); // true
console.log('test' instanceof String); // false❗
```

隐式转换
```js
'5' + 3  // '53'（优先字符串连接）
'5' - 2  // 3（转换为数字） 
```

多行字符串
```js
// Bad（依赖行尾反斜杠）
const bad = 'line1\
line2';

// Good（使用模板字符串）
const good = `line1
line2`;
```

空值处理
```js
String(null)         // 'null'
String(undefined)   // 'undefined'
```