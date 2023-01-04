---
description: OOP / ProtoType
---

# II OOP / protoType

<figure><img src="https://pica.zhimg.com/80/v2-32cd3feef8b961e3c9d8a6cb673028be_720w.webp?source=1940ef5c" alt=""><figcaption></figcaption></figure>

### JavaScript 数据类型

基本类型：存储在栈，传递的是当前的值，修改不会影响原先的值；

引用类型：索引的引用地址，存储在栈，其值存储在堆中。

### 手写 `call` / `apply` / `bind`

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Function.prototype._apply = function () {
Function.prototype.__call = function () {
  // const [caller, args] = arguments;
  const [caller, ...args] = arguments;

  caller._callFn = this;
  const res = caller._callFn(...args);

  delete caller._callFn;

  return res;
}
```
{% endcode %}

#### `bind - 1` 参数略有区别，会合并参数

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// 先实现普通版 bind
Function.prototype.__bind = function () {
  const calledFn = this;
  const [binder, ...args] = arguments;

  const bindFn = function () {
    return calledFn.call(
      // 判断是否 被当作了构造函数
      binder,
      ...args,
      ...arguments,
    )
  }
  return bindFn;
}
```
{% endcode %}

#### `bind - 2` `bind`后的函数还可以作为`构造器`使用 _这该如何实现？_

`bind - 2` 实现前要先看下`new`是如何实现的或者其内部的机制如何

> ```javascript
> // 构造函数 Foo() { ... }
> ```
>
> 当代码 `new Foo(...)` 执行时，会发生以下事情：
>
> 1. 一个继承自 `Foo.prototype` 的新对象被创建。
> 2. 使用指定的参数调用构造函数 _`Foo`_，并将 [`this`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this) 绑定到新创建的对象。
>    * `new Foo` 等同于 _`new Foo`_`()`，也就是没有指定参数列表，_`Foo`_ 不带任何参数调用的情况。
> 3. 由构造函数返回的对象就是 `new` 表达式的结果。如果构造函数没有显式返回一个对象，则使用步骤 1 创建的对象。（一般情况下，构造函数不返回值，但是用户可以选择主动返回对象，来覆盖正常的对象创建步骤）
>
>
>
> 【参考链接】： [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new)

{% code overflow="wrap" lineNumbers="true" %}
```javascript
/**
 * 因为 new 为特殊操作符，所以用 function 来代替实现
 */

function operatorNew(_Constructor, ...args) {
  // 以 _Constructor.prototype 为原型创建空对象。
  const tempRes = Object.create(_Constructor.prototype);
  // 以新创建的空对象作为 this 调用构造函数 _Constructor
  const constructRes = _Constructor.apply(tempRes, args);
  // 判断构造函数返回结果是否为对象。  
  const realRes = typeof constructRes === 'object' 
    ? constructRes
    : tempRes;
  return realRes;
}
```
{% endcode %}

从上面代码的`7-9`行可以看出如下两个细节

1. 构造函数被调用时，需要接收新的`this`
2. 新的`this`是以构造函数原型为原型创建的

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// 改造如下⬇️
/**
 * ......
 * line 2 ～ line 5
 */ 
  const bindFn = function () {
    return calledFn.call(
      // 判断是否 被当作了构造函数
      this instanceof bindFn ? this : binder,
      ...args,
      ...arguments,
    )
  }
  bindFn.prototype = this.prototype
  return bindFn;
```
{% endcode %}

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
