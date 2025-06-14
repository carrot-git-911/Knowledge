> [!info] MongoDB是什么?
> - 一个基于文件存储的分布式NoSQL数据库系统
> - 数据结构由键值对(key,value)组成
> - 拥有非常强大的查询能力

> [!tip] MongoDB有哪些特性?
> 1. 文档型数据库,较强可扩展性,拥有强大的查询语言,多中存储引擎
> 2. 高性能、高可用、水平扩展:支持数据嵌入,子文档查询间、支持副本集与分片
> 3. 多种查询类型支持,且支持数据聚合查询、文本检索、地址位置查询

> [!check] 使用场景
> 1. 对数据处理性能有较高要求
> 2. 需要借助缓存层来处理数据
> 3. 需要高度的伸缩性


## 安装 MongoDB

mongoDB 官网

1. 奇数版本为测试版,偶数为稳定版
2. 3.2之后,不再支持32位操作系统
3. 目前最新稳定版为5.0(课程中使用)

安装
```bash
brew tap mongodb/brew
brew update
brew install mongodb-community@8.0
```

连接
```js
brew services start mongodb-community@8.0
// Successfully started `mongodb-community` (label: homebrew.mxcl.mongodb-community)
```
停止
```js
mongod --config /opt/homebrew/etc/mongod.conf --fork
```

连接并使用 MongoDB
```js
mongosh
```

验证 MongoDB 是否正在运行
```js
brew services list
```


navicat
[Navicat \| 下载 Navicat Premium 14 天免费 Windows、macOS 和 Linux 的试用版](https://www.navicat.com.cn/download/navicat-premium)

数据库相关
```js
// 查看所有数据库
show databases
show dbs

// 选择数据库(如果数据库不存在,不会报错;会隐式创建:当后期该数据库有数据时自动创建)
use 数据库名

// 删除数据库(先选中数据库)
db.dropDatabase()

```

集合相关
```js
// 查看所有集合
show collections

// 创建集合(插入数据会隐式创建)
db.createCollection('集合名')

// 删除集合
db.集合名.drop()
```

插入
```js
db.collection.insert(json数据)
db.collection.insertOne(document, options)
db.collection.insertMany(documents, options)
```

查询
```js
db.collection.find(query, projection)
db.collection.findOne(query, projection)
```

高级查询方法
比较符
`$gt、$lt、$gte、$lte、$eq、$ne`
```js
// 查找年龄大于 25 的文档:
db.myCollection.find({ age: { $gt: 25 } });
```

逻辑
`$and、$or、$not、$nor`
```js
db.myCollection.find({
    $and: [
        { age: { $gt: 25 } },
        { city: "New York" }
    ]
});
```


更新
```js
db.collection.updateOne(filter, update, options)
db.collection.updateMany(filter, update, options)
```

- **filter**：用于查找文档的查询条件。
- **update**：指定更新操作的文档或更新操作符。
- **options**：可选参数对象，如 `upsert`、`arrayFilters` 等。

删除
```js
// deleteOne() 方法用于删除匹配过滤器的单个文档
db.users.deleteOne({ name: "John Doe" });
// deleteMany() 方法用于删除所有匹配过滤器的文档
db.collection.deleteMany(filter, options)
// findOneAndDelete() 方法用于查找并删除单个文档，并可以选择返回删除的文档
db.collection.findOneAndDelete(filter, options)
```


## node 链接 mongoDB

npm mongodb
[mongodb - npm](https://www.npmjs.com/package/mongodb)

```js
npm install mongodb
```

```js
const { MongoClient } = require('mongodb');

const client = new MongoClient('mongodb://127.0.0.1:27017')

const main = async () => {
  await client.connect();
  const db = client.db('mytest');
  const collection = db.collection('cc');
  const data = await collection.find()
  console.log(await data.toArray());
}

main().finally(() => {
  client.close();
})
```

