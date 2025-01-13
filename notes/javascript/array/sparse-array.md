# Sparse Array

### 📌 宽松数组（`Sparse Array`）是什么？

宽松数组（`Sparse Array`） 是指数组中包含未定义的索引（稀疏索引）的数组。也就是说，这个数组的长度可能大于它实际拥有的元素数。

```javascript
// 例子1：宽松数组
const sparseArray = [1, , 3];  // 中间有一个空的元素
console.log(sparseArray.length);  // 输出 3
console.log(Object.keys(sparseArray));  // 输出 ["0", "2"]


// 例子2：非宽松数组
const denseArray = [1, 2, 3];
console.log(denseArray.length);  // 输出 3
console.log(Object.keys(denseArray));  // 输出 ["0", "1", "2"]

```

### ✅ 判断数组是否为宽松数组的方法

#### 1️⃣ 方法 1：通过 `Object.keys()` 判断实际键的数量

如果数组的长度 `length` 大于实际键的数量，说明是宽松数组。

```javascript
function isSparseArray(arr) {
  if (!Array.isArray(arr)) return false;
  return Object.keys(arr).length < arr.length;
}

console.log(isSparseArray([1, , 3]));  // true
console.log(isSparseArray([1, 2, 3]));  // false
```

#### 2️⃣ 方法 2：用 `for...in` 遍历数组

`for...in` 只会遍历实际存在的索引。如果遍历的次数小于数组的长度，说明是宽松数组。

```javascript
function isSparseArray(arr) {
  if (!Array.isArray(arr)) return false;

  let count = 0;
  for (let index in arr) {
    count++;
  }

  return count < arr.length;
}

console.log(isSparseArray([1, , 3]));  // true
console.log(isSparseArray([1, 2, 3]));  // false
```

#### 3️⃣ 方法 3：用 `hasOwnProperty` 判断未定义的索引

遍历数组的长度，并检查每个索引是否是该数组的自有属性。

```javascript
function isSparseArray(arr) {
  if (!Array.isArray(arr)) return false;


  for (let i = 0; i < arr.length; i++) {
    if (!arr.hasOwnProperty(i)) {
      return true;
    }
  }


  return false;
}

console.log(isSparseArray([1, , 3]));  // true
console.log(isSparseArray([1, 2, 3]));  // false
```

### 🧪 推荐方法：

使用 `hasOwnProperty` 是最准确的方式：

⚙️ 验证宽松数组的用例

```javascript
const arr = [1,2,,4];

console.log(isSparseArray(arr));  // true
console.log(isSparseArray(new Array(5)));  // true
console.log(isSparseArray([1, 2, 3, 4]));  // false
console.log(isSparseArray([]));  // false

// 如果使用Object.keys()方法
arr.max = 'max';
console.log(isSparseArray(arr));  // false
```
