# interface 声明合并

在 `TypeScript` 中，`interface` **声明合并**时，如果多个接口具有**重复的属性**，`TypeScript` 会自动合并这些接口的属性：

* 如果**重复**的属性类型**相同**，`TypeScript` 会正常合并，不报错。
* 如果**重复**的属性类型**不同**，`TypeScript` 会尝试**创建一个联合类型**。
* 如果类型冲突**不能自动解决**，`TypeScript` 会**报错**。

***

### 🔎 1. `interface` 声明合并基础示例

```typescript
interface Person {
  name: string;
}

interface Person {
  age: number;
}

// 合并结果
interface Person {
  name: string;
  age: number;
}
```

`TypeScript` 会将两个 `Person` 接口自动合并成一个，包含所有属性。

***

### 🔍 2. 当属性重复时的处理规则

#### ✅ 属性类型相同：正常合并

```typescript
interface User {
  id: number;
}

interface User {
  id: number; // 相同类型
  name: string;
}

const user: User = {
  id: 1,
  name: "Alice",
};
```

`TypeScript` 会合并 `User` 接口，不会报错。

***

#### ⚠️  属性类型不同：自动创建联合类型

如果重复的属性类型不同，`TypeScript` 会自动将它们合并为联合类型。

```typescript
interface Config {
  mode: string;
}

interface Config {
  mode: number; // 不同类型
}

const config: Config = {
  mode: "dark", // ✅ 可以是 string
};

const anotherConfig: Config = {
  mode: 1, // ✅ 也可以是 number
};

// 合并结果
interface Config {
  mode: string | number;
}
```

***

#### ❌ 方法签名冲突：返回类型冲突会报错

如果接口中有重复的方法签名，但返回类型不同，`TypeScript` 会报错，因为它无法确定该方法的正确返回类型。

```typescript
interface Calculator {
  calculate(a: number, b: number): number;
}

interface Calculator {
  calculate(a: number, b: number): string; // 返回类型冲突
}

// ❌ Error: Subsequent property declarations must have the same type.
```

✅ 解决方法：定义联合返回类型

```typescript
interface Calculator {
  calculate(a: number, b: number): number | string;
}
```

***

#### 方法重载的合并规则

TypeScript 支持**方法重载**，所以如果方法签名不同，但参数列表不同，则不会报错。

```typescript
interface Printer {
  print(text: string): void;
}

interface Printer {
  print(text: string, copies: number): void;
}

const printer: Printer = {
  print: (text: string, copies?: number) => {
    console.log(`Printing: ${text}, Copies: ${copies ?? 1}`);
  },
};
```

### 🔔 3. 规则总结

<table><thead><tr><th width="167">情况</th><th width="168">结果</th><th>示例</th></tr></thead><tbody><tr><td>属性类型相同</td><td>正常合并</td><td><code>id: number + id: number</code></td></tr><tr><td>属性类型不同</td><td>自动创建联合类型</td><td><code>mode: string + mode: number → mode: string | number</code></td></tr><tr><td>方法签名不同</td><td>自动合并重载</td><td><code>print(text: string) + print(text: string, copies: number)</code></td></tr><tr><td>方法返回类型冲突</td><td>报错</td><td><code>calculate(a: number, b: number): number + calculate(a: number, b: number): string</code></td></tr></tbody></table>

***

### 总结

<table><thead><tr><th width="186">特性</th><th width="371">interface 声明合并的行为</th></tr></thead><tbody><tr><td>属性类型相同</td><td>正常合并</td></tr><tr><td>属性类型不同</td><td>自动创建联合类型</td></tr><tr><td>方法签名不同</td><td>自动合并为方法重载</td></tr><tr><td>方法返回类型冲突</td><td>报错，需手动调整为联合类型或重载签名</td></tr></tbody></table>

💡 建议：

* 当有可能出现冲突时，尽量手动调整属性类型为联合类型。
* 如果是方法签名冲突，考虑使用方法重载来解决问题。
