> [!success] Object
> 是 JavaScript 的一种数据类型，用于存储各种键值集合和更复杂的实体，可以通过 Object 构造函数或者使用对象字面量方式创建
> 在 JavaScript 中，几乎所有的对象都是 Object 的实例。


## 对象分类

**内建对象**
   由 ES 标准中定义的对象，在任何的 ES 的实现中都可以使用
   比如：Math String Number Boolean Function Object...

**宿主对象**
   由 JS 的运行环境提供的对象，目前来讲主要是指浏览器提供的对象
   比如：BOM DOM

**自定义对象**
   由开发人员自己创建的对象

**定义**
- 无序的数据集合
- 键值对的集合 ( key: value ) object 是七种数据类型中唯一一种复杂类型。

## 对象创建

### 字面量形式
```js
const person = {
  name: 'Alice',
  age: 25,
  greet() {
    return `Hello, I'm ${this.name}!`;
  }
};
```

### 构造函数
```js
const car = new Object()
car.brand = 'Tesla'
car.drive = function() { return 'Driving' }
```

### Object.create()

```js
const animal = { eats: true };
const rabbit = Object.create(animal);
rabbit.jumps = true;
```

### new 关键字

new 在执行时会做四件事情：
1. 在内存中创建一个新的空对象。
2. 让 this 指向这个新的对象。
3. 执行构造函数里面的代码，给这个新对象添加属性和方法。
4. 返回这个新对象（所以构造函数里面不需要 return）。

```js
function One(name,age){
  this.name=name;
  this.age=age;
}
function myNew(fn,...args){
  let obj={};
  obj.__proto__=fn.prototype;
  let res=fn.apply(obj,args);
  if(res instanceof Object){
    return res;
  }else{
    return obj;
  }
}
let person=myNew(One,"张三",18);
```
## 属性操作

- 对象里面的属性调用 : 对象.属性名 ，这个小点 . 就理解为“ 的 
- 对象里面属性的另一种调用方式 : 对象[‘属性名’]，注意方括号里面的属性必须加引号，我们后面会用
- 对象里面的方法调用：对象.方法名() ，注意这个方法名字后面一定加括号
### 访问单个属性

```js
console.log(person.name);      // 'Alice'（点符号）
console.log(person['age']);    // 25（方括号，支持动态键名）

// obj[变量名]
// []代表用a 这个变量的值作属性名，而不是字符串'a'作属性名
let a = 'xxx'
let obj = { [a]: 1111 }
```

### 添加删除修改属性

```js
obj.name="tom"；
obj["name"]="tom";

obj.name = undefined
delete obj.name;
delete obj['name'];
```

### 检查属性存在
```js
"属性名" in 对象名;
对象名.hasOwnProperty("属性名");

for (变量 in 对象名字) {
    // 在此执行代码
}
```

### 遍历对象

查看自身属性
```js
let obj = {name: 'Mia', age: 18}

console.log(Object.keys(obj)) // 查看自身属性名
console.log(Object.values(obj)) // 查看自身属性值
console.log(Object.entries(obj)) // 查看自身属性名和值
```

查看 自身属性 和 共有属性
```js
// console.dir()可以显示一个对象所有的属性和方法
// 显示指定JavaScript对象的属性列表
console.dir(obj)
```

查看共有属性（不推荐）
```js
obj.__proto__    // 不推荐
```

判断一个属性 'xxx' 是自身的还是共有的
```js
obj.hasOwnProperty('xxx')     // true就是自身的，false就是共有或不存在
```

<mark class="hltr-yellow">'xxx' in obj 不能判断出这个属性是否是自身属性还是共有属性,可以验证是否在该对象中
obj.hasOwnProperty('xxx') 可以判断出这个属性是否是自身属性</mark>

拓展：
<mark class="hltr-cyan">console.table()</mark>方法用于在控制台中以表格形式显示数组或对象的数据。这对于可视化复杂数据结构非常有用，使数据更易于阅读和理解。
## 对象方法

Object.assign()
将一个或多个源对象中所有可枚举的自有属性复制到目标对象，并返回修改后的目标对象
```js
Object.assign(target,...sources)
```

