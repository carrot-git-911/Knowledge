[Express - 基于 Node.js 平台的 web 应用开发框架 - Express中文文档 \| Express中文网](https://www.expressjs.com.cn/)

> [!tip] express 特性
> 上手简单,学习门槛低
> 具有丰富的基础API支持
> 强大的路由功能
> 灵活的中间件机制及丰富的第三方中间支持
> 性能接近原生Node


> [!question] express 能做什么
> 传统 Web 网站
> API 接口服务器
> 服务端渲染中间层
> 开发辅助工具


npx 使用

1. **避免全局安装**
	- 无需全局安装包，减少全局污染。
	- 特别适合一次性使用的工具。
2. **简化开发流程**
	- 直接运行包命令，无需手动安装和配置。
3. **支持本地和远程包**
	- 可以运行本地安装的包，也可以运行远程脚本。

```bash
npx express-generator
```

自己创建文件夹
```bash
npm install express
```

## Express 基本使用

```js
const express = require('express')
const app = express()

app.listen(3000, () => {
  console.log('服务启动成功')
})
```

```javascript
// GET method route
app.get('/', (req, res) => {
  res.send('GET request to the homepage')
})

// POST method route
app.post('/', (req, res) => {
  res.send('POST request to the homepage')
})
```


promisify
`promisify` 是一个用于将 **回调函数（Callback）** 转换为 **Promise** 的工具。它通常用于将传统的基于回调的异步函数转换为基于 Promise 的异步函数，从而更方便地使用 `async/await` 或 `.then()` 语法来处理异步操作。

在 Node.js 中，`util.promisify` 是一个内置的工具函数，专门用于实现这一功能。

```js
const { promisify } = require('util')
const readFile = promisify(fs.readFile)
const writeFile = promisify(fs.writeFile)
```

### 获取用户

```js
app.get('/', async (req, res) => {
  try {
    let back = await readFile('./db.json', 'utf8')
    const jsonback = JSON.parse(back)
    res.send(jsonback)
  } catch (error) {
    res.status(500).json({ error })
  }
}) 
```

### 添加用户
```js
app.post('/', async (req, res) => {
  let body = req.body
  console.log(body)
  if (!body) {
    res.status(403).json({ error: '没有数据' })
  }
  let back = await readFile('./db.json', 'utf8')
  const jsonback = JSON.parse(back)
  body.id = jsonback.users[jsonback.users.length - 1].id + 1
  jsonback.users.push(body)
  try {
    let w = await writeFile('./db.json', JSON.stringify(jsonback))
    if (!w) {
      res.status(200).send({
        msg: '保存成功'
      })
    }
    res.send(jsonback)
  } catch (error) {
    res.status(500).json({ error })
  }
})
```

### 修改用户

```js
app.put('/:id', async (req, res) => {
  try {
    let userInfo = await readFile('./db.json', 'utf8')
    const jsonuserInfo = JSON.parse(userInfo)
    let userId = parseInt(req.params.id)
    let user = jsonuserInfo.users.find(item => {
      return item.id === userId
    })
    if (!user) {
      res.status(403).json({ error: '没有数据' })
    }
    const body = req.body
    user.username = body.username ? body.username : user.username
    user.age = body.age ? body.age : user.age
    jsonuserInfo.users[userId - 1] = user
    let w = await writeFile('./db.json', JSON.stringify(jsonuserInfo))
    if (!w) {
      res.status(200).send({
        msg: '保存成功'
      })
    }
  } catch (error) {
    res.status(500).json({ error })
  }
})
```

