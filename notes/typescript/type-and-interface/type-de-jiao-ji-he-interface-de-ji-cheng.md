# type 的交集 和 interface 的继承

在 `TypeScript` 中，`type` 的交集 和 `interface` 的继承 都会遇到重复类型或重名类型的问题。不同的是，处理方式和结果会有一些区别：

* `interface` 的 `extends` 会**自动合并重复类型**，但如果类型冲突，会报错。
* `type` 的**交集** 会直接**覆盖重复类型**，后者会覆盖前者。

***

### 🔍 1. `interface` `extends` 重复类型的处理

如果继承的多个接口中出现**重复的属性**：

* 如果属性的类型一致，会自动合并。
* 如果属性的类型不同，TypeScript 会报错，必须手动调整类型。

#### ✅ 示例 1：类型一致时自动合并

```typescript
interface A {
  name: string;
}

interface B {
  name: string;
}

interface C extends A, B {
  age: number;
}

// 等价于：
interface C {
  name: string;
  age: number;
}
```

#### ❌ 示例 2：类型冲突时报错

```typescript
interface A {
  name: string;
}

interface B {
  name: number; // 类型冲突
}

interface C extends A, B {
  age: number;
}

//   Error: Interface 'C' cannot simultaneously extend types 'A' and 'B'.
//   Types of property 'name' are incompatible.
```

解决方法：使用联合类型

```typescript
interface A {
  name: string;
}

interface B {
  name: number;
}

interface C extends A, B {
  name: string | number; // 手动解决冲突
  age: number;
}
```

***

### 🔍 2. type 的交集（Intersection Types）重复类型的处理

对于 **type 的交集**：

* 如果有重复的属性类型，**后者会覆盖前者**。
* 不会报错，但可能会导致意外的类型覆盖行为。

#### ✅ 示例 1：后者覆盖前者

```typescript
type A = {
  name: string;
};

type B = {
  name: number;
};

type C = A & B;

// C 的类型为：
type C = {
  name: number; // 后者 B 的类型覆盖了 A 的类型
};
```

***

#### ✅ 示例 2：使用联合类型避免覆盖

如果希望避免属性被覆盖，可以手动将属性定义为**联合类型**：

```typescript
type A = {
  name: string;
};

type B = {
  name: number;
};

type C = A & B & {
  name: string | number; // 手动调整为联合类型
};
```

### 🔎 3. interface vs type 重名类型的区别

<table><thead><tr><th width="180">操作</th><th width="178">extends</th><th width="193">交集（&#x26;）</th></tr></thead><tbody><tr><td>重复类型一致</td><td>自动合并</td><td>后者覆盖前者</td></tr><tr><td>重复类型冲突</td><td>报错</td><td>后者覆盖前者，不报错</td></tr><tr><td>解决方法</td><td>手动调整联合类型</td><td>手动调整联合类型</td></tr></tbody></table>

***

### 💡最佳实践建议

1. **如果使用** `interface` **的继承**，确保继承的接口中没有冲突的属性类型。如果有冲突，**手动调整为联合类型**。
2. **如果使用** `type` **的交集**，要特别小心属性覆盖的情况。如果有重名属性，**检查是否需要用联合类型避免意外的覆盖行为**。

#### 示例

**✅ 使用 interface 时避免冲突**

```typescript
interface A {
  name: string;
}

interface B {
  name: number;
}

interface C extends A, B {
  name: string | number; // 手动调整为联合类型
  age: number;
}
```

**✅ 使用 type 时避免覆盖**

```typescript
type A = {
  name: string;
};

type B = {
  name: number;
};

type C = A & B & {
  name: string | number; // 手动调整为联合类型
};
```
