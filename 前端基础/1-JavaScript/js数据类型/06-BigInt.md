> [!abstract]
> JavaScript 的 `BigInt` 是一种特殊的数值类型，用于表示任意精度的整数，它解决了传统 `Number` 类型无法精确表示超大整数的问题

### 为什么需要 BigInt

JavaScript 的 `Number` 类型使用 IEEE 754 双精度浮点数格式表示，只能安全表示 -2⁵³ - 1 到 2⁵³ - 1 之间的整数。超出这个范围，整数可能会失去精度

```js
console.log(Number.MAX_SAFE_INTEGER) // 9007199254740991
console.log(Number.MAX_SAFE_INTEGER + 1); // 9007199254740992
console.log(Number.MAX_SAFE_INTEGER + 2); // 9007199254740992 - 这里开始失去精度
```

### 创建 BigInt

**在数字后边加n**

```js
const bigInt = 1234567890123456789012345678901234567890n
console.log(bigInt)
```

**使用 BigInt 函数**

```js
const bigInt = BigInt('1234567890123456789012345678901234567890')
console.log(bigInt)
```

BigInt 基本操作

算术运算

BigInt 支持基本的算术运算：`+` `-` `*` `**` `/`（除法会向下取整） `%`

```js
const a = 10n
const b = 20n

console.log(a + b); // 30n
console.log(b - a); // 10n
console.log(a * b); // 200n
console.log(b / a); // 2n (不是 2.5n)
console.log(b % a); // 0n
console.log(a ** 3n); // 1000n
```

比较运算

BigInt 可以和 Number 进行比较（但不能直接混合运算）

```js
console.log(10n === 10) // false (类型不同)
console.log(10n == 10) // true
console.log(10n < 20) // true
console.log(10n > 5) // true
```

位运算 #TODO 研究一下位运算

BigInt 支持位运算：`&`, `|`, `^`, `~`, `<<`, `>>`

```js
console.log(5n & 3n); // 1n (0101 & 0011 = 0001)
console.log(5n | 3n); // 7n (0101 | 0011 = 0111)
console.log(5n ^ 3n); // 6n (0101 ^ 0011 = 0110)
console.log(~5n); // -6n (~0101 = 1010)
console.log(5n << 1n); // 10n
console.log(5n >> 1n); // 2n
```


注意事项

不能与 Number 混合运算

```js
console.log(10n + 5) // TypeError: Cannot mix BigInt and other types
```

BigInt 不能用于 Math 对象的方法

```js
console.log(Math.aqrt(16n)) // TypeError: Cannot convert a BigInt value to a number
```

BigInt 除法会截断小数部分

```js
console.log(5n / 2n) // 2n 不是 2.5n
```

JSON 序列化问题

```js
const obj = { big: 10n };
console.log(JSON.stringify(obj)); // TypeError: Do not know how to serialize a BigInt
```

示例场景

解决精度问题

```js
const maxSafe = BigInt(Number.MAX_SAFE_INTEGER);
console.log(maxSafe + 1n === maxSafe + 2n); // false（BigInt 无精度丢失）
```

大数计算

```js
// 计算 2^100
const power = 2n ** 100n
console.log(power.toString()) // 1267650600228229401496703205376
```

处理大数 ID

```js
// 处理来自数据库的大数ID
const userId = BigInt("12345678901234567890");
console.log(`User ID: ${userId.toString()}`);
```

大素数检测

```js
function isPrime(x) {
  if (x < 1n) return false
  for (let i = 2n; i*i <= x; i++) {
    if (x % i === 0n) return false
  }
  return true
}
console.log(isPrime(1000000007n)); // true
console.log(isPrime(1000000008n)); // false
```

斐波那契数列(大数版)

```js
function fibonacci(n) {
  let a = 0n, b = 1n;
  for (let i = 0n; i < n; i++) {
    [a, b] = [b, a + b];
  }
  return a;
}

console.log(fibonacci(100n).toString()); 
// 354224848179261915075
```