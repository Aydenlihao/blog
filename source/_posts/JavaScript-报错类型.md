---
title: JavaScript 报错类型
date: 2020-09-21 17:38:15
tags:
  - JavaScript基础
category: JavaScript
---

# js 报错类型（6 种错误类型）

js 中的控制台的报错信息主要分为两大类，第一类是语法错误，这一类错误在预解析的过程中如果遇到，就会导致整个 JS 文件都无法执行。另一类错误错误统称为异常，这一类的错误出现的那一行之后的代码无法执行，但在那一行之前的代码不会受到影响。

## SyntaxError(语法错误)

```javascript
// SyntaxError: 语法错误
// 1) 变量名不符合规范
var 1       // Uncaught SyntaxError: Unexpected number
var 1a       // Uncaught SyntaxError: Invalid or unexpected token
// 2) 给关键字赋值
function = 5     // Uncaught SyntaxError: Unexpected token =
```

## ReferenceError（引用错误）
我的理解：这玩意压根就不存在
比如：
```javascript
// ReferenceError：引用错误(要用的变量没找到)
// 1) 引用了不存在的变量
a()       // Uncaught ReferenceError: a is not defined
console.log(b)     // Uncaught ReferenceError: b is not defined
// 2) 给一个无法被赋值的对象赋值
console.log("abc") = 1   // Uncaught ReferenceError: Invalid left-hand side in assignment
```
## TypeError（类型错误） 
我的理解：瞎几把调用
比如：
```javascript
var a；
a() ; // 谁告诉你a是个函数了
```
```javascript
// TypeError: 类型错误(调用不存在的方法)
// 变量或参数不是预期类型时发生的错误。比如使用new字符串、布尔值等原始类型和调用对象不存在的方法就会抛出这种错误，因为new命令的参数应该是一个构造函数。
// 1) 调用不存在的方法
123()        // Uncaught TypeError: 123 is not a function
var o = {}
o.run()        // Uncaught TypeError: o.run is not a function
// 2) new关键字后接基本类型
var p = new 456      // Uncaught TypeError: 456 is not a constructor
```
## RangeError（范围错误）
我的理解:你那玩意过界了
```javascript
// RangeError: 范围错误(参数超范围)
// 主要的有几种情况，第一是数组长度为负数，第二是Number对象的方法参数超出范围，以及函数堆栈超过最大值。
// 1) 数组长度为负数
[].length = -5      // Uncaught RangeError: Invalid array length
// 2) Number对象的方法参数超出范围
var num = new Number(12.34)
console.log(num.toFixed(-1))   // Uncaught RangeError: toFixed() digits argument must be between 0 and 20 at Number.toFixed
// 说明: toFixed方法的作用是将数字四舍五入为指定小数位数的数字,参数是小数点后的位数,范围为0-20.
```
## EvalError（非法调用 eval()）
我的理解: 要盯紧这货
```javascript
// EvalError: 非法调用 eval()
// 在ES5以下的JavaScript中，当eval()函数没有被正确执行时，会抛出evalError错误。例如下面的情况：
var myEval = eval;
myEval("alert('call eval')");
// 需要注意的是：ES5以上的JavaScript中已经不再抛出该错误，但依然可以通过new关键字来自定义该类型的错误提示。以上的几种派生错误，连同原始的Error对象，都是构造函数。开发者可以使用它们，认为生成错误对象的实例。
new Error([message[fileName[lineNumber]]])
// 第一个参数表示错误提示信息，第二个是文件名，第三个是行号。
```
## URIError（URI 不合法）
我的理解：瞎几把乱写
```javascript
// URIError: URI不合法
// 主要是相关函数的参数不正确。
decodeURI("%")     // Uncaught URIError: URI malformed at decodeURI
// jzz
```