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
        this.reject = this.reject.bind(this);
    }
    
    initValue() {
        // 初始化值
        this.status = 'pending' // 状态
        this.onFulfilledCallbacks = []; // +
        this.onRejectedCallbacks = []; // +
    }
    
    resolve(res) {
        if(this.status !== 'pending') {
            return;
        }
        this.status = 'fulfilled';
        this.results = res;
        while(this.onFulfilledCallbacks.length) { // +
            this.onFulfilledCallbacks.shift()(this.results); // +
        } // +
    }
    
    reject(err) {
        if(this.status !== 'pending') {
            return;
        }
        this.status = 'rejected';
        this.results = err;
        while(this.onRejectedCallbacks.length) { // +
            this.onRejectedCallbacks.shift()(this.results); // +
        } // +
    }
    
    then(onFulfilled, onRejected) {
        // 类型判断
        onFulfilled = typeof onFulfilled === 'function' ? onFulfilled : _ => _;
        onRejected = typeof onRejected === 'function' ? onFulfilled : _ => _;
        if(this.status === 'fulfilled') {
            onFulfilled(this.results);
        } else if(this.status === 'rejected') {
            onRejected(this.results);
        } else if(this.status === 'pending') { // +
            this.onFulfilledCallbacks.push(onFulfilled.bind(this)); // +
            this.onRejectedCallbacks.push(onRejected.bind(this)); // +
        }
    }
}
```
{% endcode %}

3. `then`的链式调用
   * `.then`的返回结果仍为`Promise`
   * `then`回调函数参数返回结果如果是`Promise`则直接返回，否则返回被格式化为`Promise`的结果

{% code title="" overflow="wrap" lineNumbers="true" %}
```javascript
then(onFulfilled, onRejected) {
    // 类型判断
    onFulfilled = typeof onFulfilled === 'function' ? onFulfilled : _ => _;
    onRejected = typeof onRejected === 'function' ? onFulfilled : _ => _;
    
    const thenPromise = new _Promise((resolve, reject) => {
        const promiseResolver = (callback) => {
            // setTimeout模拟事件循环 
            setTimeout(() => {
                try {
                    const x = callback(this.results);
                    // Promises/A+规范规定 x!==thenPromise
                    if(x === thenPromise) {
                        throw new Error('x cannot be equal to thenPromise');
                    }
                    // x 回调结果仍为Promise
                    if(x instanceof _Promise) {
                        x.then(resolve, reject);
                    } else {
                        resolve(x);
                    }
                } catch (err) {
                    reject(err);
                    throw new Error(err);
                }
            })
        }
    });
    return thenPromise
}
```
{% endcode %}

#### `catch`

1. 是`.then`的语法糖；
2. 相当于`.then(undefined, onRejected)`

{% code title="" overflow="wrap" lineNumbers="true" %}
```javascript
catch(onRejected) {
    return this.then(undefined, onRejected)
}
```
{% endcode %}

#### `all`

{% code title="" overflow="wrap" lineNumbers="true" %}
```javascript
```
{% endcode %}



{% embed url="https://www.yuque.com/lpldplws/atomml/gtn6hvlf3fh1gl6e?singleDoc=" %}
CDIK
{% endembed %}

{% file src="../../.gitbook/assets/DAY_03前端异步处理规范及应用.pdf" %}
