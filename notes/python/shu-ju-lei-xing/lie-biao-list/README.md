---
description: 列表是 Python 中最常用的数据结构之一，支持动态增删改查。
---

# 列表(list)

**常用方法：**

*   **添加元素**：

    ```python
    my_list.append(x)       # 在末尾添加元素 x
    my_list.insert(i, x)    # 在索引 i 处插入元素 x
    my_list.extend(iterable) # 将可迭代对象的元素添加到列表末尾
    ```
*   **删除元素**：

    ```python
    my_list.remove(x)       # 删除第一个值为 x 的元素
    my_list.pop([i])        # 删除并返回索引 i 处的元素（默认最后一个）
    del my_list[i]          # 删除索引 i 处的元素
    my_list.clear()         # 清空列表
    ```
*   **查找和排序**：

    ```python
    my_list.index(x)        # 返回第一个值为 x 的元素的索引
    my_list.count(x)        # 返回值为 x 的元素的数量
    my_list.sort()          # 对列表进行排序
    my_list.reverse()       # 反转列表
    ```
*   **其他**：

    ```python
    len(my_list)            # 返回列表长度
    my_list.copy()          # 返回列表的浅拷贝
    ```

