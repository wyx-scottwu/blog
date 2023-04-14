# Node 部署

### `koa`洋葱模型

关于洋葱模型，个人理解递归更接近这个概念，都是先进后出的模式，只是`koa`的洋葱模型，它借助了`next()`来触发下一个“递归”的执行。

{% code title="1. 递归" overflow="wrap" lineNumbers="true" %}
```javascript
function test(index, max) {
  // console.log("𝔀𝔂𝔁.𝓼𝓬𝓸𝓽𝓽𝔀𝓾 ~ file: itest.js:2 ~ test ~ index:", index)
  const res = index === max ? "completed" : test(index + 1, max);
  // console.log("𝔀𝔂𝔁.𝓼𝓬𝓸𝓽𝓽𝔀𝓾 ~ file: itest.js:4 ~ test ~ index:", index)
  return res;
}

// console.log("𝔀𝔂𝔁.𝓼𝓬𝓸𝓽𝓽𝔀𝓾 ~ file: itest.js:9 ~ test(0, 10):", test(0, 10))
```
{% endcode %}

{% code title="2. koa 🧅模型" overflow="wrap" lineNumbers="true" %}
```javascript
```
{% endcode %}
