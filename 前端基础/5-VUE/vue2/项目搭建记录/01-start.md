## 环境准备

安装 nodejs 和 npm

```js
node -v  # 查看 Node.js 版本
npm -v   # 查看 npm 版本
```

配置 npm 镜像源（可选）

```js
npm config set registry https://registry.npmmirror.com
```

安装 vue cli
```js
npm install -g @vue/cli@4
npm install -g @vue/cli@4.5.15  # 安装 Vue CLI 4.x（支持 Vue 2）
vue --version
```

## 创建 vue2项目

### 初始化

在当前文件创建项目
```js
vue create .
```

直接创建
```bash
vue create admin-system
# 手动选择配置 (Manually select features)
# 勾选: Babel, Router, Vuex, CSS Pre-processors, Linter
# Vue 版本选择 2.x
# 其他配置按需选择
cd admin-system
```

安装依赖
```bash
npm install
```

运行开发服务器
```bash
npm run serve
```

### 集成 Element UI

安装依赖
```bash
npm install element-ui@2.15.14  # 最后一个支持 Vue 2 的版本
```

完整引入
修改 `src/main.js`
```js
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'

Vue.use(ElementUI)
```

按需加载

babel-plugin-component 插件，这是实现按需引入的核心依赖
```bash
npm list babel-plugin-component // 检查依赖存在
npm install babel-plugin-component -D // 按需加载插件
```

修改 `babel.config.js`
```js
module.exports = {
  presets: ['@vue/cli-plugin-babel/preset'],
  plugins: [
    [
      "component",
      {
        "libraryName": "element-ui",
        "styleLibraryName": "theme-chalk"
      }
    ]
  ]
}
```

创建按需引入配置文件
- `element.js` - 完整版配置，包含大部分常用组件
- `element-minimal.js` - 最小化配置，仅包含最常用组件
- `README.md` - 详细的使用说明文档

`src/element.js`
```js
import Vue from 'vue'
import { Button, Form, FormItem, Input, Menu, Message } from 'element-ui'

const components = [ Button, Input, Form, FormItem ]

// 批量注册组件

components.forEach(component => {
  Vue.component(component.name, component)
})

// 挂载全局消息提示
Vue.prototype.$message = Message
```

在 `src/main.js` 引入配置
```js
import Vue from 'vue'
import App from './App.vue'
import './plugins/element'  // 加载 Element 配置

Vue.config.productionTip = false

new Vue({
  render: h => h(App)
}).$mount('#app')
```

安装 vue-router element
```js
npm install vue-router@3.6.5 element-ui@2.15.14
```

### AXIOS

安装
```js
npm install axios
```

封装 request
```js

```
### 路由

路由配置 `src/router/index.js`

```js
import Vue from 'vue'
import Router from 'vue-router'

Vue.use(Router)
```

登录

权限



sass sass-loader