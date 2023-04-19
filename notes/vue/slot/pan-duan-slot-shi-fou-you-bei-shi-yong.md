# 判断slot是否有被使用

在子组件中，可以通过 `$slots` 对象来判断插槽是否被使用。`$slots` 对象是一个包含了插槽内容的键值对对象，其中键是插槽名称，值是插槽内容。如果插槽没有被使用，则对应的值将为 `undefined`。

以下是一个示例，演示如何在子组件中判断插槽是否被使用：

```vue
vueCopy code<template>
  <div>
    <div v-if="$slots.header">
      <slot name="header"></slot>
    </div>
    <div v-else>
      <!-- 显示默认标题 -->
      <h2>{{ title }}</h2>
    </div>
    <div>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: 'Default Title'
    }
  }
}
</script>
```

在上面的示例中，我们在子组件中使用了两个插槽：一个具名插槽 `header` 和一个默认插槽。我们使用 `$slots` 对象来判断 `header` 插槽是否被使用。如果 `header` 插槽被使用，我们将渲染插槽内容，否则将显示默认标题。

注意，`$slots` 对象只包含当前组件中的插槽内容。如果您想要访问父组件中的插槽内容，您可以使用 `$parent.$slots` 对象来访问。
