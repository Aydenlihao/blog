---
title: 数组的push、unshift、pop、shift方法实现
date: 2020-04-30 11:06:15
tags:
  - 算法
category: JavaScript
---

## 尾部添加(push)

`push()函数将一个或者多个元素添加到数组的末尾，并返回该数组的新长度`
从解释中可以看出，push 函数只要将要添加的元素依次放到数组的最后即可，不会改变原有数组元素的索引。所以循环参数列表，将新元素依次放到数组的最后即可。

```javascript
Array.prototype._push = function (...value) {
  for (var i = 0; i < arguments.length; i++) {
    this[this.length] = arguments[i];
  }
  return this.length;
};
var arr = [1, 2, 3, 4];
arr._push(9, 8);
console.log(arr); // [ 1, 2, 3, 4, 9, 8 ]
```

## 头部添加(unshift)

`unshift()函数将将一个或者多个元素添加到数组的开头，并返回该数组的新长度（该函数修改原有数组）`
向数组的头部添加元素，数组的长度也会发生变化，但不像尾部添加的操作，数组原有元素索引不改变。做头部添加的操作，需要将原有元素的索引向左移动。
例如只添加一位，则需要将数组的每个元素的索引依次向右移一位，假设原来数组长度是 4，头部添加一个元素，长度变为 5。所以现在就变成：**array.length = 5**,而目前**array[5-1]**是最后一个元素，现在由于依次往后移动，所以，**array[5-1]必须是最后一个元素**
**所以我们可以从数组的最后一位的下一位往前循环，将 array[i]赋值为 array[i-1]**循环到 1 停，将 array 的第 0 项赋值为需要添加的值。
过程如下
![](/images/array/unshift.png)
具体代码实现：

```javascript
Array.prototype._unshift = function(value) { for (let i = this.length; i > 0; i--) {
 this[i] = this[i - 1] } this[0] = value return this.length
}
var arr = [1, 2, 3, 4];
arr._unshift(8);
console.log(arr); // [ 8, 1, 2, 3, 4 ]
```

但上面的代码只实现了一个元素的头部添加，unshift 方法支持添加多个元素。例如：

```javascript
var arr = [1, 2, 3, 4]arr.unshift(8, 7)
console.log(arr); // [ 8, 7, 1, 2, 3, 4 ]
```

针对这样的情况，需要知道传入了几个参数，可以从 arguments 对象入手，思路还是上面的思路：
`先以最后生成的数组长度为基准从后往前循环，依次移动元素，然后将新元素依次放到数组的头部`
新数组的长度等于原数组的长度 + 参数的个数，从后往前循环，将原数组的最后一位，移动到新数组的最后一位，
因为需要在头部插入数量为入参个数的元素，所以循环的起点为原数组的长度 + 参数的个数，循环的终点为入参的个数。
但由于索引总是比长度少一位，所以起点和终点都需要减 1。
现在可以先把循环移动的逻辑写出来

```javascript
Array.prototype._unshift = function (...value) {
  for (
    var i = this.length + arguments.length - 1;
    i > arguments.length - 1;
    i--
  ) {
    this[i] = this[i - arguments.length];
  }
};
```

再思考一下，由于上一步已经移动完了，数组头部的位置已经空出来了，第二步是有几个参数就要插入几个元素。所以现在只需要循环插入就好：

```javascript
for (var k = 0; k < arguments.length; k++) {
  this[k] = arguments[k];
}
```

## 尾部删除 (pop)

`pop()函数将删除arrayObject的最后一个元素，把数组长度减1，并且返回它删除的元素的值，如果数组已经为空，则pop()不改变数组，并返回undefined值`
这个很好实现，按照定义一步一步做就可以。首先，记录下最后一个元素，便于返回，之后从数组中删除最后一个元素，
将其指向 null 释放掉，然后将数组的长度减 1，最后判断一下是否为空数组。

```javascript
Array.prototype._pop = function () { if (!this.length) {
 return undefined
 }
 var end = this[this.length - 1] this[this.length - 1] = null;
 this.length = this.length - 1;
 return end
 }

var arr = [1, 2, 3, 4];
arr._pop();
console.log(arr); // [ 1, 2, 3 ]
```

## 头部删除（shift）

`shift()函数用于把数组的第一个元素从其中删除，并返回第一个元素的值`
头部删除，会改变原有数组元素的索引，也就是将未被删除的元素索引都往左移一位，首先要将被删除的元素记录下来便于返回，之后将数组第一个元素指向 null，
最后循环数组，移动索引。

```javascript
Array.prototype._shift = function () {
  if (!this.length) {
    return undefined;
  }
  var start = this[0];
  this[0] = null;
  for (var i = 0; i < this.length - 1; i++) {
    this[i] = this[i + 1];
  }
  this.length = this.length - 1;
  return start;
};

var arr = [1, 2, 3, 4];
arr._shift();
console.log(arr); // [ 2, 3, 4 ]
```
