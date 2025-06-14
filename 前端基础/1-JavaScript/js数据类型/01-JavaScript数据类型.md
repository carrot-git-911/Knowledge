## 栈和堆

### 栈（stack）

栈内存它是一种静态分配的内存，用于存储基本数据类型和函数调用。在 JavaScript 中，所有的基本数据类型都存储在栈内存中。当我们声明一个变量时，JavaScript 会在栈内存中为其分配一块内存空间，并将变量的值存储在这个内存空间中。

- 后进先出，先进后出，简称 **后进先出**（LIFO），这就是典型的`栈`结构。
- 新添加的或待删除的元素都保存在栈的末尾，称作`栈顶`，另一端就叫`栈底`。
- 在栈里，新元素都靠近栈顶，旧元素都接近栈底。
- 从栈的操作特性来看，是一种 `操作受限`的线性表，只允许在一端插入和删除数据。
- 不包含任何元素的栈称为`空栈`。

栈也被用在编程语言的编译器和内存中保存变量、方法调用等，比如函数的调用栈。

### 堆（heap）

堆数据结构是一种树状结构。 它的存取数据的方式，与书架和书非常相似。我们不关心书的放置顺序是怎样的，只需知道书的名字就可以取出我们想要的书了。 好比在 JSON 格式的数据中，我们存储的 key-value 是可以无序的，只要知道 key，就能取出这个 key 对应的 value。

### js堆与栈的比较


> [!success] 栈
> 栈是自动分配相对固定大小的内存空间，并由系统自动释放，存放基本数据类型和引用类型的变量
> 所有在函数/方法中定义的变量都是放在栈中，随着函数/方法的执行结束，这个函数/方法的内存栈也自然销毁。由 JavaScript 引擎来管理
> 优点：存取速度比堆快。
> 缺点：存在栈中的数据大小与生存期必须是确定的，缺乏灵活性。

> [!tip] 堆
> 堆是动态分配内存，内存大小不一，也不会自动释放，存放**引用类型的对象**
> 堆内存中的对象不会随方法的结束而销毁，即使方法结束后，这个对象还可能被另一个引用变量所引用(参数传递)。创建对象是为了反复利用。
> 由垃圾回收机制来管理

![[file-pasted-20250111172424228.png]]
## 数据类型

> [!sucess]
> **基本类型**
> 
> 字符串（String）、数字(Number)、布尔(Boolean)、空（Null）、未定义（Undefined）、Symbol（独一无二的值）、BigInt
> 
> **引用类型**
> 
> 对象(Object)、数组(Array)、函数(Function)

### 基本类型/原始类型

**number** - [[02-Number]]

- 表示数字，包括整数和浮点数
```js
let age = 25;
let price = 99.99;
```


**String** - [[03-String]]

- 表示文本数据，用单引号、双引号或反引号包裹
```js
let name = "Alice";
let message = 'Hello, world!';
let template = `Hello, ${name}!`; // 模板字符串
```

**Boolean** - [[04-boolean、null、undefined]]

- 表示逻辑值，只有 `true` 和 `false` 两个值。
```js
let isActive = true;
let isCompleted = false;
```

**undefined** - [[04-boolean、null、undefined]]

- 表示未定义的值。变量声明但未赋值时，默认值为 `undefined`
```js
let x;
console.log(x); // 输出: undefined
```

**null** - [[04-boolean、null、undefined]] 

表示空值或无值。通常用于显式清空变量
```js
let data = null;
```

**symbol** es6新增 [[05-Symbol]]

- 表示唯一的标识符，通常用于对象属性的键
```js
let id = Symbol("id");
```

**bigint** - [[06-BigInt]]

表示大整数，用于表示超出 `number` 类型范围的整数
```js
let bigNumber = 1234567890123456789012345678901234567890n;
```

### 引用类型

引用类型是存储在堆内存中的复杂数据，变量存储的是指向堆内存的地址

**object**

- 表示对象，用于存储键值对。
```js
let person = {
  name: "Alice",
  age: 25
};
```

**array**

- 表示数组，用于存储有序的数据集合。
```js
let numbers = [1, 2, 3, 4, 5];
```

**function**

- 表示函数，是一种可调用的对象。
```js
function greet(name) {
  console.log(`Hello, ${name}!`);
}
```

**date**

- 表示日期和时间。
```js
let today = new Date();
```

**repexp**

- 表示正则表达式，用于匹配字符串。
```js
let pattern = /hello/i;
```


原始类型与引用类型的区别

| 特性       | 原始类型 | 引用类型           |
| -------- | ---- | -------------- |
| **存储位置** | 栈内存  | 堆内存            |
| **存储内容** | 实际值  | 内存地址           |
| **复制行为** | 复制值  | 复制引用（指向同一内存地址） |
| **可变性**  | 不可变  | 可变             |
| **比较方式** | 比较值  | 比较引用（内存地址）     |

### 类型检测

`typeof`
用于检测原始类型（除 `null` 外）和 `function`

```js
console.log(typeof 42);          // 输出: "number"
console.log(typeof "hello");     // 输出: "string"
console.log(typeof true);        // 输出: "boolean"
console.log(typeof undefined);   // 输出: "undefined"
console.log(typeof null);        // 输出: "object" （历史遗留问题）
console.log(typeof Symbol("id"));// 输出: "symbol"
console.log(typeof {});          // 输出: "object"
console.log(typeof []);          // 输出: "object"
console.log(typeof function(){});// 输出: "function"
```

`instaceof`
用于检测引用类型的具体类型
```js
console.log([] instanceof Array);      // 输出: true
console.log({} instanceof Object);     // 输出: true
console.log(function(){} instanceof Function); // 输出: true
```

`object.prototype.toString`
用于精确检测数据类型
```js
console.log(Object.prototype.toString.call(42));       // 输出: "[object Number]"
console.log(Object.prototype.toString.call("hello"));  // 输出: "[object String]"
console.log(Object.prototype.toString.call([]));       // 输出: "[object Array]"
console.log(Object.prototype.toString.call(null));     // 输出: "[object Null]"
```