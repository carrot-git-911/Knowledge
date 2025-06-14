> [!abstract]
> - 用户（频道）系统
> - 视频系统
> - 交互系统


node 实现服务器逻辑梳理

- 使用 Node 创建一个 HTTP 的服务器,并能够接收到客户端发来的请求
- 获取到客户端具体的请求数据,并根据不同的请求数据进行处里
- 将处理之后的结果,响应回客户端,并断开本次链接

### node 核心模块http

- 创建 HTTP 服务器
- 服务器接受请求并处理
- 响应处理结果并断开链接

```js
// 导入http模块
const http = require('http');

// 创建服务器
// 获取服务器实例对象
const server = http.createServer();

// 监听端口
server.listen(8080, () => {
  console.log('服务启动成功');
  console.log('http://127.0.0.1:8080');
});

server.on('request', (req, res) => {
  console.log('收到请求');
  res.write('8888');
  res.end();
}); 
```


服务器数据响应类型处理

设置响应头
```js
res.setHeader('Content-Type', 'text/plain;charset=utf-8');
res.setHeader('Content-Type', 'text/html;charset=utf-8');
```

模块化


nodemon
自动重启服务