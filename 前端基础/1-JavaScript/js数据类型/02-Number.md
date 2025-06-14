> [!info] JavaScript 只有 `Number` 类型，没有独立的整数或浮点数类型。所有数值均以双精度浮点数形式存储。JavaScript 的 Number 类型是一个双精度64位二进制格式 IEEE754值

## IEEE 754标准

IEEE 754 双精度浮点数使用 64 位来表示 3 个部分：
- 1 位用于表示符号（sign）（正数或者负数）
- 11 位用于表示指数（exponent）（-1022 到 1023）
- 52位用于表示尾数（mantissa）（表示0和1之间的数值）

![[file-pasted-20250312002537984.png]]

**指数偏移**
IEEE 754 标准中，指数位的实际值并非直接存储，而是通过 `偏移二进制表示`（Bias Encoding）处理。
偏移值 1023
- 存储的指数值为 `1000`（二进制），对应十进制值为 `1000 - 1023 = -23`。
- 存储的指数值为 `2046`（二进制），对应十进制值为 `2046 - 1023 = 1023`。


## Number 强制转换
Number将按原样返回
undefined 转换为 NaN
null 转换为 0
BigInt 抛出 TypeError
Symbol 抛出 TypeError

构造函数

## 静态方法

`Number.isFinite(value)`

用途：判断传入值是否是一个有限数（排除 `Infinity`、`-Infinity` 和 `NaN`）。
示例：
```js
Number.isFinite(123);       // true
Number.isFinite(Infinity);  // false
Number.isFinite("123");     // false（非数值类型）
```

<mark style="background: #BBFABBA6;">Number.isFinite 和 全局 isFinite</mark>

与全局 isFinite 函数相比 此方法不会先将参数转换为数字，这意味着只有类型为数字且为有限数的值才返回 `true`，而非数字的值始终返回 `false`。

```js
isFinite("0"); // true；强制转换为数字 0
Number.isFinite("0"); // false
isFinite(null); // true；强制转换为数字 0
Number.isFinite(null); // false
```

`Number.isInteger(value)`

判断值是否为整数（忽略小数点后的零）
```js
Number.isInteger(5);        // true
Number.isInteger(5.0);      // true
Number.isInteger(5.1);      // false
Number.isInteger("5");      // false（非数值类型）
```

`Number.isNaN(value)`

严格判断值是否为 `NaN`（仅当值为 `NaN` 时返回 `true`）。
```js
Number.isNaN(NaN);          // true
Number.isNaN("NaN");        // false（字符串非NaN）
isNaN("123abc");            // true（全局方法会转换失败）
```

`Number.isSafeInteger(value)`

判断值是否为 **安全整数**（在 `-2^53 + 1` 到 `2^53 - 1` 范围内）（±9,007,199,254,740,991）
```js
Number.isSafeInteger(9007199254740991);  // true（最大安全整数）
Number.isSafeInteger(9007199254740992);  // false（超出安全范围）
Number.isSafeInteger(3.1); // false
Number.isSafeInteger(2 ** 53 - 1); // true
Number.isSafeInteger(NaN); // false
Number.isSafeInteger(Infinity); // false
Number.isSafeInteger("3"); // false
```


`Number.parseFloat`
解析参数并返回浮点数。如果无法从参数中解析出一个数字，则返回 NaN
```js
Number.parseFloat("3.14");   // 3.14
Number.parseFloat("3.14abc");// 3.14（忽略非数字部分）
```

`Number.parseInt(string,radix)`
静态方法解析一个字符串参数并返回一个指定基数的整数。
```js
Number.parseInt("1010", 2);  // 10（二进制解析）
Number.parseInt("0xA");      // 10（自动识别十六进制）
```

## 静态属性

`Number.MAX_SAFE_INTEGER`
最大的安全整数（2^53 – 1）。
9007199254740991（2^53-1）
`Number.MIN_SAFE_INTEGER`
最小安全整数 -9007199254740991
`Number.MAX_VALUE`
最大正数 ≈1.7976931348623157e+308
`Number.MIN_VALUE`
最接近 0 的正数（非最小负数） ≈5e-324

## 实例方法

### 数值格式化方法

**`toFixed(digits)`**

用途:将数值转换为**字符串**,保留指定位数的小数(四舍五入)。
参数:digits, 应该是一个介于 `0` 和 `100` 之间的值，包括 `0` 和 `100`。如果这个参数被省略，则被视为 `0`
示例:
```js
(123.456).toFixed(2);    // "123.46"  
(10).toFixed(2);         // "10.00"  
(Math.PI).toFixed(0);    // "3"  
```

如果需要截断，则将数字四舍五入；如果小数位数不足，则小数部分用零填充，以使其具有指定长度。
对负数使用 toFixed 对成员的访问优先级高于一元减号
```js
-2.34.toFixed(1); // -2.3，数字
(-2.34).toFixed(1); // '-2.3'
```

**`toExponential(fractionDigits)`**

返回一个以指数表示法表示该数字的字符串
参数 0和100之间（包含两端
```js
toExponential()
toExponential(fractionDigits)

fractionDigits
可选。一个整数，用来指定小数点后有几位数字。默认设置为完整表示该数字所需要的数字。
(12345).toExponential(2);    // "1.23e+4"  
(0.123).toExponential(1);    // "1.2e-1"  
```

**异常**
	`RangeError`
	fractionDigits 不是介于0和100之间（包含两端）的整数，则抛出该错误
	`TypeError`
	在非 Number 对象上调用该方法，则抛出该错误。


**`toPrecision(precision)`**

返回一个已指定精度表示该数字的字符串，该字符串四舍五入到 `precision` 个有效数字
precision 一个指定有效位数的整数。默认全部有效位数

```js
(123.456).toPrecision(4);    // "123.5"  
(0.123).toPrecision(2);      // "0.12"  
(12345).toPrecision(2);      // "1.2e+4"  

// 请注意，在某些情况下可能会返回指数表示法字符串
console.log((1234.5).toPrecision(2)); // 输出 '1.2e+3'
```

### 类型转换与本地化

`toString(radix)`

返回表示该数字值的字符串
参数 radix 一个整数，范围在 `2` 到 `36` 之间，用于指定表示数字值的基数。默认为 10。
示例
```js
(15).toString(16);     // "f"  
(255).toString(2);     // "11111111"  
(3.14).toString();     // "3.14"  
(-10).toString(2)      // -1010
// 负数会保留符号（如 `(-10).toString(2)` 返回 `"-1010"`）。
```

Number 对象重写了 Object 的 toString 方法，不会继承 Object.prototype.toString(),对于 `Number` 值，`toString` 方法返回数字值指定基数的字符串表示。

0和-0都以"0"作为其字符串表示。Infinity 返回"Infinity",而而 NaN 返回"NaN"

`toLocaleString([locales[, options]])`

返回这个数字在特定语言环境表示的字符串
参数
locales :语言代码(如"en-US"、"zh-CN")。
options:格式化配置(如 style:"currency"、currency:"USD)。

```js
(1234567.89).toLocaleString("zh-CN");   // "1,234,567.89"（中文环境）

(1234.56).toLocaleString("en-US", { 
  style: "currency", 
  currency: "USD" 
}); // "$1,234.56"  

// 显示百分比
(0.123).toLocaleString("en-US", { 
  style: "percent", 
  minimumFractionDigits: 2 
}); // "12.30%"

// 自定义小数位和分组
(123456.789).toLocaleString("de-DE", { 
  minimumFractionDigits: 3, 
  useGrouping: false 
}); // "123456,789"  
```

### 其他实例方法

**`valueOf`**
返回 `Number` 对象的原始数值
该方法通常由 JavaScript 在内部调用，而非在 Web 代码中显式调用。
示例
```js
const numObj = new Number(10)
console.log(typeof numObj) // object

const num = numObj.valueOf()
console.log(num) // 10
console.log(typeof num) // number
```

## 四舍五入规则

方法如 toFixed、toPrecision 遵循"银行家舍入法"(四合舍六入五取偶),可能导致预期外的结果
```js
(2.55).toFixed(1);    // "2.5"（而非 "2.6"）  
(1.255).toFixed(2);   // "1.25"（而非 "1.26"）  
```


## 常见陷阱

- **误用赋值运算符**：`if (x = 5)` 应改为 `if (x === 5)`。
- **对象包装陷阱**：避免 `new Boolean()`，直接使用字面量。
- **0 或空字符串误判**
```js
// 错误：count 为 0 时会误判
if (count) { /* ... */ }
// 正确：显式检查
if (count !== 0) { /* ... */ }
```
- **短路运算的返回值**：`&&` 返回第一个 falsy 值，`||` 返回第一个 truthy 值。

## Math

#### random
Math.random()：生成 0~1 之间的随机数（含0不含1）
```js
console.log(Math.random()); // 例如：0.5486354912
```
#### round
Math.round()：四舍五入取整
```js
console.log(Math.ceil(3.1));   // 4
console.log(Math.ceil(-3.9));  // -3
```
#### ceil
Math.ceil()：向上取整
```js
console.log(Math.ceil(3.1));   // 4
console.log(Math.ceil(-3.9));  // -3
```
#### floor
Math.floor()：向下取整
```js
console.log(Math.floor(3.9));  // 3
console.log(Math.floor(-3.1)); // -4
```
#### abs
Math.abs()：取绝对值
```js
console.log(Math.abs(-5));     // 5
console.log(Math.abs(3.5));    // 3.5
```
#### sqrt
Math.sqrt()：求平方根
```js
console.log(Math.sqrt(25));    // 5
console.log(Math.sqrt(3));     // ≈1.732
console.log(Math.sqrt(-1));    // NaN（负数平方根无效）
```
#### pow
* 语法: Math.pow(基数, 幂)
* 作用: 求一个基数的 X 次幂
```js
console.log(Math.pow(2, 3));   // 8（2的3次方）
console.log(Math.pow(4, 0.5)); // 2（等价于平方根）
```
#### max
* 语法: Math.max(数据1, 数据2, 数据3, ...)
* 作用: 求参数中 的 最大值
```js
console.log(Math.max(1, 5, 3)); // 5
console.log(Math.max(-1, -5));  // -1
```
#### min
* 语法: Math.min(数据1, 数据2, 数据3, ...)
* 作用: 求参数中 的 最小值
```js
console.log(Math.min(1, 5, 3)); // 1
console.log(Math.min(-1, -5));  // -5
```
#### PI
Math.PI：圆周率常量
```js
console.log(Math.PI); // ≈3.141592653589793
```

#### 注意点

**负数取整**
向上取整(ceil)时,-3.9→-3(向数轴正方向取整);向下取整(floor)时,-3.1→-4(向数轴负方向取整)。

**平方根限制**
Math.sqrt(-1)会返回 NaN,因为负数没有实数平方根。

**幂运算灵活性**
Math.pow(4,0.5)等效于计算平方根,可用于替代 sqrt。

**参数处理**
max 和 min 方法不接受数组参数,但可通过展开运算符处理数组
```js
const nums = [1, 5, 3];
console.log(Math.max(...nums)); // 5
```