# stage1

````ini
---

### 📦 **项目1：手动配置第一个 Webpack 项目（零 CLI 依赖）**
**核心目标**：不使用任何脚手架工具，纯手动配置 Webpack 基础打包流程

---

#### 🔧 **前置知识清单**
1. Node.js 基础（会使用 `npm init`）
2. 理解前端模块化概念（CommonJS/ES Module）
3. 知道浏览器无法直接解析 `import/export` 语法

---

### 📝 **分步实现手册**

#### **步骤1：环境准备**
```bash
# 创建项目目录并初始化 npm
mkdir my-webpack-demo && cd my-webpack-demo
npm init -y  # -y 表示自动生成 package.json
````

**步骤2：安装核心依赖**

```bash
# 安装 Webpack 本体（注意：不安装 webpack-cli）
npm install webpack --save-dev
```

**关键说明**：

* 为什么不用 `webpack-cli`？为了强制手动配置，避免工具自动生成文件干扰理解
*   此时你的 `package.json` 中会出现：

    ```json
    "devDependencies": {
      "webpack": "^5.x.x"
    }
    ```

***

**步骤3：创建基础文件结构**

```bash
# 创建必要目录和文件
mkdir src dist
touch src/index.js dist/index.html webpack.config.js
```

文件结构应如下：

```
my-webpack-demo/
├── src/
│   └── index.js       # 入口文件
├── dist/
│   └── index.html     # 手动创建的 HTML
├── webpack.config.js  # Webpack 配置文件
└── package.json
```

***

**步骤4：编写基础代码**

1.  **src/index.js**（入口文件）：

    ```javascript
    const sayHello = () => {
      console.log('Hello from Webpack!');
      document.body.innerHTML = '<h1>手动配置成功!</h1>';
    };

    sayHello();
    ```
2.  **dist/index.html**（手动 HTML）：

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <title>Webpack 手动配置演示</title>
    </head>
    <body>
      <!-- 注意：这里暂时手动引入打包后的文件 -->
      <script src="./main.js"></script>
    </body>
    </html>
    ```

***

**步骤5：配置 Webpack 核心**

**webpack.config.js**：

```javascript
const path = require('path');

module.exports = {
  // 开发模式（不压缩代码）
  mode: 'development',

  // 入口文件路径
  entry: './src/index.js',

  // 输出配置
  output: {
    filename: 'main.js',          // 输出文件名
    path: path.resolve(__dirname, 'dist'),  // 输出目录
    clean: true                   // 每次构建前清理 dist 目录（Webpack 5 新增）
  }
};
```

**配置解析**：

| 配置项      | 作用说明                                 |
| -------- | ------------------------------------ |
| `mode`   | 控制构建模式，`development` 会保留源码映射，不压缩代码   |
| `entry`  | 定义打包入口文件，Webpack 从这里开始分析依赖           |
| `output` | 指定输出位置和文件名，`path.resolve()` 用于处理绝对路径 |

***

**步骤6：添加打包脚本**

修改 **package.json**：

```json
{
  "scripts": {
    "build": "webpack --config webpack.config.js"
  }
}
```

**执行构建**：

```bash
npm run build
```

**预期输出**：

```
asset main.js 1.25 KiB [emitted] (name: main)
runtime modules 670 bytes 3 modules
cacheable modules 155 bytes
  ./src/index.js 155 bytes [built] [code generated]
webpack 5.xx.x compiled successfully in 123 ms
```

***

**步骤7：验证结果**

1. 用浏览器打开 **dist/index.html**
2. 页面应显示 "手动配置成功!"
3. 控制台输出 "Hello from Webpack!"

***

#### 🧪 **练习题与答案**

**练习1：修改入口文件**

1.  创建一个新文件 `src/hello.js`：

    ```javascript
    export const greet = () => {
      console.log('这是动态导入的模块！');
    };
    ```
2.  修改 `src/index.js`：

    ```javascript
    import { greet } from './hello.js';

    greet(); // 调用新模块的方法
    document.body.innerHTML += '<p>动态加载测试</p>';
    ```
3. 重新运行 `npm run build`
4. 观察控制台和页面变化

**答案验证**：

* 打包后的 `main.js` 应包含两个模块的代码
* 浏览器控制台会输出两条信息

***

**练习2：故意制造错误**

1. 在 `webpack.config.js` 中注释掉 `entry` 配置
2. 运行 `npm run build`
3. 观察错误信息

**预期错误**：

```
ERROR in 
Configuration error: 
No entry configuration found
```

**解决方法**：

* 恢复 `entry` 配置
* 理解入口文件是 Webpack 的必需配置

***

**练习3：自定义输出文件名**

修改 `webpack.config.js` 的 `output.filename` 为 `[name].bundle.js`

**问题**：

* 打包后生成的文件名是什么？
* 为什么需要这样命名？

**答案**：

1. 输出文件名为 `main.bundle.js`（因为默认入口名是 `main`）
2. 多入口时可通过 `[name]` 自动生成不同文件名

***

#### 🚨 **常见问题排查**

**问题1**：执行 `npm run build` 时报错 `Cannot find module 'webpack'` **原因**：未正确安装 Webpack **解决**：重新执行 `npm install webpack --save-dev`

**问题2**：浏览器打开 HTML 文件后无效果 **检查点**：

1. 打包是否成功完成（查看终端输出）
2. HTML 中引用的 JS 文件名是否与输出一致
3. 浏览器是否缓存了旧文件（尝试强制刷新 Ctrl+F5）

***

#### 💡 **扩展思考**

1. 如果要在配置中添加更多入口文件（如 `app.js` 和 `admin.js`），需要修改哪些配置？
2. `mode: 'development'` 和 `mode: 'production'` 的输出有何本质区别？
3. 为什么说 `webpack-cli` 不是必需的核心依赖？

