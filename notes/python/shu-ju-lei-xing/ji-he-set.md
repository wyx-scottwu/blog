---
description: 集合是无序且不重复的元素集合，支持集合运算。
---

# 集合(set)

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
