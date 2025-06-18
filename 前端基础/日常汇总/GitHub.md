### 配置 SSH Key

**查看是否有 SSH Key**
路径 查看是否有 SSH Key

**生成 SSH Key**
```js
ssh-keygen -t rsa -C 1667899744@qq.com

// -t 来指定秘钥类型，这里使用的是rsa
// -C 指定在秘钥中的一个注释字段，方便用户标识这个秘钥的用途或其他有用信息

Enter passphrase, 回车
Enter same passphrase again，再次回车
SSH Key 创建成功
```

**问题**
```js
connect to host github.com port 22: Connection timed out
```

测试连接
```js
ssh -T git@github.com
```

修改端口
```js
ssh -T -p 443 git@ssh.github.com
```

修改 SSH 的 config 配置文件
```js
Host github.com
  Hostname ssh.github.com
  port 443
```

再次测试连接
```js
Hi xxxxx! You've successfully authenticated, but GitHub does not provide shell access
```

可以克隆仓库

### LF 和 CRLF 换行符问题

可以使用 `git config` 命令来查看或修改 `core.autocrlf` 属性
```js
git config --global core.autocrlf [input | true | false]
```

也可以在 `.gitconfig` 文件中直接编辑 `core.autocrlf` 属性

```js
[core]
  autocrlf = input
```

除了 `core.autocrlf` 之外，还有一个配置项，`core.eol`（end of line），可以指定仓库中文件使用哪种换行符
- `lf`：表示仓库中文件使用 LF 作为换行符。
- `crlf`：表示仓库中文件使用 CRLF 作为换行符。
- `native`：表示仓库中文件使用当前操作系统默认的换行符。
可以使用 `git config` 命令来查看或修改 `core.eol` 属性
```js
git config --global core.eol [lf | crlf | native]
```