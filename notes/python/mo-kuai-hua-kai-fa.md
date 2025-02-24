# 模块化开发

在 Python 中，模块的导入和导出是通过 `import` 和 `from ... import ...` 语句实现的。以下是详细的用法和示例：

***

#### **1. 模块的导入**

**导入整个模块**

```python
import math

# 使用模块中的函数
print(math.sqrt(16))  # 输出 4.0
```

**导入模块并指定别名**

```python
import numpy as np

# 使用别名调用模块中的函数
print(np.array([1, 2, 3]))  # 输出 [1 2 3]
```

**从模块中导入特定函数或类**

```python
from math import sqrt, pi

# 直接使用导入的函数
print(sqrt(25))  # 输出 5.0
print(pi)        # 输出 3.141592653589793
```

**从模块中导入所有内容（不推荐）**

```python
from math import *

# 直接使用模块中的所有函数
print(sqrt(36))  # 输出 6.0
print(pi)        # 输出 3.141592653589793
```

***

#### **2. 模块的导出**

在 Python 中，模块的导出是通过定义模块中的函数、类、变量等实现的。其他模块可以通过导入来使用这些内容。

**示例：创建一个模块 `mymodule.py`**

```python
# mymodule.py
def greet(name):
    return f"Hello, {name}!"

def add(a, b):
    return a + b

PI = 3.14159
```

**在其他模块中导入 `mymodule`**

```python
import mymodule

# 使用 mymodule 中的函数和变量
print(mymodule.greet("Alice"))  # 输出 "Hello, Alice!"
print(mymodule.add(2, 3))       # 输出 5
print(mymodule.PI)              # 输出 3.14159
```

**从 `mymodule` 中导入特定内容**

```python
from mymodule import greet, add

# 直接使用导入的函数
print(greet("Bob"))  # 输出 "Hello, Bob!"
print(add(4, 5))     # 输出 9
```

***

#### **3. 模块的 `__all__` 变量**

`__all__` 是一个特殊的变量，用于定义模块中哪些内容可以被 `from module import *` 导入。

**示例：在 `mymodule.py` 中定义 `__all__`**

```python
# mymodule.py
__all__ = ['greet', 'PI']

def greet(name):
    return f"Hello, {name}!"

def add(a, b):
    return a + b

PI = 3.14159
```

**使用 `from mymodule import *`**

```python
from mymodule import *

# 只能使用 __all__ 中定义的内容
print(greet("Charlie"))  # 输出 "Hello, Charlie!"
print(PI)                # 输出 3.14159

# add 函数未在 __all__ 中定义，无法使用
try:
    print(add(1, 2))
except NameError as e:
    print(f"Error: {e}")  # 输出 "Error: name 'add' is not defined"
```

***

#### **4. 模块的 `if __name__ == "__main__"`**

`if __name__ == "__main__"` 用于判断模块是直接运行还是被导入。如果是直接运行，则执行该代码块。

**示例：在 `mymodule.py` 中添加 `if __name__ == "__main__"`**

```python
# mymodule.py
def greet(name):
    return f"Hello, {name}!"

def add(a, b):
    return a + b

PI = 3.14159

if __name__ == "__main__":
    print(greet("World"))  # 直接运行模块时输出 "Hello, World!"
```

***

#### **总结**

* **导入模块**：使用 `import` 或 `from ... import ...`。
* **导出模块**：通过定义函数、类、变量等实现。
* **控制导出内容**：使用 `__all__` 变量。
* **模块直接运行**：使用 `if __name__ == "__main__"`。

通过这些方法，可以灵活地组织和使用 Python 模块！
