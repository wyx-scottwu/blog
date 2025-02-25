# 模式匹配

在 Python 3.10 中引入了 **`match` 语句**，它是一种强大的模式匹配工具，类似于其他语言中的 `switch` 语句，但功能更强大。`match` 语句可以用于匹配不同的模式，并根据匹配结果执行相应的代码块。

***

#### **`match` 语句的基本语法**

```python
match subject:
    case pattern1:
        # 处理 pattern1
    case pattern2:
        # 处理 pattern2
    case _:
        # 默认情况
```

* `subject`：需要匹配的对象。
* `pattern`：匹配的模式，可以是字面值、变量、类型、结构等。
* `_`：默认情况，类似于 `switch` 语句中的 `default`。

***

#### **`match` 的用法和场景**

**1. 匹配字面值**

匹配具体的值（如整数、字符串等）。

```python
def handle_status(status):
    match status:
        case 200:
            print("Success")
        case 404:
            print("Not Found")
        case 500:
            print("Server Error")
        case _:
            print("Unknown Status")

handle_status(200)  # 输出 "Success"
handle_status(404)  # 输出 "Not Found"
```

***

**2. 匹配类型**

匹配对象的类型。

```python
def handle_value(value):
    match value:
        case int():
            print("Integer")
        case str():
            print("String")
        case list():
            print("List")
        case _:
            print("Unknown Type")

handle_value(42)        # 输出 "Integer"
handle_value("Hello")    # 输出 "String"
handle_value([1, 2, 3])  # 输出 "List"
```

***

**3. 匹配结构**

匹配复杂的数据结构（如列表、字典等）。

```python
def handle_data(data):
    match data:
        case [x, y]:
            print(f"List with two elements: {x}, {y}")
        case {"name": name, "age": age}:
            print(f"Dictionary with name: {name}, age: {age}")
        case _:
            print("Unknown Structure")

handle_data([1, 2])  # 输出 "List with two elements: 1, 2"
handle_data({"name": "Alice", "age": 25})  # 输出 "Dictionary with name: Alice, age: 25"
```

***

**4. 匹配嵌套结构**

匹配嵌套的数据结构。

```python
def handle_nested(data):
    match data:
        case {"user": {"name": name, "age": age}}:
            print(f"User: {name}, Age: {age}")
        case _:
            print("Unknown Nested Structure")

handle_nested({"user": {"name": "Bob", "age": 30}})  # 输出 "User: Bob, Age: 30"
```

***

**5. 匹配变量**

将匹配的值绑定到变量。

```python
def handle_variable(data):
    match data:
        case (x, y):
            print(f"Tuple with elements: {x}, {y}")
        case _:
            print("Unknown Data")

handle_variable((10, 20))  # 输出 "Tuple with elements: 10, 20"
```

***

**6. 匹配条件**

在模式中添加条件（`if` 语句）。

```python
def handle_condition(data):
    match data:
        case (x, y) if x > y:
            print(f"First element is greater: {x} > {y}")
        case (x, y) if x < y:
            print(f"Second element is greater: {x} < {y}")
        case _:
            print("Unknown Condition")

handle_condition((10, 5))  # 输出 "First element is greater: 10 > 5"
handle_condition((3, 7))   # 输出 "Second element is greater: 3 < 7"
```

***

**7. 匹配枚举**

匹配枚举类型。

```python
from enum import Enum

class Status(Enum):
    SUCCESS = 200
    NOT_FOUND = 404
    SERVER_ERROR = 500

def handle_enum(status):
    match status:
        case Status.SUCCESS:
            print("Success")
        case Status.NOT_FOUND:
            print("Not Found")
        case Status.SERVER_ERROR:
            print("Server Error")
        case _:
            print("Unknown Status")

handle_enum(Status.SUCCESS)  # 输出 "Success"
```

***

**8. 匹配通配符**

使用 `_` 匹配任意值。

```python
def handle_wildcard(data):
    match data:
        case (_, _):
            print("Tuple with two elements")
        case _:
            print("Unknown Data")

handle_wildcard((1, 2))  # 输出 "Tuple with two elements"
```

***

#### **总结**

`match` 语句的常见用法包括：

1. 匹配字面值。
2. 匹配类型。
3. 匹配结构。
4. 匹配嵌套结构。
5. 匹配变量。
6. 匹配条件。
7. 匹配枚举。
8. 匹配通配符。

`match` 语句非常适合处理复杂的条件分支和数据结构匹配，可以显著提高代码的可读性和简洁性！
