# 快速入门

通过一个小例子来快速入门。需求：

<img src="/Users/dennisge/Library/Application Support/typora-user-images/image-20201110161958257.png" alt="image-20201110161958257" style="zoom:50%;" />

## 原生实现

工作目录下，新建一个`vanilla.html`文件，输入一下内容：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Demo for React</title>
</head>
<body>
  <div class="app">
    <h2 class="title">Hello World</h2>  
    <button class="change-btn">改变脚本</button>
  </div>

  <script>
    // 1. 获取 title DOM 节点
    const titleElement = document.getElementsByClassName("title")[0];

    // 2. 数据处理
    let message = "Hello World";

    // 3. 将数据显示于 titleElement
    titleElement.innerHTML = message;

    // 4. 更改title内容
    const changeBtn = document.getElementsByClassName("change-btn")[0];
    changeBtn.addEventListener('click', (e) => {
      message = "Hello React";
      titleElement.innerHTML = message;
    })
  </script>
</body>
</html>
```

在 VSCode界面，在文件上右键，【Open With Live Server】。然后再浏览器查看效果。

## React 实现

### 依赖

React 应用开发必须依赖的三个库：

- react: 包含 react 的核心代码
- React-dom: react 渲染在不同平台所需要的代码。
- babel: 对  jsx 和 ES6 语法转换的工具

可以通过 CDN 和 npm 的方式引入。这里我们使用 CDN 的方式：

```js
<script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```

`crossorigin`属性用于拿到跨域脚本的错误信息。

### 基础结构

静态显示 Hello World。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Hello React with React</title>
  </head>
  <body>
    <div id="app"></div>

    <script
      src="https://unpkg.com/react@16/umd/react.development.js"
      crossorigin
    ></script>
    <script
      src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"
      crossorigin
    ></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
    <script type="text/babel">
      // 使用 ReactDOM 渲染页面内容
      ReactDOM.render(<h2>Hello World</h2>, document.getElementById("app"));
    </script>
  </body>
</html>
```

几点要注意的：

- 编写 React 的 script 需要使用`type="text/babel"`来让 babel 解析 jsx 语法。
- ReactDOM.render 函数：渲染页面内容，两个参数
  - 参数1： HTML 元素或者 React 组件
  - 参数2： 渲染内容要挂在的 HTML 元素。

### 插值

上面的内容是写死的，可以通过 `{}语法`引入外部的变量或者表达式。修改 script 脚本为：

```js
 let message = "Hello World";
 // 使用 ReactDOM 渲染页面内容
 ReactDOM.render(<h2>{message}</h2>, document.getElementById("app"));
```

### 添加按钮事件

```html
<script type="text/babel">
      let message = "Hello World";

      render();

      // click handler
      function btnClick() {
        message = "Hello React";
        render();
      }
      // 使用 ReactDOM 渲染页面内容
      function render() {
        ReactDOM.render(
          <div>
            <h2>{message}</h2>
            <button onClick={btnClick}>改变文本</button>
          </div>,
          document.getElementById("app")
        );
      }
</script>
```

### 组件 Component

通过如下方式定义一个组件：

```js
 class App extends React.Component {
        render() {
          return <h2>Hello World</h2>;
        }
  }
```

- 继承 React.Component
- 实现 render 函数

#### 组件数据

组件中的数据分为两类：

- 参与界面更新的数据：数据变化，更新组件渲染的内容
- 不参与界面更新的数据：数据变化不会渲染

参与界面更新的数据，成为参与数据流，定义在当前对象的 `state` 中。在构造函数中通过`this.state={定义数据}`。当数据发生变化是，通过`this.setState()`方法来更新数据，并且通知 React 进行 update 。React 会调用 render 函数进行渲染。

**事件绑定**

可以在组件的HTML 元素中增加事件绑定。

```js
// 事件绑定 
<button onClick={this.changeText.bind(this)}>改变文本</button>

// 事件处理
changeText() {
    this.setState({
    	message: "Hello React",
    });
}
```

这里需要解释一下 `this.changeText.bind(this)`.为什么需要绑定 this 不可以直接`this.changeText()`？

在正常的 DOM 操作中，监听函数中的 this 是指向节点对象，比如 button。但 React 不是直接渲染为真实的DOM, 本质是 React 的 Element 对象。React 内部在事件监听时，给监听函数绑定的this是 undefined。所以监听函数中的使用的 this 全是 undefined。所以，需要绑定 this。

完整代码如下：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Hello React with React</title>
  </head>
  <body>
    <div id="app"></div>

    <script
      src="https://unpkg.com/react@16/umd/react.development.js"
      crossorigin
    ></script>
    <script
      src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"
      crossorigin
    ></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
    <script type="text/babel">
      class App extends React.Component {
        constructor() {
          super();
          this.state = {
            message: "Hello World",
          };
        }

        changeText() {
          this.setState({
            message: "Hello React",
          });
        }
        render() {
          return (
            <div>
              <h2>{this.state.message}</h2>
              <button onClick={this.changeText.bind(this)}>改变文本</button>
            </div>
          );
        }
      }
      ReactDOM.render(<App />, document.getElementById("app"));
    </script>
  </body>
</html>

```

