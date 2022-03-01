---
title: TypeScript 泛型
date: 2020-09-07 10:56:55
tags:
  - TypeScript基础
category: TypeScript
---

泛型的使用主要在于它的重用性，当一个组件可以使用多种类型的数据来使用时，这个组件就拥有很高的复用性，这时就可以用泛型来代替使用数据，这在创建大型系统时为我们提供了十分灵活的功能。

## 泛型基础使用

设置泛型类似于接口中规范了使用参数的类型，限制了函数中参数类型的使用。

```Typescript
function identity(arg: number): number {
    return arg;
}
let output = identity(1);
```

## 使用泛型变量

使用泛型可以用变量代替泛型声明，变量可以代表任意数据类型，类似于使用泛型声明为 any 类型，不过由于是变量所以不能使用类型中的指定函数。

```Typescript
function identity<T>(arg: T): T {
    return arg;
}
```

```Typescript
function loggingIdentity<T>(arg: Array<T>): Array<T> {
    console.log(arg.length);  // Array has a .length, so no more error
    return arg;
}
```

## 泛型类型

泛型函数的类型与非泛型函数的类型没什么不同，只是有一个类型参数在最前面，像函数声明一样,我们也可以使用不同的泛型参数名，只要在数量上和使用方式上能对应上就可以。

```Typescript
interface GenericIdentityFn<T> {
    (arg: T): T;
}

function identity<T>(arg: T): T {
    return arg;
}

let myIdentity: GenericIdentityFn<number> = identity;
```

## 泛型约束

将泛型变量继承我们的约束条件，泛型中就有的传输参数的限制，当我们使用泛型定义时就要遵守规则。
约束条件可以使接口定义

```Typescript
interface Lengthwise {
    length: number;
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
    console.log(arg.length);  // Now we know it has a .length property, so no more error
    return arg;
}
loggingIdentity(3);
loggingIdentity({length: 10, value: 3});
```

### 在泛型里使用类类型

使用原型属性推断并约束构造函数与类实例的关系

```typescript
class BeeKeeper {
  hasMask: boolean;
}

class ZooKeeper {
  nametag: string;
}

class Animal {
  numLegs: number;
}

class Bee extends Animal {
  keeper: BeeKeeper;
}

class Lion extends Animal {
  keeper: ZooKeeper;
}

function createInstance<A extends Animal>(c: new () => A): A {
  return new c();
}

createInstance(Lion).keeper.nametag; // typechecks!
createInstance(Bee).keeper.hasMask; // typechecks!
```
