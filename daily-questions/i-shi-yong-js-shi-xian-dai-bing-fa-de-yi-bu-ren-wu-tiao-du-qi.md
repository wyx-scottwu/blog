# 📝 I 使用JS实现带并发的异步任务调度器

### Q: 实现一个带并发限制的异步调度器 `Scheduler`，保证同时运行的任务最多有`N`个。完善下面代码中的 `Scheduler` 类，使得以下程序能正确输出：

{% code overflow="wrap" lineNumbers="true" %}
```javascript
class Scheduler {
  add(promiseCreator) { ... }
  // ...
}

const timeout = (time) => new Promise(resolve => {
  setTimeout(resolve, time)
})

const scheduler = new Scheduler(n)
const addTask = (time, order) => {
  scheduler.add(() => timeout(time)).then(() => console.log(order))
}

addTask(1000, '1')
addTask(500, '2')
addTask(300, '3')
addTask(400, '4')

// 打印顺序是：2 3 1 4
```
{% endcode %}

## A:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
class Scheduler {
  constructor(max) {
    this.max = max;
    this.count = 0;
    this.waitingQueue = [];
  }
  
  async add(promiseCreator) {
    if(typeof promiseCreator !== 'function') {
      throw new TypeError("promiseCreator is not a function");
    }
    
    if(this.count >= this.max) {
      // 在等待队列中push一个resolve
      // 等待上一个正在执行的任务执行完成后将其shift出并执行
      // 使代码继续向下执行
      await new Promise(resolve=> this.waitingQueue.push(resolve));
    }
    
    this.count++;
    // 定义返回值传回
    const res = await promiseCreator();
    this.count--;
    
    if(this.waitingQueue.length) {
      this.waitingQueue.shift()();
    }
    return res;
  }
}

const timeout = (time) => new Promise(resolve => {
  setTimeout(resolve, time)
})

const scheduler = new Scheduler(2)
const addTask = (time, order) => {
  scheduler.add(() => timeout(time)).then(() => {
    console.log(order);
  })
}

addTask(1000, '1')
addTask(500, '2')
addTask(300, '3')
addTask(200, '4')

// 打印顺序是：2 3 1 4
```
{% endcode %}

### Summary:

考点在于`promise`运行时机





{% embed url="https://github.com/xianzao/xianzao-interview/issues/1" %}
