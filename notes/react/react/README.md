# 🔗 react

`react` 如何防范 `xss`

`react` 天生会输入与输出的结果进行转义，即对标签等特殊字符进行转义，如下

{% code title="" overflow="wrap" lineNumbers="true" %}
```javascript
for(index = match.index; index<str.length; index++){
  switch (str.charCodeAt(index)){
    case 34: // "
      escape = "&quot;";
      break;
    case 38: // &
      escape = "&amp;";
      break;
    case 39: // '
      escape = "&#x27;";
      break;
    case 60: // <
      escape = "&lt;";
      break;
    case 62: // >
      escape = "&gt;";
      break;
    default:
       continue;
  }
}
```
{% endcode %}
