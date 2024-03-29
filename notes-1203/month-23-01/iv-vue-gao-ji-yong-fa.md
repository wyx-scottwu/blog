---
description: Vue
---

# IV Vue 高级用法

### `vuex` 与 `mixin`的区别

> [`vuex`](https://vuex.vuejs.org/zh/guide/)vue`状态管理工具`
>
> `mixin` 一个用以服用状态以及逻辑的`api`

#### `mixin`用法

{% code title="" overflow="wrap" lineNumbers="true" %}
```javascript
export const mixinName = {
    data() {
        // ...data,
    },
    created() {
        // ...created actions
    }
}

// in .vue components
// ...
// </template>
import { mixinName } from 'mixin-path';
<script>
export default {
    mixins: [mixinName],
    // ...
}
</script>
// in global


```
{% endcode %}

{% embed url="https://www.yuque.com/lpldplws/web/ck0csfxciuzol315?singleDoc=" %}
