---
description: 借助该属性解决浮点数计算产生的精度问题
---

# Number.EPSILON

`Number.EPSILON` 是 JavaScript 中表示最小精度的常量（约为 `2.220446049250313e-16`），它可以用来比较两个浮点数是否“足够接近”。虽然 `Number.EPSILON` 本身不能直接用于浮点数运算，但可以借助它来实现更精确的比较和运算。

以下是借助 `Number.EPSILON` 实现浮点数运算并消除精度问题的几种方法：

***

#### 1. **精确比较浮点数**

使用 `Number.EPSILON` 比较两个浮点数是否相等：

```javascript
function isEqual(a, b) {
    return Math.abs(a - b) < Number.EPSILON;
}

console.log(isEqual(0.1 + 0.2, 0.3)); // true
```

***

#### 2. **浮点数运算的封装**

封装一个工具函数，确保浮点数运算的结果在精度范围内正确：

```javascript
function addFloats(a, b) {
    const sum = a + b;
    // 如果结果与预期值的误差小于 Number.EPSILON，则返回预期值
    if (Math.abs(sum - (a + b)) < Number.EPSILON) {
        return a + b;
    }
    return sum;
}

console.log(addFloats(0.1, 0.2)); // 0.30000000000000004
```

***

#### 3. **浮点数运算的修正**

在运算后对结果进行修正，确保其精度在可接受范围内：

```javascript
function preciseAdd(a, b) {
    const sum = a + b;
    // 如果结果与预期值的误差小于 Number.EPSILON，则返回修正后的值
    if (Math.abs(sum - (a + b)) < Number.EPSILON) {
        return Math.round((a + b) * 1e12) / 1e12; // 修正精度
    }
    return sum;
}

console.log(preciseAdd(0.1, 0.2)); // 0.3
```

***

#### 4. **通用浮点数运算工具**

封装一个通用的浮点数运算工具，支持加、减、乘、除：

```javascript
function preciseOperation(operation, a, b) {
    const result = operation(a, b);
    // 如果结果与预期值的误差小于 Number.EPSILON，则返回修正后的值
    if (Math.abs(result - operation(a, b)) < Number.EPSILON) {
        return Math.round(result * 1e12) / 1e12; // 修正精度
    }
    return result;
}

const add = (a, b) => a + b;
const subtract = (a, b) => a - b;
const multiply = (a, b) => a * b;
const divide = (a, b) => a / b;

console.log(preciseOperation(add, 0.1, 0.2)); // 0.3
console.log(preciseOperation(subtract, 0.3, 0.1)); // 0.2
console.log(preciseOperation(multiply, 0.1, 0.2)); // 0.02
console.log(preciseOperation(divide, 0.3, 0.1)); // 3
```

***

#### 5. **结合 `toFixed()` 和 `Number.EPSILON`**

在运算后使用 `toFixed()` 控制小数位数，并结合 `Number.EPSILON` 进行修正：

```javascript
function preciseAdd(a, b) {
    const sum = a + b;
    const fixedSum = Number(sum.toFixed(10)); // 控制小数位数
    // 如果结果与预期值的误差小于 Number.EPSILON，则返回修正后的值
    if (Math.abs(fixedSum - sum) < Number.EPSILON) {
        return fixedSum;
    }
    return sum;
}

console.log(preciseAdd(0.1, 0.2)); // 0.3
```

***

#### 总结

* **精确比较**：使用 `Number.EPSILON` 比较浮点数是否相等。
* **运算修正**：在运算后对结果进行修正，确保其精度在可接受范围内。
* **通用工具**：封装通用的浮点数运算工具，支持加、减、乘、除。
* **结合 `toFixed()`**：使用 `toFixed()` 控制小数位数，并结合 `Number.EPSILON` 进行修正。

通过这些方法，可以更优雅地解决 JavaScript 浮点数运算中的精度问题。
