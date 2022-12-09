---
description: 1/2
---

# I JavaScript 高级用法

<figure><img src="https://picx.zhimg.com/80/v2-eb49ab1ef23e8447c37c059344f359ea_720w.webp?source=1940ef5c" alt=""><figcaption></figcaption></figure>

### I 原型相关

#### protoType

#### **proto**

**proto** 指向原型对象的prototType

**总结⬆️：**

1. 原型对象的 `protoType` === 示例对象的`__proto__`
2. 实例对象的 `constructor/__proto__.constructor` 指向 原型对象

### II 作用域相关

#### 词法作用域 -- 定义 时确定

#### 动态作用域 -- 运行时确定

#### 执行上下文

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

#### 执行上下文栈

```javascript
// 不知所云。。。
// 看不到重点，讲不到场景，垃圾
// 毫无章法，毫无重点
```

#### 变量对象？？？？？

`JavaScript` 执行代码会创建执行上下文。 其包含如下三个属性：

* 变量对象(上下文相关联的作用域)
* 作用域链
* `this`

**变量对象** 是与执行上下文相关的数据作用域，存储上下文中定义的变量和函数声明。

**变量对象** 又可细分为如下两点。

**全局上下文变量**

全局对象，`window / global`

**函数上下文变量**

`activation object` -- `AO` 活动对象。

_个人理解：_ 活动对象是变量对象的可访问的版本。

> TIPS: 变量对象是规范或引擎上实现的，是不能在 `JavaScript` 环境中访问的。只有进入执行上下文，这个执行上下文中的变量对象才会被激活并可以被访问使用，而被激活后的变量对象也就称之为 活动对象 -- `AO`

> TIPS 💡
>
> * [先早 personal-blog](https://github.com/xianzao/xianzao-interview/issues)

***

**以上描述及解决方案均属个人观点，若您存在任何疑问及意见，还请联系本人** [**✉️ 邮箱**](mailto:wyx.scottwu@gmail.com)**。**

{% file src="../../.gitbook/assets/DAY_02JavaScript高级用法(2_2).pdf" %}
