# 泛型

泛型（`Generics`）是 `TypeScript` 的一种强大特性，允许我们在定义函数、类、接口或类型时，不预先指定具体的类型，而是在使用时再传入具体的类型。这样使得代码更加灵活、可重用，同时保持类型安全。

### 🧩 1. 为什么需要泛型？

在 `JavaScript` 中，函数和类通常是用来处理多种类型的数据的。为了支持多种类型，通常会使用 `any` 类型，但这会丢失类型检查的能力：

```typescript
function identity(arg: any): any {
  return arg;
}

const result = identity(123); // result 的类型是 any
```

使用 `any` 虽然灵活，但无法保证类型安全。我们希望函数能接受任意类型的参数，但返回值类型和参数类型保持一致，这就是泛型的作用。

### 🧩 2. 泛型的基本语法

定义一个支持泛型的函数：

```typescript
function identity<T>(arg: T): T {
  return arg;
}
```

🔹 解释：

* `T` 是一个泛型类型变量，表示任意类型。
* `identity` 函数接受一个类型为 `T` 的参数，并返回类型为 `T` 的值。
* 调用时指定具体类型：

```typescript
const result1 = identity<number>(123); // result1 的类型是 number
const result2 = identity<string>("Hello"); // result2 的类型是 string
```

也可以自动推断类型：

```typescript
const result3 = identity(123); // TypeScript 自动推断 T 为 number
```

### 🧩 3. 泛型函数

🔹 定义泛型函数：

```typescript
function getArray<T>(items: T[]): T[] {
  return items;
}
```

* 传入一个数组，并返回一个相同类型的数组。

```typescript
const numberArray = getArray<number>([1, 2, 3]); // number[]
const stringArray = getArray<string>(["a", "b", "c"]); // string[]
```

### 🧩 4. 泛型接口

🔹 定义泛型接口：

```typescript
interface GenericIdentityFn<T> {
  (arg: T): T;
}

const identity: GenericIdentityFn<number> = (arg) => arg;

console.log(identity(123)); // 输出：123
```

### 🧩 5. 泛型类

🔹 定义泛型类：

```typescript
class GenericNumber<T> {
  zeroValue: T;
  add: (x: T, y: T) => T;
}

const myGenericNumber = new GenericNumber<number>();
myGenericNumber.zeroValue = 0;
myGenericNumber.add = (x, y) => x + y;

console.log(myGenericNumber.add(10, 20)); // 输出：30
```

### 🧩 6. 多个类型参数

泛型可以同时接受多个类型参数：

```typescript
function swap<T, U>(tuple: [T, U]): [U, T] {
  return [tuple[1], tuple[0]];
}

const result = swap<number, string>([123, "Hello"]);
console.log(result); // 输出：["Hello", 123]
```

### 🧩 7. 泛型约束（`Constraints`）

有时候我们希望限制泛型只能是某些类型的子类型。这时可以使用泛型约束：

```typescript
interface Lengthwise {
  length: number;
}

function logLength<T extends Lengthwise>(arg: T): T {
  console.log(arg.length);
  return arg;
}

logLength("Hello"); // 有 length 属性
logLength([1, 2, 3]); // 有 length 属性
// logLength(123); // ❌ 报错：number 类型没有 length 属性
```

🔹 解释：

• `T extends Lengthwise` 表示 `T` 必须具有 `Lengthwise` 接口的属性（即必须有 `length` 属性）。

### 🧩 8. 泛型与类型推断

`TypeScript` 通常可以自动推断泛型类型，因此在很多情况下，我们不需要手动指定类型：

```typescript
function identity<T>(arg: T): T {
  return arg;
}

const result = identity(123); // 自动推断 T 为 number
```

### 🧩 9. 泛型工具类型（`Utility Types`）

`TypeScript` 内置了许多基于泛型的工具类型，常见的有：

<table><thead><tr><th width="190">工具类型</th><th width="282">作用</th></tr></thead><tbody><tr><td><code>Partial&#x3C;T></code></td><td>将所有属性变为可选</td></tr><tr><td><code>Required&#x3C;T></code></td><td>将所有属性变为必选</td></tr><tr><td><code>Readonly&#x3C;T></code></td><td>将所有属性变为只读</td></tr><tr><td><code>Pick&#x3C;T, K></code></td><td>从类型 T 中选取部分属性</td></tr><tr><td><code>Omit&#x3C;T, K></code></td><td>从类型 T 中排除指定的属性</td></tr><tr><td><code>Record&#x3C;K, T></code></td><td>构建一个键值对类型</td></tr><tr><td><code>ReturnType&#x3C;T></code></td><td>获取函数的返回值类型</td></tr></tbody></table>

🔹 示例：

```typescript
interface Person {
  name: string;
  age: number;
}


type PartialPerson = Partial<Person>;
type ReadonlyPerson = Readonly<Person>;
```

### 🧩 10. 泛型默认类型

你可以为泛型提供默认类型：

```typescript
function createArray<T = string>(length: number, value: T): T[] {
  return Array(length).fill(value);
}

const stringArray = createArray(3, "Hello"); // T 默认为 string
const numberArray = createArray<number>(3, 42); // 显式指定 T 为 number
```

### 🧩 11. 泛型工具函数

`TypeScript` 的工具函数常用泛型来处理复杂的类型转换。以下是一个工具函数的示例：

```typescript
function merge<T, U>(obj1: T, obj2: U): T & U {
  return { ...obj1, ...obj2 };
}

const person = merge({ name: "Alice" }, { age: 25 });
console.log(person); // 输出：{ name: "Alice", age: 25 }
```

### 🧩 12. 实战案例

用泛型实现一个简单的缓存工具类：

```typescript
class Cache<T> {
  private data: Map<string, T> = new Map();

  set(key: string, value: T): void {
    this.data.set(key, value);
  }

  get(key: string): T | undefined {
    return this.data.get(key);
  }
}

const cache = new Cache<number>();
cache.set("age", 25);
console.log(cache.get("age")); // 输出：25
```

### 🧩 13. 总结

<table><thead><tr><th width="198">优点</th><th width="394">描述</th></tr></thead><tbody><tr><td>类型安全</td><td>泛型保留了类型信息，避免了 <code>any</code> 类型的缺点。</td></tr><tr><td>灵活性</td><td>支持多种类型，避免重复编写相同逻辑的代码。</td></tr><tr><td>可读性强</td><td>泛型使代码结构清晰、易于维护。</td></tr></tbody></table>

👨‍💻 泛型使 `TypeScript` 在保持类型安全的同时，也能编写高度灵活和可复用的代码！
