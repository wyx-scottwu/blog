# IV 模块化开发

<figure><img src="https://pic1.zhimg.com/80/v2-ac1cc476379c858ef58a965839cdb7ab_720w.webp?source=1940ef5c" alt=""><figcaption></figcaption></figure>

### `CommonJS`

* `CommonJS`模块的加载机制是，输⼊的是被输出的值的拷⻉。也就是说，⼀旦输出⼀个值，模块内部的 变化就影响不到这个值。
*

### `AMD`

```javascript
// define 定义
define(['require-module-name'], function() {
    return { ... }
})
// require 引入

```

### `CMD`





{% file src="../../../.gitbook/assets/DAY_04前端模块化.pdf" %}
