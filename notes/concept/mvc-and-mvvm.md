---
description: 一文彻底搞懂 MVC 与 MVVM
---

# MVC & MVVM

## `MVC`

首先它是一种软件设计/架构模式，旨在根据不同代码的职责进行区分，来提高系统的可维护性与可扩展性。

* `Model:` 模型，通常指系统的数据部分；
* `View:` 视图，通常指用户界面；
* `Controller:` 控制器，个人理解为更新视图与更新数据的逻辑部分

<figure><img src="https://developer.mozilla.org/en-US/docs/Glossary/MVC/model-view-controller-light-blue.png" alt=""><figcaption></figcaption></figure>

## `MVVM`

`Modal`与`View`仍然是那个`Modal`与`View`而原本由`Controller`完成的事情交由了`ViewModal` 使得数据响应式的更新。\
`ViewModal` 实现了`Modal`与`View` 的双向绑定，使得数据更新能够自动触发视图更新，视图更新自动触发数据更新。





