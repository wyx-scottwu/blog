---
description: 字符串是不可变的序列，支持多种操作方法。
---

# 字符串(str)

**常用方法：**

*   **查找和替换**：

    ```python
    s.find(sub)             # 返回子字符串 sub 的首次出现索引，未找到返回 -1
    s.replace(old, new)     # 将字符串中的 old 替换为 new
    s.count(sub)            # 返回子字符串 sub 的出现次数
    ```
*   **大小写转换**：

    ```python
    s.lower()               # 转换为小写
    s.upper()               # 转换为大写
    s.title()               # 每个单词首字母大写
    ```
*   **去除空白**：

    ```python
    s.strip()               # 去除两端空白字符
    s.lstrip()              # 去除左端空白字符
    s.rstrip()              # 去除右端空白字符
    ```
*   **分割和连接**：

    ```python
    s.split(sep)            # 按分隔符 sep 分割字符串，返回列表
    s.join(iterable)        # 将可迭代对象的元素用字符串 s 连接
    ```
*   **其他**：

    ```python
    len(s)                  # 返回字符串长度
    s.startswith(prefix)    # 检查字符串是否以 prefix 开头
    s.endswith(suffix)      # 检查字符串是否以 suffix 结尾
    ```
