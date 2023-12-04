# 引导组件

踩坑1: 使用expo 创建 react native 组件demo并运行，以 pnpm 作为包管理工具时运行报错：

`Error: Unable to resolve module ./node_modules/expo/AppEntry from *`

why？

据了解到，react native 存在大量隐式依赖，pnpm 默认不会拍平展开以来，便导致无法正常访问到pnpm所连接到的依赖
