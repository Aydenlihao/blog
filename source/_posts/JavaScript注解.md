---
title: JavaScript好用还未火的注解@Decorator
date: 2020-06-03 14:42:48
tags:
  - JavaScript基础
category: JavaScript
---

## Decorator 使用

修饰器（Decorator）是一个函数，用来修改类的行为

### Babel 支持

在使用之前需要先下载 babel 插件

```
npm install @babel/plugin-proposal-decorators --save
```

修改配置 ( 我用的是 webpack,所有只要在 webpack.config.js 的配置中加上这句话就行 )

```
plugins: [
              ["@babel/plugin-proposal-decorators", { legacy: true }],
            ],
```

### Class Decorator

```javaScript
const mixins = (...list)=> {
  return function (target) {
    Object.assign(target.prototype, ...list);
  };
}

const Foo = {
  foo() { console.log('foo') }
};

@mixins(Foo)
class MyClass {}

let obj = new MyClass();
obj.foo()
```

修饰类就相当于对类进行了一次封装，重新封装的类拥有了指定的函数或执行了指定操作。

### method Decorator

```javaScript
class Math {
  @log
  add(a, b) {
    return a + b;
  }
}

function log(target, name, descriptor) {
  var oldValue = descriptor.value;
  console.log(oldValue, target)
  descriptor.value = function() {
    // 这里把console.log改成另外一个监听的add函数，就是一个简单的观察者模式了
    console.log(`Calling "${name}" with`, arguments);
    return oldValue.apply(null, arguments);
  };

  return descriptor;
}

const math = new Math();

// passed parameters should get logged now
math.add(2, 4);
```

装饰器第一个参数是类的原型对象,第二个参数是所要装饰的属性名,第三个参数是该属性的描述对象
descriptor 对象
{
value：specifiedFunction,// 置换调用
enumerable: false, // 是否可以枚举（for in 循环能否遍历的到）
configurable: true, // 是否可以配置（是否可以用 delete 删除）
writable: true // 是否可以修改（为 false 的时候，只是修改没起作用，不会报错）
}

修饰函数相当于对指定函数添加了响应事件、回调函数、监听事件。

### property Decorator

```javaScript

class C {
  @readonly(false)
  methods = "cat";
}

function readonly(value) {
  return function (target, key, descriptor) {
    /**
     * 此处 target 为 C.prototype;
     * key 为 method;
     * 原 descriptor 为：{ value: f, enumarable: false, writable: true, configurable: true }
     */
    descriptor.writable = value;
    return descriptor;
  };
}

const c = new C();
c.methods = "bog";

console.log(c);
```

修饰属性相当于对指定属性添加或者修改了属性对象的访问器属性

### 装饰类原理

装饰一个类的属性
ES6 中的类实际上就是一个语法糖，本质上是构造函数，类的属性的定义使用的是 Object.defineProperty() 用一个简单的栗子来理解如下：

```javascript
Object.defineProperty(obj, prop, descriptor);
```

接收的参数和作用于类的属性的时候装饰器函数的接收的参数很像。
本质上也就是说装饰器在作用于类的属性的时候，实际上是通过 Object.defineProperty 来对原有的 descriptor 进行封装
