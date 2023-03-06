# TypeScript 详解

## 一、TS基础概念

### 1. 什么是TS？

a. 对比原理

* 他是Javascript的一个超集，在原有的语法基础上，添加了可选的静态类型和基于类的面向对象编程

> 面向项目： TS：面向于解决大型复杂项目中，架构以及代码维护复杂场景 JS: 脚本化语言，用于面向单一简单场景

> 自主检测： TS：编译期间，主动发现并纠正错误 JS: 运行时报错

> 类型检测： TS: 弱类型，支持对于动态和静态类型的检测 JS: 弱类型，无静态类型选项

> 运行流程 TS: 依赖编译，依赖工程化体系 JS: 直接在浏览器中运行

> 复杂特性 TS - 模块化、泛型、接口

b. 安装运行

```js
    npm install -g typescript
    tsc -v

    tsc test.ts
    // .ts => .js => 浏览器执行环境

    // 面试点：所有类型检测和语法检测 => 编译时
```

### 2. TS基础类型与写法

* boolean、string、number、array、null、undefined

```ts
    // es
    let isEnabled = true;
    let class = 'zhaowa';
    let classNum = 2;
    let u = undefined;
    let n = null;
    let classArr = ['basic', 'execute'];

    // TS
    let isEnabled: boolean = true;
    let class: string = 'zhaowa';
    let classNum: number = 2;
    let u: undefined = undefined;
    let n: null = null;
    let classArr: string[] = ['basic', 'execute'];
    let classArr: Array<string> = ['basic', 'execute'];
```

* tuple - 元组

```ts
    let tupleType: [string, boolean];
    tupleType = ['zhaowa', true];
```

* enum - 枚举

```ts
    // 数字类枚举 - 默认从零开始，从上往下依次递增
    enum Score {
        BAD,
        NG,
        GOOD,
        PERFECT
    }

    let sco: Score = Score.BAD;

    // 字符串类型枚举
    enum Score {
        BAD = 'BAD',
        NG = 'NG',
        GOOD = 'GOOD',
        PERFECT = 'PERFECT',
    }

    // 反向映射
    enum Score {
        BAD,
        NG,
        GOOD,
        PERFECT
    }

    let scoName = Score[0] // BAD
    let scoVal = Score['BAD'];  // 0

    // 异构
    enum Enum {
        A,      // 0
        B,      // 1
        C = 'C',
        D = 'D',
        E = 6,
        F,      // 7
    }
    // 面试题：指出异构的枚举值
    // 面试题: 手写将其转化为JS实现
    let Enum;
    (function(Enum) {
        // 正向
        Enum['A'] = 0;
        Enum['B'] = 1;
        Enum['C'] = 'C';
        Enum['D'] = 'D';
        Enum['E'] = 6;
        Enum['F'] = 7;

        // 反向
        Enum[0] = 'A';
        Enum[1] = 'B';
        Enum[6] = 'E';
        Enum[7] = 'F';
    })(Enum || (Enum = {}));
```

* any unknown void

```ts
    // any - 绕过所有类型检查 => 类型检测和编译筛查都全部失效
    let anyValue: any = 123;

    anyValue = 'anyValue';
    anyValue = false;

    let value1:boolean = anyValue;

    // unknown - 绕过了赋值检查 => 禁止更改传递
    let unknownValue: unknown;
    
    unknownValue = true;
    unknownValue = 123;
    unknownValue = 'unknownValue';

    let value1: unknown = unknownValue; // OK
    let value1: any = unknownValue; // OK
    let value1: boolean = unknownValue; // NOK

    // void - 声明函数的返回值
    function voidFunction(): void {
        console.log('void function');
    }

    // never - 函数永不返回
    function error(msg: string): never {
        throw new Error(msg);
    }

    function longlongLoop(): never {
        while(true) {}
    }
```

* object / {} - 对象

```ts
    // TS将js的object分成两个接口来定义
    interface ObjectConstructor {
        create(o: object | null): any;
    }

    const proto = {};

    Object.create(proto);
    Object.create(null);
    Object.create(undefined);  // Error

    // Object
    // Object.prototype上属性
    interface Object {
        constructor: Function;
        toString(): string;
        toLocaleString(): string;
        valueof(): Object;
        hasOwnProperty(v: PropertyKey): boolean;
        isPrototypeOf(v: Object): boolean;
    }

    // {} - 空对象定义空属性
    const obj = {};

    obj.prop = 'zhaowa';  // Error
    // 可以使用Object上的所有方法的
    obj.toString();  // OK
```

## 二、接口 - interface

* 对行为的一种抽象，具体行为由类实现

```ts
    interface Class {
        name: string;
        time: number;
    }

    let zhaowa: Class = {
        name: 'ts',
        time: 2
    }

    // 只读 & 任意
    interface Class {
        readonly name: string;
        time: number;
    }

    // 面试题 - 只读和JS的引用是不同的 < = > const => 执行阶段
    let arr: number[] = [1, 2, 3, 4];
    let ro: ReadonlyArray<number> = arr;

    ro[0] = 12;
    ro.push(5);
    ro.length = 100;
    arr = ro;
    // ERROR

    // 任意
    interface Class {
        readonly name: string;
        time: number;
        [propName: string]: any;
    }
    const c1 = {name: 'JS', time: 1}
    const c2 = {name: 'browser', time: 1}
    const c3 = {name: 'ts', level: 1, time: }
```

## 三、交叉类型 - &

```ts
    // 合并
    interface A {x: D}
    interface B {x: E}
    interface C {x: F}

    interface D {d: boolean}
    interface E {e: string}
    interface F {f: number}

    type ABC = A & B & C;

    let abc: ABC = {
        x: {
            d: false,
            e: 'zhaowa',
            f: 5
        }
    }

    // 合并冲突
    interface A {
        c: string,
        d: string
    }
    interface B {
        c: number,
        e: string
    }

    type AB = A & B;
    let ab: AB = {
        d: 'class',
        e: 'class'
    }
    // => 且关系 => c: never
```

## 四、断言 - 类型声明、转换（开发者和编译器的告知交流）

* 编译状态在产生作用

```ts
    // 尖括号形式声明
    let anyValue: any = 'hi zhaowa';
    let anyLength: number = (<string>anyValue).length;

    // as声明
    let anyValue: any = 'hi zhaowa';
    let anyLength: number = (anyValue as string).length;

    // 非空 - 只判断不为空
    type ClassTime = () => number;

    const start = (classTime: ClassTime | undefined) => {
        let num = classTime!(); // 具体类型待定，但是非空确认
    }
    // 使用场景
    const tsClass: number | undefined = undefined;
    const zhaowa: number = tsClass!;

    // 底层实现后，上层应用1
    const tsClass = undefined;
    const zhaowa = tsClass;
    // => 产出undefined可能
    
    // 肯定化保证
    let score: number;
    startClass();
    console.log(2 * score);

    function startClass() {
        score = 5;
    }
    let score!: number; // 告知编辑器，运行时会被赋值的
```

### 五、类型守卫 - 保障语法规定的范围内，额外的确认

* 多态 - 多重状态类型

```ts
    interface Teacher {
        name: string;
        courses: string[];
        score: number;
    }
    interface Student {
        name: string;
        startTime: Date;
        score: string;
    }

    type Class = Teacher | Student;

    // in - 是否包含某种属性
    function startCourse(cls: Class) {
        if ('courses' in cls) {
            // 老师
        }
        if ('startTime' in cls) {
            // 学生
        }
    }
    
    // typeof / instanceof - 类型分类场景下的身份确认
    function startCourse(cls: Class) {
        if (typeof cls.score === 'number') {
            // 老师
        }
        if (typeof cls.score === 'string') {
            // 学生
        }
    }

    function startCourse(cls: Class) {
        if (cls instanceof Teacher) {
            // 老师
        }
        if (cls instanceof Student) {
            // 学生
        }
    }

    // 自定义类型
    const isTeacher = function(cls: Teacher | Student): cls is Teacher {
        // 老师……
    }

    const getInfo = (cls: Teacher | Student) => {
        if (isTeacher(cls)) {
            return cls.courses;
        }
    }
```

### 六、TS进阶方案

### 1. 函数重载

```ts
    class Class {
        start(name: number, score: number): number;
        start(name: string, score: string): string;
        start(name: string, score: number): number;
        start(name: Comnbinable, score: Comnbinable) {
            if (typeof name === 'number' || typeof score === 'number') {
                // 处理
            }
            if (typeof name === 'string' || typeof score === 'string') {
                // 处理
            }
            if (typeof name === 'string' || typeof score === 'number') {
                // 处理
            }
        }
    }
```

### 2. 泛型 - 重用

```ts
    function startClass <T, U>(name: T, score: U): T {
        // 逻辑
    }
    function startClass <T, U>(name: T, score: U): string {
        // 逻辑
    }
    function startClass <T, U>(name: T, score: T): T {
        return (name + score) as T;
    }
```

### 3. 装饰器 - decorator

```ts
    function Zhaowa(target: Function): void {
        target.prototype.startClass = function(): void {
            // 逻辑
        }
    }

    @Zhaowa
    class Course {
        constructor() {
            // 业务逻辑
        }
    }

    // 属性/方法装饰器
    function nameWrapper(target: any, key: string): void {
        Object.defineProperty(target, key, {})
    }

    class Course {
        constructor() {
            // 业务逻辑
        }

        @nameWrapper
        public name: string;
    }
```

### TS 原理流程

```ts
    // 1. 源码
    var a = 2;

    // 2. scanner扫描器生成令牌流
    [
        'var': 'keyword',
        'a': 'identifier',
        '=': 'assignment',
        '2': 'imteger',
        ';': 'eos'
    ]

    // 3. parser 解析器
    {
        operation: '=',
        left: {
            keyword: 'var',
            right: 'a'
        }
        right: '2'
    }

    // 4. binder绑定器
    // AST节点 node.symbol <=> 辅助校验器

    // 5.1. 校验器checker
    // ts节点语法检查 => 类型检查

    // 5.2 发射器emitter
    // 翻译完成每个node节点的内容，翻译成js => 输出
```
