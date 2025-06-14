> [!info]
> `Symbol` 是 ES6引入的一种原始数据类型，用于表示唯一的标识符，它常用于对象属性的键，以避免命名冲突，并支持元编程能力

## 核心特性

**唯一性**
每个 Symbol 值都是唯一的，即使他们的描述相同
```js
const s1 = Symbol('id');
const s2 = Symbol('id');
console.log(s1 === s2); // false
```

**不可显式创建实例**
`Symbol` 是原始类型，不能使用 `new` 关键字

```js
const s = new Symbol(); // TypeError: Symbol is not a constructor
```

**描述符仅用于调试**
创建时的描述符（字符串）仅用于标识 Symbol，不影响其唯一性
```js
const s = Symbol('debug_desc');
console.log(s.description); // 'debug_desc' (ES2019+)
```

## 创建Symbol

**基本创建**
```js
const sym1 = Symbol();
const sym2 = Symbol('自定义描述');
```

**全局 Symbol 注册表**
使用 `Symbol.for(key)` 在全局注册表中创建或复用 Symbol
```js
const globalSym1 = Symbol.for('global_key')
const globalSym2 = Symbol.for('global_key')
console.log(globalSym1 === globalSym2); // true
```

**获取已注册 Symbol 的值**
```js
const key = Symbol.keyFor('globalSym1')
console.log(key) // 'global_key'
```

## 应用场景

**唯一对象属性名**

防止属性名冲突，适合作为对象的“特殊”属性
```js
const user = {
  id: 100,
  [Symbol('internal_id')]: 'X1-Y2' // 内部使用的唯一属性
};

console.log(Object.keys(user)); // ['id'] （Symbol 属性默认不可枚举）
```

**模拟私有属性**
注意：并非真正私有，但可避免意外访问

```js
const _password = Symbol('password')

class User {
  constructor(name, password) {
    this.name = name;
    this[_password] = password; // “伪私有”属性
  }

  checkPassword(pwd) {
    return this[_password] === pwd;
  }
}
const alice = new User('Alice', '123');
console.log(alice[_password]); // 仍可访问，但需要 Symbol 引用
console.log(Object.getOwnPropertySymbols(alice)); // [Symbol(password)]
```


**内置 Symbol 值(Well-knownSymbols)**
通过实现内置 Symbol 方法，自定义对象行为

`Symbol.iterator`
使对象可迭代
```js
const myIterable = {
  [Symbol.iterator]: function* () {
    yield 1;
    yield 2
    yield 3
  }
}
```

`Symbol.toStringTag`
自定义 `Object.prototype.toString` 结果
```js
class MyClass {
  get [Symbol.toStringTag]() {
    return 'MyClass';
  }
}

console.log(Object.prototype.toString.call(new MyClass())); // [object MyClass]
```

`Symbol.hasInstance`
自定义 `instanceof` 行为
```js
class MyArray {
  static [Symbol.hasInstance](instance) {
    return Array.isArray(instance)
  }
}
console.log([] instanceof MyArray) // true
```

## 注意事项

**Smybol 属性不可枚举**
默认不会被 `for...in`、`Object.keys()` 遍历，需用 `Object.getOwnPropertySymbols()` 获取

JSON 序列化会忽略 Symbol
```js
const obj = { [Symbol('key')]: 'value' };
console.log(JSON.stringify(obj)); // {}
```

**类型转换限制**
Symbol 不能隐式转换为字符串或数字，需显式转换

```js
const sym = Symbol('desc');
console.log(String(sym)); // 'Symbol(desc)'
console.log(sym.toString()); // 'Symbol(desc)'
```

## 总结

- **核心价值**：唯一性、避免命名冲突、元编程。
- **适用场景**：唯一属性键、自定义对象行为、库/框架开发。
- **慎用场景**：需要序列化或隐式类型转换的属性。
- 用 `typeof` 判断 Symbol 类型