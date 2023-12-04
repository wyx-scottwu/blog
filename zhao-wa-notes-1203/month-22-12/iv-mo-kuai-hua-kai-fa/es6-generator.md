# es6-generator

## **前言**

  在各路文档中，了解到 `Generator` 是一个生成器，目的是为了生成一个 `Iterator` -- `"迭代器"`，用以进行流程控制，让代码在你需要停止的地方提下来，并能够在下次流程进行的时候在上次停止的地方开始。

  其中有几个重要的名次及其概念列举如下：

*   `Generator` 其译为生成器，目的是为了通过其创建一个迭代器，声明方法如下👇；

    ```javascript
    function * generatorFun(){} // 或
    function* generatorFun(){} // 或
    function *generatorFun(){} // 或
    function* generatorFun(){}
    ```

    其中 `*` 的位置并没有强制限制，只要保证在 `function` 与生成器名称之间就可以了。
*   `next()` 为获取迭代器执行结果的方法，主要用法如下：

    ```javascript
      function * generatorFun(){
        yield 1;
      };
      const gf = generatorFun();
      gf.next();  // { value:1, done: false }
    ```

    需要注意的是，直接调用 `generatorFun`，并不能像常规函数那样直接获取函数执行结果，而是获得了一个迭代器 `Iterator`，在找到的一些文章中，大多愿意称其为指向函数内部状态的 `指针对象`，当调用迭代器对象内的 `next` 方法时，其指针便会从函数头部或上一次停下来的地方继续执行；
*   `yield` 其译为产出，产出的是其后面的表达式的运行结果，然后在 `yield` 处暂停执行，直到下次调用 `next` 方法触发才会在停止处继续执行，且当 `yield` 用在表达式中时，需要放在圆括号里，如下，：

    ```javascript
    function* demo() {
      console.log('Hello' + yield); // SyntaxError
      console.log('Hello' + yield 'world'); // SyntaxError

      console.log('Hello' + (yield)); // OK
      console.log('Hello' + (yield 'world')); // OK
    }
    ```

## **基本用法**

  从上述描述中基本可以了解到 `Generator` 的基本用法如下👇图所示。

  其中有这么几个需要注意的点[\[1\]](broken-reference)：

* 如上图中的代码，即使只有一个 `yield`，当第一次调用 `gf.next()` 也并没有直接到 `done` 的状态，这其实比较好理解，因为第一次的 `next` 并没有使代码运行到函数尾部，而是停留在了 `yield` 上，尽管 `yield` 之后再无可执行代码；
* 生成器函数执行流程区别于普通函数，举个🌰：  从上图可以看到，普通函数与生成器函数的执行顺序主要区别在于 `yield` 表达式使得每一次调用 `next` 最终都会将函数暂停在 `yield` 表达式或者函数尾部，直到下次调用 `next` 将从上一个 `yield` 运行到下一个 `yield` 或者函数尾部。
*   从上图的生成函数代码中会发现一个问题，就是最后的输出结果是 `NaN`，这其实是因为 `yield` 只负责`“产出”`导致的，也就是 `yield` 表达式并不能将它右侧的表达式运行结果返回到左侧，而如果需要上一步的结果，则可以借助 `next` 来进行传参，如下：

    ```javascript
    function * generatorFun(){
      ...
      const a = yield 1;
      console.log("🐛. a", a) // 2
      ...
    }
    const gf = generatorFun();
    const a = gf.next();
    gf.next(a + 1);
    ```

## **进阶**

### **`for of`**

  `for of` 循环可以自动遍历 `Generator` 函数时生成的 `Iterator` 对象，且此时不再需要调用 `next` 方法。如下：

```javascript
function * for0f(){
  yield 'hello';
  yield ' ';
  yield 'world';
  return ' javascript';
}
for(let v of for0f()){
  console.log("🐛. ~ v", v)
} // 'hello', ' ', 'world'
```

  通过观察输出结果，我们发现一个问题，就是最后的 `javascript` 并没有输出出来，这是因为 `for of` 循环在 `done === true` 时便中止掉了，并且不会返回当前结果，所以最后的 `return` 结果并没有获取到。

  除了 `for...of` 循环以外，扩展运算符（`...`）、解构赋值和 `Array.from`[\[2\]](broken-reference) 方法内部调用的，都是遍历器接口。这意味着，它们都可以将 `Generator` 函数返回的 `Iterator` 对象，作为参数。[\[3\]](broken-reference)

```javascript
function * for0f(){
  yield 'hello';
  yield ' ';
  yield 'world';
  return ' ';
  yield 'javascript';
}

// for...of 循环
for (let i of for0f()) {
  console.log(i)
}
// 'hello', ' ', 'world'

// 扩展运算符
[...for0f()] // ['hello', ' ', 'world]

// 解构赋值
let [x, y, z] = for0f();
x // 'hello'
y // ' '
z // 'world'

// Array.from 方法
Array.from(for0f()) // ['hello', ' ', 'world]
```

### **`Generator.prototype.throw()`**

  一个在生成器函数外部向函数体内部抛出错误的方法。

### **`Generator.prototype.return()`**

  一个在生成器函数外部向函数体内部 `return`，并终结遍历。

### **`yield*`**

  `yield*` 表达式用于委托给另一个 `generator` 或 `可迭代对象`[\[4\]](broken-reference)。[\[5\]](broken-reference)

  `yield*` 有区别于 `yield`。`yield` 可以将其理解为暂停标识符，即在 `yield` 处开始或停止。而 `yield*` 则可以理解为展开一个可迭代对象进行迭代。举个🌰：

```javascript
function* gf1() {
  yield* gf2();
}
function* gf2() {
  yield 1;
  yield 2;
  return 3;
}
const iterable1 = gf1();
function demo() {
  iterable1.next();
}
```



  上述代码其实可以看作等价于下面的代码

```javascript
function* gf1() {
  yield 1;
  yield 2;
  yield_return 3;
}
const iterable1 = gf1();
function demo() {
  iterable1.next();
}
```

  只不过有一条需要注意的是 `yield_return` 是我为了方便理解自己定义的一个标识，实际上是没有这个东西的。之所以这么定义是因为 `yield*` 所委托的迭代对象 `return` 的 `value` 将作为返回值返回到 `yield*` 表达式上，再举个🌰：

```javascript
function* gf1() {
  const v = yield* gf2();
  console.log("🐛. ~ function*gf1 ~ v", v)  // 🐛. ~ function*gf1 ~ v,3
}
function* gf2() {
  return 3;
}
const iterable1 = gf1();
function demo() {
  iterable1.next();
}
```



> 参考资料:
>
> \[1]. [es 异步流程(二)之generator篇](https://blog.csdn.net/weixin\_39798049/article/details/87111633)
>
> \[2]. [Array.from](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/Array/from)
>
> \[3]. [ES6中的Generator函数](https://www.jianshu.com/p/56000dcf7cfe)
>
> \[4]. [JS 可迭代对象](https://juejin.cn/post/6873457657018728456)
>
> \[5]. [yield\*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/yield\*)
>
> \[6]. [Markdown syntax](http://www.markdown.cn/)



**以上描述及解决方案均属个人观点，若您存在任何疑问及意见，还请联系本人** [**✉️ 邮箱**](mailto:wyx.scottwu@gmail.com)**。**
