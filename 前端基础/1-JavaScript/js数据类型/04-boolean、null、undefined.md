## boolean

**`Boolean`** 对象是一个布尔值的对象包装器
### 基本特性

- `boolean` 类型只有两个值：`true` 和 `false`。
- 通常用于条件判断和逻辑运算。

```js
let isActive = true;
let isCompleted = false;
```

### 布尔值的来源

布尔值通常由以下方式产生

**比较运算符**
```js
// == === > <
console.log(10 > 5); // 输出: true
console.log(10 === "10"); // 输出: false
```

**逻辑运算**
逻辑运算符（如 `&&`、`||`、`!`）返回布尔值
```js
console.log(true && false); // 输出: false
console.log(true || false); // 输出: true
console.log(!true); // 输出: false
```

条件判断
`if`、`while` 等语句中的条件表达式会隐式转换为布尔值。
```js
if (1) {
  console.log("This will run"); // 输出: This will run
}
```

### 隐式转换

在 JavaScript 中，许多值可以隐式转换为布尔值

**Falsy 值**
`false`, `0`, `""`, `null`, `undefined`, `NaN`

**Truthy 值**
其他所有值（包括 `"0"`, `" "`, `[]`, `{}`）。

### 显示转换

使用 `Boolean()` 或 `!!` 快速转换。
```js
const isValid = !!email; // 若 email 非空字符串，则为 true
```

### Boolean 对象

- `Boolean` 对象是 `boolean` 原始类型的包装对象。
- 通常不建议使用 `Boolean` 对象，而是直接使用原始值
```js
let boolObj = new Boolean(false);
if (boolObj) {
  console.log("This will run"); // 输出: This will run
}
```

### 实例方法

`Boolean.prototype.toString()`
```js
let bool = true;
console.log(bool.toString()); // 输出: "true"
```

`Boolean.prototype.valueOf()`
```js
let bool = new Boolean(false);
console.log(bool.valueOf()); // 输出: false
```

## null

- `null` 是一个原始值，表示“无”或“空”。
- 它是一个字面量，不是对象。

```js
let data = null;
console.log(data); // 输出: null
```

**null 的使用场景**
- *初始化变量*：当变量尚未赋值时，可以使用 `null` 初始化。
- *清空对象*：当不再需要某个对象时，可以将其设置为 `null`。
- *表示无值*：用于表示某个变量或属性没有值。

**null 的类型**

- `null` 的类型是 `object`，这是 JavaScript 的一个历史遗留问题。
```js
console.log(typeof null); // 输出: object
```

**null 的强制转换**

- 在布尔上下文中，`null` 被转换为 `false`。
- 在数值上下文中，`null` 被转换为 `0`。

## undefined

`undefined` 是全局对象_的一个属性。也就是说，它是全局作用域的一个变量

- `undefined` 是一个原始值，表示“未定义”。
- 它是一个全局对象的属性（在浏览器中是 `window.undefined`）
```js
let data;
console.log(data); // 输出: undefined
```


**undefined 使用场景**

- *变量未初始化*：变量声明但未赋值时，默认值为 `undefined`。
- *函数无返回值*：函数没有 `return` 语句时，默认返回 `undefined`。
- *对象属性不存在*：访问对象不存在的属性时，返回 `undefined`。
```js
let a; // 变量未初始化
console.log(a); // 输出: undefined

function foo() {} // 函数无返回值
console.log(foo()); // 输出: undefined

let obj = { name: "Alice" };
console.log(obj.age); // 输出: undefined
```

- `undefined` 的类型是 `undefined`。
```js
console.log(typeof undefined); // 输出: undefined
```

**undefined的强制转换**

- 在布尔上下文中，`undefined` 被转换为 `false`。
- 在数值上下文中，`undefined` 被转换为 `NaN`。


## null 与 undefined

### 对比

| 特性       | `null`     | `undefined`     |
| -------- | ---------- | --------------- |
| **含义**   | 表示“无”或“空”  | 表示未定义的值         |
| **类型**   | `object`   | `undefined`     |
| **默认值**  | 需要显式赋值     | 变量声明但未赋值时默认值    |
| **使用场景** | 表示变量或对象没有值 | 表示变量未初始化或函数无返回值 |

### 赋值操作
#### 逻辑空赋值 (??=)

```js
const a = { duration: 50 };
a.speed ??= 25;
console.log(a.speed); // 25

// x ??= y 等价于 x ?? (x = y);
```

#### 空值合并运算符 (??)
```js
const foo = null ?? "default string";
console.log(foo); // "default string"
```

将 `??` 直接与逻辑与（`&&`）和逻辑或（`||`）运算符组合使用是不可取的
```js
null || undefined ?? "foo"; // 抛出 SyntaxError
true && undefined ?? "foo"; // 抛出 SyntaxError
```

提供括号以明确表示优先级

```js
(null || undefined) ?? "foo"; // 返回“foo”
```