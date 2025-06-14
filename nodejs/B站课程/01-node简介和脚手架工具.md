> [!info] nodejs 是什么
> `Nodejs`并不是`JavaScript`应用，也不是编程语言，它是`JavaScript`运行时环境，是开源、跨平台的
> `Nodejs`是构建在V8引擎之上的，V8引擎是由C/C++编写的，因此我们的Js代码需要有C/C++转化后再执行

> [!bug] nodejs 能做什么
> nodejs 使用异步 I/O 和事件驱动的设计理念，可以高效的处理大量并发请求，提供了非阻塞式 I/O 接口和事件循环机制,可以编写高性能可扩展的应用程序

读取文件
```js
const fs = require('fs')
fs.readFile('fs/a.txt', 'utf8', function (err, data) {
  console.log(err)
  console.log(data)
})
```

写入内容
```js
const fs = require('fs')
  fs.writeFile('fs/a.txt', '666', function (err) {
  console.log(err)
})
```

追加内容
```js
const fs = require('fs')
fs.readFile('fs/a.txt', 'utf8', function (err, data) {
  if (!err) {
    const newData = data + '888'
    fs.writeFile('fs/a.txt', newData, function (err) {
      if (!err) {
        console.log('写入成功')
      }
    })
  }
})
```

### 模块化编程概念

- 拆分代码
- 相互独立
- 导入导出

JavaScript 模块化开发规范

1. ESMAScript Module 标准规范
   文件结尾 .mjs
   package.json type: module
2. CommonJS 规范（node 默认）

## npm 包管理器

`npm` 全称 Node Package Manager 是 Nodej.s 的包管理工具,他是一个基于命令行的工具，用于帮助开发者在自己的项目中安装、升级、移除和管理依赖项

### npm 命令
- `npm init`
- `npm install`
- `npm install <package-name>`
- `npm install <package-name> --save`
- `npm install <package-name> --save-dev`
- `npm install -g <package-name>`
- `npm update <package-name>`
- `npm uninstall <package-name>`
- `npm run <script-name>`
- `npm search <keyword>`
- `npm info <package-name>`
- `npm list`
- `npm outdated`
- `npm publish`
- `npm login`
- `npm logout`
- `npm config list`
- `npm get registry`

npm install 原理


## 脚手架工具

> [!question] 什么是脚手架
> - 全局命令行工具
> - 创建项目初始化代码文件及目录

> [!check] 脚手架基本能力
> - 全局命令行执行能力
> - 命令行交互能力
> - 项目初始化代码下载能力

> [!abstract] 如何实现一个自己的脚手架工具
> - 创建自定义全局命令
> - 命令参数接收处理
> - 终端交互
> - 下载远程项目代码
> - 项目初始化完成提示

### 创建自定义全局命令

新建文件夹 bin
新建文件 cli.js
```js
#! /usr/bin/env node
console.log('hello world')
```

初始化
```bash
npm init
// package name: (nodejs) mycli
// ...

npm link
// 这个命令会在全局 npm 目录中创建一个符号链接，指向你当前的本地包。

npm unlink --global mycli
// 删除 link
```

package.json
```json
{
  "name": "mycli",
  "version": "1.0.0",
  "main": "index.js",
  "bin": {
    "mycli": "bin/cli.js"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "description": "",
}

```

> [!tip] npm link
>在本地包目录中创建链接
>`npm link`
>在项目中使用链接的包
>`npm link <package>`
>取消链接
> - 在项目目录中运行以下命令，取消项目中的链接
>   `npm unlink <package-name>`
> - 在本地包目录中运行以下命令，取消全局链接
>   `npm unlink`

### 命令参数接收处理
#### process.argv
cli.js
```js
if (process.argv[2] == '--help') {
  console.log('help')
}
```

```bash
mycli --help
// help
```

#### commander 命令参数处理工具

**--help 选项参数处理**

```bash
npm install commander
```

```js
const {program} = require('commander')

program.option('-f --framWork <framWork>', '选择框架')
```

```js
mycli --help
// -f --framWork <framWork>  选择框架
// -h, --help                display help for command
```


**自定义命令参数处理**
cli.js
```js
program
.command('create <projectName> [options...]', '初始化项目')
.alias('crt')
.description('初始化项目')
.action((projectName, options) => {
  // 命令行逻辑代码
  console.log(projectName)
  console.log(options)
})

program.parse(process.argv)
```

模块化拆分
help.js
```js
const myHelp = function (program) {
  program.option('-f --framWork <framWork>', '选择框架')
}
module.exports = myHelp
```

commander.js
```js
const myAction = require('./action')
const myCommander = function (program) {
  program
  .command('create <projectName> [options...]')
  .alias('crt')
  .description('初始化项目')
  .action(myAction)
}

module.exports = myCommander
```

action.js
```js
const inquirer = require('inquirer')

const myAction = function (projectName, args) {
  inquirer.prompt([
    {
      type: 'list',
      name: 'frameWork',
      message: '选择框架',
      choices: ['vue', 'react', 'angular'],
    }
  ]).then((answers) => {
    console.log(answers)
  }).catch(error => {
    console.error(error);
  });
}

module.exports = myAction
```

### 命令行交互式问答
```bash
npm install inquirer
```

这里请注意 Inquirer v9及更高版本是 native esm 模块，这意味着您不能再使用 commonjs 语法require，如果还要使用 require 需要低版本的 Inquirer.js （8.0.0）

新版本的引入方式
```js
import inquirer from 'inquirer';

inquirer
  .prompt([
    /* Pass your questions in here */
  ])
  .then((answers) => {
    // Use user feedback for... whatever!!
  })
  .catch((error) => {
    if (error.isTtyError) {
      // Prompt couldn't be rendered in the current environment
    } else {
      // Something else went wrong
    }
  });

```

### 下载远程项目代码
download-git-repo
```bash
 npm install download-git-repo
```

默认支持 
- **GitHub** - `github:owner/name` or simply `owner/name`
- **GitLab** - `gitlab:owner/name`
- **Bitbucket** - `bitbucket:owner/name`

### 项目初始化完成提示

ora 提示
```bash
npm install ora@5
```

```js
const ora = require('ora')
const spinner = ora()
spinner.start()
spinner.text = '代码正在下载'
spinner.fail('下载失败')
spinner.succeed('下载成功')
```



chalk 样式
```bash
npm install chalk@4
```

```js
console.log(chalk.green.bold('done, you run'))
```