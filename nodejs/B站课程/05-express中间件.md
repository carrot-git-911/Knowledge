
 > [!check] 分类
 > 应用程序级别中间件
 > 路由级别中间件
 > 错误处理中间件
 > 内置中间件
 > 第三方中间件
 
 ```js
 const express = require('express')
 
 // 加一个注释，用以说明，本项目代码可以任意定制更改
 const app = express()
 
 const PORT = process.env.PORT || 3000
 
 app.use((req, res, next) => {
   console.log(`${req.method}`, req.url, Date.now())
   next()
 })
 app.get('/', (req, res) => {
   res.send('/index')
 })
 
 app.get('/register', (req, res) => {
   res.send('/register')
 })
 
 app.get('/login', (req, res) => {
   res.send('/login') 
 })
 
 app.listen(PORT, () => {
   console.log(`Server is running at http://localhost:${PORT}`)
 })
 
 ```

### 应用程序级别中间件

```js
app.use((req, res, next) => {
  console.log(`${req.method}`, req.url, Date.now())
  next()
})
```

```js
app.get('/user', (req, res, next) => {
  res.send('/index')
})
```

### 路由级别

```js
app.use('/user',router)
app.use('/video',routerVideo)

app.use((req, res, next) => {
  res.status(404).send('404 not found')
})

app.use((err, req, res, next) => {
  console.log(err)
  res.status(500).send('500 error')
})
```


? + *
127.0.0.1:3000/us?er
127.0.0.1:3000/us+er
127.0.0.1:3000/us * er


```js
app.get('/user/:id', (req, res) => {
  console.log(req.params)
  res.send('/users')
})
// 127.0.0.1:3000/user/3
// {id: 3}
```

路由的链式调用
```js
app
.get('/user/:id', (req, res) => {
  console.log(req.params)
  res.send('/users')
})
.post('/vedio', (req, res) => {
  
})
```

```js
router
.get('/', (req, res) => {
  console.log(req.method)
  res.send('/index')
})
.get('/users', (req, res) => {
  console.log(req.method)
  res.send('/users')
})
```

响应方法
```js
// res.send('/users')
// res.download('./db.json')
// res.end()
// res.json()
// res.redirect()
// res.render()
// res.sendStatus(200)
// res.status(200).json()
```