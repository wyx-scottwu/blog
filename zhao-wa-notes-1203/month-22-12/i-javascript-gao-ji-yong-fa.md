---
description: 1/2
coverY: 0
---

# I JavaScript 高级用法

<figure><img src="https://picx.zhimg.com/80/v2-df56f09828d6ca46e17eeecc619ce88f_720w.webp?source=1940ef5c" alt=""><figcaption></figcaption></figure>

### I 原型相关

#### I.I `prototype`

#### **I.II `__proto__`**

`__proto__` 指向原型对象的`prototype`

**总结⬆️：**

1. 原型对象的 `prototype` === 示例对象的`__proto__`
2. 实例对象的 `constructor/__proto__.constructor` 指向 原型对象

### II 作用域相关

#### II.I 词法作用域 -- 定义 时确定

#### II.II 动态作用域 -- 运行时确定

#### II.III 执行上下文

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// demo
var foo = function () {
  console.log("🚀 ~ file: 1203day01.md ~ line 33 ~ foo ~ 1", 1);
}
foo();
var foo = function () {
  console.log("🚀 ~ file: 1203day01.md ~ line 37 ~ foo ~ 2", 2);
}
foo();
function foo () {
  console.log("🚀 ~ file: 1203day01.md ~ line 41 ~ foo ~ 3", 3);
}
foo();
function foo () {
  console.log("🚀 ~ file: 1203day01.md ~ line 45 ~ foo ~ 4", 4);
}
foo();

// output ⬇️
1
2
2
2
```
{% endcode %}

{% code overflow="wrap" lineNumbers="true" %}
```javascript
/**
 *  解释 ⬇️
 * var function 均会变量提升
 * function 的提升会优先于 var 变量声明
 * 所以最终实际的运行过程如下面代码
 */

function foo () {
  console.log("🚀 ~ file: 1203day01.md ~ line 41 ~ foo ~ 3", 3);
}
function foo () {
  console.log("🚀 ~ file: 1203day01.md ~ line 45 ~ foo ~ 4", 4);
}
var foo = function () {
  console.log("🚀 ~ file: 1203day01.md ~ line 33 ~ foo ~ 1", 1);
}
foo();
var foo = function () {
  console.log("🚀 ~ file: 1203day01.md ~ line 37 ~ foo ~ 2", 2);
}
foo();
foo();
foo();

```
{% endcode %}

#### II.IV 执行上下文栈

```javascript
// 不知所云云。。。
```

#### II.V 变量对象？？？？？

`JavaScript` 执行代码会创建执行上下文。 其包含如下三个属性：

* 变量对象(上下文相关联的作用域)
* 作用域链
* `this`

_变量对象_ 是与执行上下文相关的数据作用域，存储上下文中定义的变量和函数声明。

_变量对象_ 又可细分为如下两点。

**II.VI 全局上下文变量**

全局对象，`window / global`

**II.VII 函数上下文变量**

`activation object` -- `AO` 活动对象。

_个人理解：_ 活动对象是变量对象的可访问的版本。

> TIPS: 变量对象是规范或引擎上实现的，是不能在 `JavaScript` 环境中访问的。只有进入执行上下文，这个执行上下文中的变量对象才会被激活并可以被访问使用，而被激活后的变量对象也就称之为 活动对象 -- `AO`

#### II.VII `this`

`this`获取步骤：

1. 将 `MemberExpression` 计算结果赋值给 `ref`
2. 判断 `ref` 是否是一个 `Reference`&#x20;
   * `ref` 是一个 `Reference`
     * `IsPropertyReference(ref)`结果为`true`时，`this` 即为 `GetBase(ref)`
     * 否则判断`base value` 值是否为`Environment Record`是则为 `ImplicitThisValue(ref)`
   * `ref` 不是一个 `Reference` `this`值为`undefined`

看到这里发现有这些未知的名词&#x20;

1. `MemberExpression这里就`简单理解 `()左边的部分吧。` &#x20;
2. `Reference`&#x20;
3. `GetBase`
4. `base value`
5. `Environment Record`
6. `ImplicitThisValue`

{% hint style="info" %}
此处参考这篇文章，能够更好的理解。[https://blog.csdn.net/qq\_39759115/article/details/78733251](https://blog.csdn.net/qq\_39759115/article/details/78733251)
{% endhint %}

#### 闭包

指能够访问自由变量的函数。

_自由变量_ 指在函数中使用，但不是函数参数，也不是函数局部变量的一种变量。











> TIPS 💡
>
> * [先早 personal-blog](https://github.com/xianzao/xianzao-interview/issues)
> * [React 学习路径](https://www.yuque.com/lpldplws/atomml/bgn3sl?singleDoc#%20%E3%80%8Areact%E5%AD%A6%E4%B9%A0%E8%B7%AF%E5%BE%84%E3%80%8B%20%E5%AF%86%E7%A0%81%EF%BC%9Aei05)
> * [JavaScript高级用法](https://www.yuque.com/lpldplws/atomml/tmbe7ykqmslqszhe?singleDoc=%E5%AF%86%E7%A0%81=bwxh)

{% hint style="info" %}
**以上描述及解决方案均属个人观点，若您存在任何疑问及意见，还请联系本人** [**✉️ 邮箱**](mailto:wyx.scottwu@gmail.com)**。**
{% endhint %}

{% file src="../../.gitbook/assets/DAY_01JavaScript高级用法(1_2).pdf" %}
