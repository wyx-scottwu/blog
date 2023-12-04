# III Vue 基础

### [`mvc`](../../notes/concept/mvc-and-mvvm.md#mvc)&#x20;

### [`mvvm`](../../notes/concept/mvc-and-mvvm.md#mvvm)

### 生命周期



<table><thead><tr><th width="187">生命周期</th><th>描述</th><th></th></tr></thead><tbody><tr><td><code>beforeCreate</code></td><td></td><td></td></tr><tr><td><code>created</code></td><td></td><td></td></tr><tr><td><code>beforeMount</code></td><td></td><td></td></tr><tr><td><code>mounted</code></td><td></td><td></td></tr><tr><td><code>beforeUpdate</code></td><td></td><td></td></tr><tr><td><code>updated</code></td><td></td><td></td></tr><tr><td><code>beforeDestroy</code></td><td></td><td></td></tr><tr><td><code>destroyed</code></td><td></td><td></td></tr></tbody></table>

### 其他

#### `v-for`  `v-if` 优先级

`vue2:` `v-for` 优先级高于`v-if`当两者存在于同一`dom`节点时，`v-if`作用于其子节点。

`vue3:` `v-if`都作用于当前`dom`节点，`v-if`优先级高于`v-for`

#### `dom diff`

关于`dom`节点上的`key`

1. 不要使用`index`。因为index顺序始终不会变，当使用`index`作为`key`且`dom`顺序发生变化后，将有可能使得错误的渲染结果出现。
2. 尽量不要用`random`值，`random`值使得每次生成节点的`key`都是变化的，就导致了每次都会重新渲染`dom`，那么`diff`就是去了其原本的意义与价值。
3. 尽量使用静态的值，即这个`key`只会对应这个节点，或者说这个`key`对应的渲染结果始终是这个。

#### 模版语法

`{{  }}`内可以填充任意[`JavaScript`表达式](../../notes/javascript/javascript-biao-da-shi.md)



{% file src="../../.gitbook/assets/Vue基础.pdf" %}
