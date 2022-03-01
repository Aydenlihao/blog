---
title: TypeScript 接口
date: 2020-08-20 14:04:51
tags:
  - TypeScript基础
category: TypeScript
---

TypeScript 里，接口的作用就是为这些类型定义和为你的代码或第三方代码定义规范

## 基础使用

```TypeScript
function printLabel(labelledObj: { label: string }) {
  console.log(labelledObj.label);
}

let myObj = { size: 10, label: "Size 10 Object" };
printLabel(myObj);
```

## 属性

### 可选属性

接口定义的可选属性，就是在属性名“：”前加“？”，属性就成了非必需的，这样定义的属性可以不进行默认传值。

```TypeScript
interface SquareConfig {
  color?: string;
  width?: number;
}

function createSquare(config: SquareConfig): {color: string; area: number} {
  let newSquare = {color: "white", area: 100};
  if (config.color) {
    newSquare.color = config.color;
  }
  if (config.width) {
    newSquare.area = config.width * config.width;
  }
  return newSquare;
}

let mySquare = createSquare({color: "black"});
```

### 只读属性

```TypeScript
interface Point {
    readonly x: number;
    readonly y: number;
}
let p1: Point = { x: 10, y: 20 };
p1.x = 5;
```

接口定义的只读属性，只能读取该属性

### 属性检查

即使接口中使用了可选属性，但只是意味着接口实例里可以没有这个属性，并不意味着可以多出其他属性，检查是否有不在接口定义中的属性，就是额外的属性检查。

```TypeScript
interface SquareConfig {
    color?: string;
    width?: number;
}
function createSquare(config: SquareConfig): { color: string; area: number } {
    // ...
}

let mySquare = createSquare({ colour: "red", width: 100 });
```

## 函数类型

除了描述带有属性的普通对象外，接口也可以描述函数类型。

```TypeScript
interface SearchFunc {
  (source: string, subString: string): boolean;
}
let mySearch: SearchFunc;
mySearch = function(source: string, subString: string) {
  let result = source.search(subString);
  return result > -1;
}
```

### 可索引的类型

```TypeScript
interface StringArray {
  [index: number]: string;
}

let myArray: StringArray;
myArray = ["Bob", "Fred"];

let myStr: string = myArray[0];
```

TypeScript 支持两种索引签名：字符串和数字，可索引类型具有一个索引签名，它描述了对象索引的类型，还有相应的索引返回值类型，当你定义了 string 类型的对象索引并确定了索引返回值，其他的索引返回值就已经确定，因为当其他索引转换为 JavaScript 时都会转为 string。

```TypeScript
interface StringArray {
  [index: number]: string;
}

let myArray: StringArray;
myArray = ["Bob", "Fred"];

let myStr: string = myArray[0];
class Animal {
    name: string;
}
class Dog extends Animal {
    breed: string;
}

// 错误：使用数值型的字符串索引，有时会得到完全不同的Animal!
interface NotOkay {
    [x: number]: Animal;
    [x: string]: Dog;
}
```

## 类类型

子类限时父接口时，可以显示父接口的方法。
当一个类实现了一个接口时，只对其实例部分进行类型检查，构造函数属于静态部分，不进行属性检查

```typeScript
interface ClockInterface {
    currentTime: Date;
}

class Clock implements ClockInterface {
    currentTime: Date;
    constructor(h: number, m: number) { }
}
```

当用构造器签名去定义一个接口并试图定义一个类去实现这个接口时会得到一个错误

```typeScript
interface ClockConstructor {
    new (hour: number, minute: number);
}

class Clock implements ClockConstructor {
    currentTime: Date;
    constructor(h: number, m: number) { }
}
```

## 继承

接口可以多继承接口，当接口继承父接口时，子接口就具备父接口的属性或方法

```TypeScript
interface Shape {
    color: string;
}

interface Square extends Shape {
    sideLength: number;
}

let square = <Square>{};
square.color = "blue";
square.sideLength = 10;
```

多继承

```TypeScript

interface Shape {
    color: string;
}

interface PenStroke {
    penWidth: number;
}

interface Square extends Shape, PenStroke {
    sideLength: number;
}

let square = <Square>{};
square.color = "blue";
square.sideLength = 10;
square.penWidth = 5.0;
```

## 混合

使用混合可以使一个对象拥有多种使用方式，可以作为函数使用也可以作为对象使用

```typeScript
interface Counter {
    (start: number): string;
    interval: number;
    reset(): void;
}

function getCounter(): Counter {
    let counter = <Counter>function (start: number) { };
    counter.interval = 123;
    counter.reset = function () { };
    return counter;
}

let c = getCounter();
c(10);
c.reset();
c.interval = 5.0;
```

## 继承类

当接口继承了一个类类型时，它会继承类的成员但不包括其实现，接口同样会继承到类的 private 和 protected 成员。

```typeScript
class Control {
    private state: any;
}

interface SelectableControl extends Control {
    select(): void;
}

class Button extends Control implements SelectableControl {
    select() { }
}

class TextBox extends Control {
    select() { }
}

// 错误：“Image”类型缺少“state”属性。
class Image implements SelectableControl {
    select() { }
}
```
