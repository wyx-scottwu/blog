# IV 模块化开发

<figure><img src="https://pic1.zhimg.com/80/v2-ac1cc476379c858ef58a965839cdb7ab_720w.webp?source=1940ef5c" alt=""><figcaption></figcaption></figure>

### `CommonJS`

* `CommonJS`模块的加载机制是，输⼊的是被输出的值的拷⻉。也就是说，⼀旦输出⼀个值，模块内部的 变化就影响不到这个值。
* **特点：**
  * 所有代码都运⾏在模块作⽤域，不会污染全局作⽤域；&#x20;
  * 模块可以多次加载，但是只会在第⼀次加载时运⾏⼀次，然后运⾏结果就被缓存了，以后再加载， 就直接读取缓存结果。要想让模块再次运⾏，必须清除缓存；
  * 模块加载的顺序，按照其在代码中出现的顺序；

{% code title="基本用法" overflow="wrap" lineNumbers="true" %}
```javascript
// 导出语法
module.exports = value
// 或
exports.moduleName = value
// 需要注意的是
// 1. 当一个文件中有多个module.exports时，最后一个module.exports生效
// 2. 当一个文件中既有module.exports 又有 exports.moduleName 时，最后一个module.exports生效
// 3. 当一个文件中只有exports.moduleName 且有多个时，最终导出结果是导出的合并

// 导入语法
const moduleName = reuqire('module-path')
```
{% endcode %}

### `AMD`

```javascript
// define 定义
define(['dependencies1'], function(dependencies1) {
    return { ... }    // 暴露模块
})
或
define(function () {
    return { ... }    // 暴露模块
})

// require 引入
require(['dependencies1'], function(dependencies1) {
    // 使用dependencies1
    ...
})


// 入口文件配置
(()=>{
    require.config({
        baseUrl: 'js/', //基本路径 出发点在根⽬录下
        paths: {
            //⾃定义模块
            moduleName: './modulePath', //此处不能写成alerter.js,会报错
            // 第三⽅库模块
            jquery: './libs/jquery-1.10.1' //注意：写成jQuery会报错
        }
    })
})()

<script data-main="js/main" src="js/libs/require.js" />
```

### `CMD - sea.js`



> [**`ESM 是值的引用`**](../../notes/concept/esm-yu-commonjs-de-qu-bie.md)&#x20;
>
> [**`CommonJS 是值的拷贝`** ](../../notes/concept/esm-yu-commonjs-de-qu-bie.md)

{% file src="../../.gitbook/assets/DAY_04前端模块化.pdf" %}
