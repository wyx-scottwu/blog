# 循环

在 Python 中，`for` 和 `while` 是两种主要的循环结构，但 Python 还提供了其他一些与循环相关的机制和技巧。以下是 Python 中循环的完整总结：

***

#### **1. `for` 循环**

`for` 循环用于遍历可迭代对象（如列表、元组、字符串、字典、集合等）。

**语法**

```python
for item in iterable:
    # 循环体
```

**示例**

```python
for i in range(5):
    print(i)  # 输出 0, 1, 2, 3, 4
```

***

#### **2. `while` 循环**

`while` 循环在条件为真时重复执行代码块。

**语法**

```python
while condition:
    # 循环体
```

**示例**

```python
count = 0
while count < 5:
    print(count)  # 输出 0, 1, 2, 3, 4
    count += 1
```

***

#### **3. 循环控制语句**

Python 提供了以下循环控制语句：

* **`break`**：立即退出循环。
* **`continue`**：跳过当前迭代，进入下一次迭代。
* **`pass`**：占位符，不执行任何操作。

**示例**

```python
for i in range(5):
    if i == 3:
        break  # 退出循环
    print(i)  # 输出 0, 1, 2
```

***

#### **4. `else` 子句**

`for` 和 `while` 循环可以带有 `else` 子句，当循环正常结束（即没有通过 `break` 退出）时执行。

**示例**

```python
for i in range(5):
    print(i)  # 输出 0, 1, 2, 3, 4
else:
    print("Loop finished!")  # 输出 "Loop finished!"
```

***

#### **5. 列表推导式**

列表推导式是一种简洁的创建列表的方式，可以替代简单的 `for` 循环。

**示例**

```python
squares = [x**2 for x in range(5)]
print(squares)  # 输出 [0, 1, 4, 9, 16]
```

***

#### **6. 生成器表达式**

生成器表达式类似于列表推导式，但返回的是一个生成器对象，支持惰性求值。

**示例**

```python
squares = (x**2 for x in range(5))
for square in squares:
    print(square)  # 输出 0, 1, 4, 9, 16
```

***

#### **7. `map()` 和 `filter()`**

`map()` 和 `filter()` 是函数式编程工具，可以替代某些循环场景。

**示例**

```python
# 使用 map() 对列表中的每个元素应用函数
squares = map(lambda x: x**2, range(5))
print(list(squares))  # 输出 [0, 1, 4, 9, 16]

# 使用 filter() 过滤列表中的元素
evens = filter(lambda x: x % 2 == 0, range(5))
print(list(evens))  # 输出 [0, 2, 4]
```

***

#### **8. 递归**

递归是一种通过函数调用自身来实现循环的技术。

**示例**

```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)

print(factorial(5))  # 输出 120
```

***

#### **9. `itertools` 模块**

`itertools` 模块提供了许多高效的迭代工具，可以替代复杂的循环。

**示例**

```python
import itertools

# 无限循环
for i in itertools.count():
    if i > 3:
        break
    print(i)  # 输出 0, 1, 2, 3

# 循环遍历多个可迭代对象
for a, b in itertools.product([1, 2], ['a', 'b']):
    print(a, b)  # 输出 (1, 'a'), (1, 'b'), (2, 'a'), (2, 'b')
```

***

#### **总结**

Python 的主要循环结构是 `for` 和 `while`，但还提供了以下机制：

* 循环控制语句（`break`、`continue`、`pass`）。
* `else` 子句。
* 列表推导式和生成器表达式。
* `map()` 和 `filter()`。
* 递归。
* `itertools` 模块。

根据具体需求选择合适的循环方式即可！
