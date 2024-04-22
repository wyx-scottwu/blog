# 手写bind

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// bind
function.prototype._bind = function (f, target) {
    if(!target instanceof Object) 
        throw new TypeError("Target must be object");
    return function(...args) {
        const targetCopy = new Object(target);
        targetCopy.__TEMP_FN__ = f;
        const res = targetCopy.__TEMP_FN__(...args);
        return res;
    }
}
```
{% endcode %}
