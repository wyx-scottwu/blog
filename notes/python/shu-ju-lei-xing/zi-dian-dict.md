---
description: 字典是键值对的集合，支持高效的查找和更新。
---

# 字典(dict)

**常用方法：**

*   **添加和更新**：

    ```python
    my_dict[key] = value    # 添加或更新键值对
    my_dict.update(other)  # 用其他字典更新当前字典
    ```
*   **删除**：

    ```python
    del my_dict[key]        # 删除指定键的键值对
    my_dict.pop(key)        # 删除并返回指定键的值
    my_dict.clear()         # 清空字典
    ```
*   **查找和遍历**：

    ```python
    my_dict.get(key)        # 返回键 key 的值，不存在则返回 None
    my_dict.keys()          # 返回所有键的视图
    my_dict.values()        # 返回所有值的视图
    my_dict.items()         # 返回所有键值对的视图
    ```
*   **其他**：

    ```python
    len(my_dict)            # 返回字典中键值对的数量
    key in my_dict          # 检查键是否存在于字典中
    ```

#### **4. 集合（`set`）**

集合是无序且不重复的元素集合，支持集合运算。

**常用方法：**

*   **添加和删除**：

    ```python
    my_set.add(x)           # 添加元素 x
    my_set.remove(x)        # 删除元素 x，不存在则报错
    my_set.discard(x)       # 删除元素 x，不存在则忽略
    my_set.pop()            # 删除并返回任意一个元素
    my_set.clear()          # 清空集合
    ```
*   **集合运算**：

    ```python
    my_set.union(other)     # 返回并集
    my_set.intersection(other) # 返回交集
    my_set.difference(other) # 返回差集
    my_set.symmetric_difference(other) # 返回对称差集
    ```
*   **其他**：

    ```python
    len(my_set)             # 返回集合中元素的数量
    x in my_set             # 检查元素是否存在于集合中
    ```

***

#### **5. 数字（`int`, `float`）**

数字是不可变的基本数据类型，支持数学运算。

**常用方法：**

*   **数学运算**：

    ```python
    abs(x)                  # 返回绝对值
    round(x, n)             # 四舍五入到 n 位小数
    pow(x, y)               # 返回 x 的 y 次方
    divmod(x, y)            # 返回商和余数
    ```
*   **类型转换**：

    ```python
    int(x)                  # 转换为整数
    float(x)                # 转换为浮点数
    ```
*   **其他**：

    ```python
    max(x, y)               # 返回最大值
    min(x, y)               # 返回最小值
    ```

***

#### **总结**

* **列表**：动态增删改查，支持排序和反转。
* **字符串**：查找、替换、分割、连接等操作。
* **字典**：键值对的增删改查，支持高效查找。
* **集合**：无序不重复元素，支持集合运算。
* **数字**：数学运算和类型转换。

这些原生方法使得 Python 的数据结构非常强大且易于使用！
