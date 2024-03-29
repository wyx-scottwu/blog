---
description: 基于vue-plugin-hiprint
---

# 🖨️ Hiprint

### 🕳️ I: Hiprint初始化

```javascript
import { defaultElementTypeProvider } from 'vue-plugin-hiprint'
hiprint.init({
    /** 
    * provider 支持配置多个，且可自定义，具体可参考源代码
    * hiprint官方默认providers配置变量名为customElementTypeProvider
    */
    providers: [new defaultElementTypeProvider()],
})
```

* [ ] Note: 需要确认provider配置的内容是否需要和`hiprint.PrintElementTypeManager.buildByHtml()`所绑定的保持一致

### 🕳️ II: Hiprint 标尺显示配置

需要手动给 `hiprintTemplate.design`所处容器加`padding`后才能正常显示标尺

### 🕳️ III: 控制网格背景显隐

`hiprintTemplate.design('', {grid:true|false})`



`editable`属性只限`table`类型使用



