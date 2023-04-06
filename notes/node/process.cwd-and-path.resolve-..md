---
description: 一个有趣的问题
---

# process.cwd() & path.resolve('.')

现在有如下脚本文件

{% code title="/desktop/node/test1.js" overflow="wrap" lineNumbers="true" %}
```javascript
// ...
console.log('path.resolve', path.resolve('.'));
console.log('process.cwd', process.cwd());
// ...  
```
{% endcode %}

当我在其他位置如`/desktop/other`下通过命令行去执行上面的`js`脚本文件

{% code overflow="wrap" lineNumbers="true" %}
```shell
node /desktop/node/test1.js
```
{% endcode %}

那么得到的结果将是

{% code overflow="wrap" lineNumbers="true" %}
```sh
path.resolve /desktop/other
process.cwd /desktop/other
```
{% endcode %}

可我们又知道，`process.cwd()`是用来获取当前脚本执行的路经的，也就是说它的结果是没有问题的；

而`path.resolve('.')`它所应该返回的是`.`，也就是当前文件目录，可为什么也跟着返回了脚本所执行的位置的路经呢？

呐，原因呢就是 `path.resolve('.')` 返回的是 Node.js 进程的当前工作目录，而不是正在执行的脚本的目录。当在命令行中执行 `node` 命令时，Node.js 进程的当前工作目录通常是命令行所在的目录。因此，`path.resolve('.')` 返回的是该目录。
