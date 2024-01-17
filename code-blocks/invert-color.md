---
description: Invert color with tinycolor2
---

# ❔ Invert Color

{% code title="invert-color.js" overflow="wrap" lineNumbers="true" %}
```javascript
import tinycolor from "tinycolor2";

export default function (_color) {
  const originColor = tinycolor(_color).toRgb();
  const invertedColor = {
    r: 255 - originColor.r,
    g: 255 - originColor.g,
    b: 255 - originColor.b,
  }
  return tinycolor(invertedColor).toHexString()
}
```
{% endcode %}
