---
description: mock
---

# mock

> 【内容参考官方文档】：
>
> [https://cn.vitejs.dev/config/#conditional-config](https://cn.vitejs.dev/config/#conditional-config)

`vite` `mock`开关配置：

{% code overflow="wrap" lineNumbers="true" %}
```javascript
/** ... **/

viteMockServe({
    mockPath: 'mock',
    localEnabled: command === 'serve',     // 该 command 值在开发环境（即 CLI 命令 vite、vite dev 和 vite serve） 为 serve。

}),

/** ... **/
```
{% endcode %}
