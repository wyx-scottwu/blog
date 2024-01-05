# animate

`animateName`

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
