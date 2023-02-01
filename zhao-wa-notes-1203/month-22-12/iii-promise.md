# III Promise

<figure><img src="https://picx.zhimg.com/80/v2-fbfef3cba00cd5e6a0e529a32676d9fa_720w.webp?source=1940ef5c" alt=""><figcaption></figcaption></figure>

### `Promises/A+` 规范解读

#### 状态

* `Promise` 有`3`个状态：`pending` `fulfilled` `rejected`；
* 状态可由`pending` 转为`fulfilled`或`rejected`，不可逆转且改变后不可再更改；

{% code title="" overflow="wrap" lineNumbers="true" %}
```javascript
class _Promise {
    constructor(exculator) {
        this.initValue();
        this.initBind();
        try {
            exculator(this.resolve, this.reject);
        } catch (e) {
            this.reject(e)
        }
    }
    
    initBind() {
        // 初始化this
        this.resolve = this.resolve.bind(this);
        this.reject = this.reject.bind(this)
    }
    
    initValue() {
        // 初始化值
        this.status = 'pending' // 状态
    }
    
    resolve(res) {
        if(this.status !== 'pending') {
            return;
        }
        this.status = 'fulfilled';
        this.results = res;
    }
    
    reject(err) {
        if(this.status !== 'pending') {
            return;
        }
        this.status = 'rejected';
        this.results = err;
    }
}
```
{% endcode %}

#### `then`

1. `then`接收两个回调`onFulfilled, onRejected`；

{% code title="" overflow="wrap" lineNumbers="true" %}
```javascript
then(onFulfilled, onRejected) {
    // 类型判断
    onFulfilled = typeof onFulfilled === 'function' ? onFulfilled : _ => _;
    onRejected = typeof onRejected === 'function' ? onFulfilled : _ => _;
    if(this.status === 'fulfilled') {
        onFulfilled(this.results);
    } else if(this.status ==='rejected') {
        onRejected(this.results);
    }
}
```
{% endcode %}

2. `then`内部接收异步处理；

{% code title="" overflow="wrap" lineNumbers="true" %}
```javascript
```
{% endcode %}







{% embed url="https://www.yuque.com/lpldplws/atomml/gtn6hvlf3fh1gl6e?singleDoc=" %}
CDIK
{% endembed %}

{% file src="../../.gitbook/assets/DAY_03前端异步处理规范及应用.pdf" %}
