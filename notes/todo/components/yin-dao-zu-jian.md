# 引导组件

### 踩坑 1:&#x20;

使用`expo` 创建 `react native` 组件`demo`并运行，以 `pnpm` 作为包管理工具时运行报错：

`Error: Unable to resolve module ./node_modules/expo/AppEntry from *`

#### why？

据了解到，`react native`存在大量隐式依赖，`pnpm`默认不会拍平展开以来，便导致无法正常访问到`pnpm`所连接到的依赖

解决方案：

根目录下新建 `.npmrc`文件并添加如下代码，而后再次`pnpm install`

`node-linker=hoisted`

含义：创建无符号扁平 `node_modules`\
[https://pnpm.io/zh/npmrc#node-linker](https://pnpm.io/zh/npmrc#node-linker)

***
