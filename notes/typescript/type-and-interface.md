---
description: usage
---

# Type & Interface

在 TypeScript 中，interface 和 type 都可以用来定义对象的结构，但它们之间有一些重要的区别和使用场景。以下是对两者的详细比较：

***

### I. `interface` 和 `type` 的相同点

* 都可以用来描述对象结构
* 都支持扩展（extends/交并集）
* 都支持对函数、数组、类的类型定义。

**示例：描述对象结构**

```typescript
// 使用 interface
interface User {
  id: number;
  name: string;
}

// 使用 type
type User = {
  id: number;
  name: string;
};
```

***

### II. `interface`和`type`的区别

#### 区别 1：扩展方式不同

* `interface`使用`extends`关键字扩展
* `type`使用交集（`&`）来实现类型组合

```typescript
// interface 扩展
interface Person {
  name: string;
}
interface Employee extends Person {
  id: number;
}

// type 扩展
type Person = {
  name: string;
};
type Employee = Person & {
  id: number;
};
```

***

#### 区别 2：`interface` 支持声明合并，`type` 不支持

* `interface`支持多次声明，所有声明会自动合并
* `type`不支持多次声明，如果重复声明会报错

```typescript
// interface 声明合并
interface User {
  id: number;
}

interface User {
  name: string;
}

// 最终合并为：
interface User {
  id: number;
  name: string;
}

// type 不支持声明合并
type User = {
  id: number;
};

type User = {
  name: string;
}; // Error: Duplicate identifier 'User'
```

***

#### 区别3：`type`可以定义更复杂的类型

* `type`可以用来定义联合类型，交集类型，条件类型等
* `interface`则不支持

```typescript
// type 的联合类型
type Status = "success" | "error" | "loading";

// type 的交集类型
type Admin = {
  role: "admin";
};

type User = {
  name: string;
};

type AdminUser = Admin & User;
```

***

#### 区别4：类型别名`type` 可以用于基本类型和元组

* `type`可以用来定义基本类型别名和元组类型。
* `interface`不支持

```typescript
// type 的基本类型别名
type ID = number | string;

// type 的元组类型
type Point = [number, number];
```

***

#### 区别 5：`interface` 可以被类实现，`type` 不行

* `interface` 可以被类实现（`implements`）
* `type` 不支持类的实现

```typescript
// interface 类实现
interface Person {
  name: string;
  greet(): void;
}

class Employee implements Person {
  name = "John";
  greet() {
    console.log("Hello");
  }
}

// type 无法直接实现类
type Person = {
  name: string;
  greet(): void;
};

class Employee implements Person {
  // Error: 'Person' only refers to a type, but is being used as a value here.
}
```

***

### 总结：`interface` `vs` `type`

| 特性      | interface | type |
| ------- | --------- | ---- |
| 定义对象结构  | ✅         | ✅    |
| 扩展方式    |           |      |
| 声明合并    |           |      |
| 定义联合累心  |           |      |





