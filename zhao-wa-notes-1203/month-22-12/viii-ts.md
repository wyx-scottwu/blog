# VIII TypeScript（I）

<figure><img src="https://pic1.zhimg.com/80/v2-5a37ef0ee2a339e08a0a8c913d69f236_720w.webp?source=1940ef5c" alt=""><figcaption></figcaption></figure>

### `TS`基础类型

* `string` `number` `boolean` `array` `undefined` `null`
*   `Tuple`

    元组中规定的元素类型顺序必须是完全对照的，而且不能多、不能少；
*   `enum`

    {% code overflow="wrap" lineNumbers="true" %}
    ```typescript
    // 数字型枚举
    enum Test {
        enum0,
        enum1,
        enum2,
        enuma,
        enumb,
    }
    // 默认不对枚举赋值的情况下，其值为从 0 开始计数的数字

    enum Test1 {
        enum0,
        enum1,
        enum2,
        enuma = 'a',
        enumb, 
    }
    // 向上面这种情况下，ts 将会对 enumb 抛出错误，提示需要对 enumb 进行初始化，需要修改如下⬇️
    enum Test1 {
        enum0,
        enum1,
        enum2,
        enuma = 'a',
        // enumb, // enumb = 0|1|2.... 或者其他字符串，boolean 等等
        // 如果下方仍然有枚举且上方未设置为数字的情况下，仍需继续对其初始化设置。 
    }
    ```
    {% endcode %}







