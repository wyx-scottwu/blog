# animate

#### `animateName`

用于标识父元素需要动态改变的属性名

如下`demo`即表示动态改变`rect`元素的`rx`值

```html
<svg viewBox="0 0 10 10" xmlns="http://www.w3.org/2000/svg">
  <rect width="8" height="8">
    <animate
      attributeName="rx"
      values="0;5;0"
      dur="5s"
      repeatCount="indefinite" />
  </rect>
</svg>
```

#### `dur`

即`duration`，指每一次动画运行时间间隔，可用元素见[链接](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Element#animation)

默认`indefinite`，可以理解为没有运行时间，即不运行动画
