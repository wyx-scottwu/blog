# Class

在 `TypeScript` 中，`protected`、`public`、`private`、`readonly` 和 `abstract` 是面向对象编程（`OOP`）中的关键字，它们用于控制类中属性和方法的访问权限、不可变性以及类的抽象化。下面是详细解释和使用场景：

### 🎯 1. `public`（公开）

✅ 默认修饰符，属性/方法可以被任何地方访问

* 默认值：如果不指定任何访问修饰符，`TypeScript` 会将其视为 `public`。
* 访问范围：可以在类内部、子类以及类外部访问。

📌 示例：

```typescript
class Animal {
  public name: string; // 默认是 public
  constructor(name: string) {
    this.name = name;
  }

  public makeSound() {
    console.log(`${this.name} is making a sound.`);
  }
}

const dog = new Animal("Dog");
console.log(dog.name); // ✅ 可以在类外访问
dog.makeSound(); // ✅ 可以在类外访问
```

### 🎯 2. `private`（私有）

🚫 属性/方法只能在类内部访问，不能在类的外部或子类中访问

* 无法通过实例或子类访问 `private` 属性或方法。

📌 示例：

```typescript
class Animal {
  private name: string;
  constructor(name: string) {
    this.name = name;
  }

  private makeSound() {
    console.log(`${this.name} is making a sound.`);
  }

  public introduce() {
    console.log(`Hello, I am a ${this.name}`);
    this.makeSound(); // ✅ 可以在类内部访问
  }
}

const dog = new Animal("Dog");
// console.log(dog.name); // ❌ 错误：无法访问私有属性
// dog.makeSound(); // ❌ 错误：无法访问私有方法
dog.introduce(); // ✅ 类内部调用私有方法是允许的
```

### 🎯 3. `protected`（受保护）

🛡️ 属性/方法只能在类内部和子类中访问

* 区别于 `private`：`protected` 可以在子类中访问，但不能在类的外部访问。

📌 示例：

```typescript
class Animal {
  protected name: string;
  constructor(name: string) {
    this.name = name;
  }
}

class Dog extends Animal {
  public introduce() {
    console.log(`Hello, I am a ${this.name}`); // ✅ 子类可以访问 protected 属性
  }
}

const dog = new Dog("Dog");
// console.log(dog.name); // ❌ 错误：不能在类外访问 protected 属性
dog.introduce(); // ✅ 正确
```

### 🎯 4. `readonly`（只读）

🔒 属性在初始化后不可修改

* 可以在构造函数中赋值，但在之后不能修改。
* 常用于表示常量或不可变值。

📌 示例：

```typescript
class Animal {
  readonly species: string;

  constructor(species: string) {
    this.species = species;
  }
}

const dog = new Animal("Dog");
console.log(dog.species); // ✅ 输出：Dog
// dog.species = "Cat"; // ❌ 错误：只读属性不能被修改
```

### 🎯 5. `abstract`（抽象）

📚 用于创建抽象类和抽象方法

* 抽象类不能被直接实例化，必须通过子类实现。
* 抽象方法在抽象类中定义，但不包含具体实现，必须在子类中实现。

📌 示例：

```typescript
abstract class Animal {
  abstract makeSound(): void; // 抽象方法，无具体实现

  public move(): void {
    console.log("Moving...");
  }
}

class Dog extends Animal {
  makeSound(): void {
    console.log("Woof! Woof!");
  }
}

const dog = new Dog();
dog.makeSound(); // ✅ 输出：Woof! Woof!
dog.move(); // ✅ 输出：Moving...
```

### 🔥 总结表格

<table><thead><tr><th width="143">修饰符</th><th>访问权限</th><th>用途</th></tr></thead><tbody><tr><td><code>public</code></td><td>类内、子类、类外部均可访问</td><td>默认访问修饰符</td></tr><tr><td><code>private</code></td><td>仅限类内部访问</td><td>用于隐藏实现细节</td></tr><tr><td><code>protected</code></td><td>类内部和子类可访问</td><td>用于类继承时的访问控制</td></tr><tr><td><code>readonly</code></td><td>初始化后不可修改</td><td>用于定义只读属性</td></tr><tr><td><code>abstract</code></td><td>必须由子类实现，不能实例化</td><td>用于抽象类和抽象方法</td></tr></tbody></table>

### 💡 最佳实践

1. `private` 和 `protected` 常用于隐藏内部实现细节，提供更好的封装性。
2. `readonly` 用于表示属性的不可变性，提高代码的健壮性。
3. `abstract` 用于设计抽象类和接口，提升代码的扩展性和维护性。

