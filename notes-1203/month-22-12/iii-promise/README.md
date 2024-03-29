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

1. 接收一个可迭代对象；
2. 所有`Promise`成功才成功；
3. 第一个错误出现后直接`reject`；

{% code title="" overflow="wrap" lineNumbers="true" %}
```javascript


Promises/A+ 规范解读
状态
Promise 有3个状态：pending fulfilled rejected；
状态可由pending 转为fulfilled或rejected，不可逆转且改变后不可再更改；
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
then
then接收两个回调onFulfilled, onRejected；
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
then内部接收异步处理；
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
then的链式调用
.then的返回结果仍为Promise
then回调函数参数返回结果如果是Promise则直接返回，否则返回被格式化为Promise的结果
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
catch
是.then的语法糖；
相当于.then(undefined, onRejected)
catch(onRejected) {
    return this.then(undefined, onRejected)
}
all
接收一个可迭代对象；
所有Promise成功才成功；
第一个错误出现后直接reject；
all(promises) {
    const tempResults = [];
    let counts = 0;
    let prevIndex = 0;
    return new _Promise((resolve, reject) => {
        try {
             const addData = (res, index) => {
                tempResults[index] = res;
                if(++counts === promises.length) {
                    resolve(tempResults);
                }
            }
            // 用 for···of 原生来判断是否是可迭代对象
            for(let promise of promises) {
                const index = prevIndex++;
                if(promise instanceof _Promise) {
                    promise
                        .then(res=>addData(res, index))
                        .catch(reject);
                } else {
                    addData(promise, index);
                }
            }
        } catch (err) {
            reject(err)
        }
    })
}
race
同样接收可迭代对象；
任意一个成功即返回成功；
任意一个失败即返回失败；
race(promise) {
    let prevIndex = 0;
    return new _Promise((resolve, reject) => {
        try {
            // 用 for···of 原生来判断是否是可迭代对象
            for(let promise of promises) {
                const index = prevIndex++;
                if(promise instanceof _Promise) {
                    promise.then(resolve, reject)
                } else {
                    resolve(promise);
                }
            }
        } catch (err) {
            reject(err);
        }
    })
}
allSettled
接收可迭代对象；
不论失败/成功，直到所有promise执行完后再返回结果数组；
返回的数组status存储promise执行状态，value存储成功结果，reason存储失败原因；
不论是否全部成功/失败，返回的Promise状态都是fulfilled；
allSettled(promises) {
    const tempResults = [];
    this.counts = 0;
    this.prevIndex = 0;
    
    return new _Promise((resolve, reject) => {
        const addData = (res, index) => {
            tempResults[index] = res;
            if(++counts === promises.length) {
                resolve(tempResults);
            }
        }
        for(let promise of promises) {
            const index = prevIndex++;
            if(promise instanceof _Promise) {
                promise
                    .then(value => addData({
                        status: 'fulfilled',
                        value
                    },index))
                    .catch(reason => addData({
                        status: 'rejected',
                        reason
                    }))
            } else {
                addData({
                    status: 'fulfilled',
                    value: promise
                },index)
            }
        }
    })    
}
any
接收可迭代对象；
任意一个成功即为成功；
全部失败则为失败；
any(promises) {
    const errors = [];
    let prevIndex = 0;
    return new _Promise((resolve, reject) => {
        for (let promise of promises) {
            const index = prevIndex++;
            if(promise instanceof _Promise) {
                promise
                    .then(resolve)
                    .catch((err) => {
                        errors[index] = err;
                        if(prevIndex === promises.length) {
                        reject(new AggregateError(errors, 'All promises were rejected'))
                        }
                    })
            } else {
                resolve(promise);
            }
        } 
    })
}
Async/Await
是generator的语法糖。
利用 generator/yield表达式实现async/await
思路：
利用HOC对generator函数进行封装处理；
自动执行传入的generator函数；
返回Promise结果；
function generator2Async(generator) {
    return function() {
        // 绑定this 只为纠正this指向，在不考虑使用this时，不绑定this也可以。
        const gen = generator.apply(this, arguments);
        return new Promise((resolve, reject) => {
            try {
                const autoRun = (key, args) => {
                    let res;
                    try {
                        res = gen[key](args);
                    } catch(err) {
                        return reject(err)
                    }
                    const { done, value } = res;
                    if(done) {
                        resolve(value);
                    } else {
                        return Promise
                            .resolve(value)
                            // 继续向下next
                            .then(res => autoRun('next', value))
                            // 调用generator内部throw方法
                            .catch(err => autoRun('throw', err));
                    }
                }
                autoRun('next');
            } catch (err) {
                reject(err);
            }
        })
    }
}




CDIK


```
{% endcode %}

#### `race`

1. 同样接收可迭代对象；
2. 任意一个成功即返回成功；
3. 任意一个失败即返回失败；

{% code title="" overflow="wrap" lineNumbers="true" %}
```javascript
race(promise) {
    let prevIndex = 0;
    return new _Promise((resolve, reject) => {
        try {
            // 用 for···of 原生来判断是否是可迭代对象
            for(let promise of promises) {
                const index = prevIndex++;
                if(promise instanceof _Promise) {
                    promise.then(resolve, reject)
                } else {
                    resolve(promise);
                }
            }
        } catch (err) {
            reject(err);
        }
    })
}
```
{% endcode %}

#### `allSettled`

1. 接收可迭代对象；
2. 不论失败/成功，直到所有`promise`执行完后再返回结果数组；
3. 返回的数组`status`存储`promise`执行状态，`value`存储成功结果，`reason`存储失败原因；
4. 不论是否全部成功/失败，返回的Promise状态都是`fulfilled`；

{% code title="" overflow="wrap" lineNumbers="true" %}
```javascript
allSettled(promises) {
    const tempResults = [];
    this.counts = 0;
    this.prevIndex = 0;
    
    return new _Promise((resolve, reject) => {
        const addData = (res, index) => {
            tempResults[index] = res;
            if(++counts === promises.length) {
                resolve(tempResults);
            }
        }
        for(let promise of promises) {
            const index = prevIndex++;
            if(promise instanceof _Promise) {
                promise
                    .then(value => addData({
                        status: 'fulfilled',
                        value
                    },index))
                    .catch(reason => addData({
                        status: 'rejected',
                        reason
                    }))
            } else {
                addData({
                    status: 'fulfilled',
                    value: promise
                },index)
            }
        }
    })    
}
```
{% endcode %}

#### `any`

1. 接收可迭代对象；
2. 任意一个成功即为成功；
3. 全部失败则为失败；

{% code title="" overflow="wrap" lineNumbers="true" %}
```javascript
any(promises) {
    const errors = [];
    let prevIndex = 0;
    return new _Promise((resolve, reject) => {
        for (let promise of promises) {
            const index = prevIndex++;
            if(promise instanceof _Promise) {
                promise
                    .then(resolve)
                    .catch((err) => {
                        errors[index] = err;
                        if(prevIndex === promises.length) {
                        reject(new AggregateError(errors, 'All promises were rejected'))
                        }
                    })
            } else {
                resolve(promise);
            }
        } 
    })
}
```
{% endcode %}

### `Async/Await`

是`generator`的语法糖。

#### 利用 `generator/yield`表达式实现`async/await`

_思路：_

1. 利用`HOC`对`generator`函数进行封装处理；
2. 自动执行传入的`generator`函数；
3. 返回`Promise`结果；

{% code title="" overflow="wrap" lineNumbers="true" %}
```javascript
function generator2Async(generator) {
    return function() {
        // 绑定this 只为纠正this指向，在不考虑使用this时，不绑定this也可以。
        const gen = generator.apply(this, arguments);
        return new Promise((resolve, reject) => {
            try {
                const autoRun = (key, args) => {
                    let res;
                    try {
                        res = gen[key](args);
                    } catch(err) {
                        return reject(err)
                    }
                    const { done, value } = res;
                    if(done) {
                        resolve(value);
                    } else {
                        return Promise
                            .resolve(value)
                            // 继续向下next
                            .then(res => autoRun('next', value))
                            // 调用generator内部throw方法
                            .catch(err => autoRun('throw', err));
                    }
                }
                autoRun('next');
            } catch (err) {
                reject(err);
            }
        })
    }
}
```
{% endcode %}







{% embed url="https://www.yuque.com/lpldplws/atomml/gtn6hvlf3fh1gl6e?singleDoc=" %}
CDIK
{% endembed %}

{% file src="../../../.gitbook/assets/DAY_03前端异步处理规范及应用.pdf" %}
