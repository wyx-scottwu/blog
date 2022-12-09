---
description: 2/2
---

# II JavaScript 高级用法

<figure><img src="https://pica.zhimg.com/80/v2-32cd3feef8b961e3c9d8a6cb673028be_720w.webp?source=1940ef5c" alt=""><figcaption></figcaption></figure>

### JavaScript 数据类型

基本类型：存储在栈，传递的是当前的值，修改不会影响原先的值；

引用类型：索引的引用地址，存储在栈，其值存储在堆中。

### 手写 `call` / `apply` / `bind`

```js
Function.prototype._call = function () {
  const [caller, ...args] = arguments;

  caller._callFn = this;

  const res = caller._callFn(...args);

  delete caller._callFn;

  return res;
}
```

`bind` 参数略有区别，会合并参数

```javascript
Function.prototype.bind = function () {
  const calledFn = this;
  const [binder, ...args] = arguments;

  const bindFn = function () {
    return calledFn.call(
      // 判断是否 被当作了构造函数
      this instanceof bindFn ? this : binder,
      ...arguments,
      ...args)
  }
  // 继承调用者的原型。
  bindFn.prototype = this.prototype;
  return bindFn;
}
```

### `new`

```javascript


```

### 类数组

只有基本元素及`length`属性

> #### 小记
>
> **`slice`  `splice` 区别⬇️**
>
> * `slice` 不改变原数组，`slice` 仅读取
> * `splice` 改变原数组，`splice` 支持替换
>
> **`arguments.callee`**
>
> 函数自身

***

**以上描述及解决方案均属个人观点，若您存在任何疑问及意见，还请联系本人** [**✉️ 邮箱**](mailto:wyx.scottwu@gmail.com)**。**

{% file src="../../.gitbook/assets/DAY_02JavaScript高级用法(2_2).pdf" %}
