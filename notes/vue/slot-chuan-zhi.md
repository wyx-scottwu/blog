# Slot 传值

在 Vue 3 中，父组件可以通过在子组件的 `<slot>` 标签上添加 `v-bind` 绑定来接收子组件通过插槽传递的数据。

假设子组件的模板如下所示：

```html
<template>
  <div>
    <slot message="Hello from child"></slot>
  </div>
</template>
```

在父组件中，可以使用 `v-slot` 或 `#` 来定义一个插槽，并在其中使用子组件的标签名，然后通过 `v-bind` 将子组件传递的数据绑定到父组件的模板中。例如：

```html
<template>
  <div>
    <child-component>
      <template v-slot:default="{ message }">
        <p>{{ message }}</p>
      </template>
    </child-component>
  </div>
</template>
```

或者，使用简写的 `#` 符号：

```html
<template>
  <div>
    <child-component>
      <template #default="{ message }">
        <p>{{ message }}</p>
      </template>
    </child-component>
  </div>
</template>
```

在上述例子中，`message` 是子组件传递给插槽的一个属性，可以在父组件的插槽模板中使用。父组件会渲染一个包含子组件传递的数据的 `<p>` 元素。
