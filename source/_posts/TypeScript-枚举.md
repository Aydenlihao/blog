---
title: TypeScript 枚举
date: 2020-10-15 10:14:45
tags:
  - TypeScript基础
category: TypeScript
---

## 使用枚举

使用**enum**关键字定义对象

```TypeScript
enum  obj {
  A = 1,
  B = 'B',
  C
}
```

## 数字枚举

在未设置初始之时，枚举类中的第一个值为 0，其他成员会从 1 开始自动增长（自动加 1）

```typeScript
enum Direction {
    Up,
    Down,
    Left,
    Right,
}
```

Up 的值为 0， Down 的值为 1 等等。

在设置了第一个初始值时，其他成员会从初始值开始自动增长（自动加 1）

```typeScript
enum Direction {
   Up = 1,
   Down,
   Left,
   Right
}
```

Up 使用初始化为 1，其余的成员会从 1 开始自动增长。换句话说 Direction.Up 的值为 1，Down 为 2， Left 为 3， Right 为 4。当我们不在乎成员的值时，使用自动增长是可以更加简便的。

## 字符串枚举

每个成员都必须用字符串字面量，或另外一个字符串枚举成员进行设置初始化值

```typescript
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT",
}
```

数字枚举和字符串枚举的区别在于，字符串枚举的值初始化时已经设置，数字枚举的值是运行中提供的，如果要在运行中获取一个数字枚举的值，这是很难读取的，虽然数字枚举中有反向映射，但数字枚举本来就作用于我们不在乎成员值的时候。字符串枚举可以提供一个运行时有意义并可读的值。

## 异构枚举

从技术的角度来说，枚举可以混合字符串和数字成员。

```Typescript
enum BooleanLikeHeterogeneousEnum {
    No = 0,
    Yes = "YES",
}
```

除非你真的想要利用 JavaScript 运行时的行为，否则我们不建议这样做。

## 计算的和常量成员

每个枚举成员都带有一个值，它可以是常量或计算出来的，常数枚举表达式是 TypeScript 表达式的子集，它可以在编译阶段求值，所以枚举的值可以是一个常量枚举表达式：

- 一个枚举表达式字面量（主要是字符串字面量或数字字面量）
- 一个对之前定义的常量枚举成员的引用（可以是在不同的枚举类型中定义的）
- 带括号的常量枚举表达式
- 一元运算符 +, -, ~其中之一应用在了常量枚举表达式
- 常量枚举表达式做为二元运算符 +, -, \*, /, %, <<, >>, >>>, &, |, ^的操作对象。 若常数枚举表达式求值后为 NaN 或 Infinity，则会在编译阶段报错。

```typescript
enum FileAccess {
  // constant members
  None,
  Read = 1 << 1,
  Write = 1 << 2,
  ReadWrite = Read | Write,
  // computed member
  G = "123".length,
}
```

## 联合枚举与枚举成员的类型

存在一种特殊的非计算的常量枚举成员的子集：字面量枚举成员。 字面量枚举成员是指不带有初始值的常量枚举成员，或者是值被初始化为

- 任何字符串字面量（例如： "foo"， "bar"， "baz"）
- 任何数字字面量（例如： 1, 100）
- 应用了一元 -符号的数字字面量（例如： -1, -100）

```typescript
enum ShapeKind {
  Circle,
  Square,
}

interface Circle {
  kind: ShapeKind.Circle;
  radius: number;
}

interface Square {
  kind: ShapeKind.Square;
  sideLength: number;
}

let c: Circle = {
  kind: ShapeKind.Square,
  //    ~~~~~~~~~~~~~~~~ Error!
  radius: 100,
};
```

## 运行时的枚举

枚举是在运行时真正存在的对象。

```typescript
enum E {
  X,
  Y,
  Z,
}
function f(obj: { X: number }) {
  return obj.X;
}

// Works, since 'E' has a property named 'X' which is a number.
f(E);
```

在代码编译时，数字枚举的值还没有提供，所以成员的类型不是 number。

## 外部枚举

使用关键字**declare**
官方说法：外部枚举和非外部枚举之间有一个重要的区别，在正常的枚举里，没有初始化方法的成员被当成常数成员。 对于非常数的外部枚举而言，没有初始化方法时被当做需要经过计算的。
我的看法：仅仅会用于编译时的检查，在编译结果中会被删除

```typescript
declare enum Enum {
  A = 1,
  B,
  C = 2,
}
```
