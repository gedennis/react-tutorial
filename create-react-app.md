## React 脚手架

现在前端工程化越来越复杂，我们需要使用脚手架工具来完成。脚手架让项目从搭建到开发，再到部署，整个流程变得快速和便捷。React 中常用的脚手架工具是 `create-react-app`。



## 安装

首先确保安装了 node 和 npm。

```bash
$ node --version
v10.13.0
$ npm --version
6.4.1
```

安装 create-react-app。

```bash
npm i -g create-react-app
```

验证安装。

```bash
$ create-react-app --version
4.0.0
```

## 创建项目

通过以下命令创建项目，注意项目名称不能包含大写字母：

```bash
$ create-react-app 项目名称
```

这里我们创建一个项目 `react-demo`，并启动。

```bash
$ create-react-app react-demo
$ cd react-demo
$ npm start
```

可以在浏览器看到如下页面：

<img src="/Users/dennisge/Library/Application Support/typora-user-images/image-20201111162945373.png" alt="image-20201111162945373" style="zoom:50%;" />

## 项目目录结构

默认的目录结构如下：

```
react-demo
├─ README.md // readme说明文档
├─ package.json // 对整个应用程序的描述：包括应用名称、版本号、一些依赖包、以及项目的启动、打包等等（node管理项目必备文件）
├─ public
│    ├─ favicon.ico // 应用程序顶部的icon图标
│    ├─ index.html // 应用的index.html入口文件
│    ├─ logo192.png // 被在manifest.json中使用
│    ├─ logo512.png // 被在manifest.json中使用
│    ├─ manifest.json // 和Web app配置相关
│    └─ robots.txt // 指定搜索引擎可以或者无法爬取哪些文件
├─ src
│    ├─ App.css // App组件相关的样式
│    ├─ App.js // App组件的代码文件
│    ├─ App.test.js // App组件的测试代码文件
│    ├─ index.css // 全局的样式文件
│    ├─ index.js // 整个应用程序的入口文件
│    ├─ logo.svg // 刚才启动项目，所看到的React图标
│    ├─ reportWebVitals.js // 默认帮助我们写好的注册PWA相关的代码
│    └─ setupTests.js // 测试初始化文件
└─ package-lock.lock
```

React 脚手架是使用 Webpack 来打包的。Webpack 是一个现代的 JavaScript 应用程序的静态模块打包器，它会递归的构建一个依赖关系图，将各个模块打包成一个或多个 bundle。

![image-20201111163927947](/Users/dennisge/Library/Application Support/typora-user-images/image-20201111163927947.png)

脚手架默认把 webpack 相关的配置封装在 react-script 中，可以通过 eject 命令，将其暴露。这个过程不可逆。

```bash
$ npm run reject
```

## Hello World 应用

### 精简项目

我们将脚手架项目简化，将目录简化：

- 删除 src 目录下所有文件
- 只留下public 文件下的 favicon.ico 和 index.html 文件。

在 src 目录下创建 `index.js` 文件，这是 webpack的打包入口。输入一下代码：

```js
import React, { Component } from "react";
import ReactDOM from "react-dom";

class App extends Component {
  render() {
    return <h2>Hello World</h2>;
  }
}

ReactDOM.render(<App />, document.getElementById("root"));
```

重新运行项目，看到浏览器显示 `Hello World` 字样。