---
title: 本地存储的localStorage和sessionStorage
date: 2020-05-06 10:38:38
tags:
  - HTML5
category: JavaScript
---

## localStorage(本地存储)

localStorage 是只读的。数据存储也是跨浏览器会话。数据储存在 localStorage 是无期限的。
常用的四个 API 也很简单 ：

```javascript
// 增加了一个 localStorage ‘myCat’ 数据项
localStorage.setItem("myCat", "Tom");

// 读取 localStorage ‘myCat’ 数据项
let cat = localStorage.getItem("myCat");

// 移除 localStorage ‘myCat’ 数据项
localStorage.removeItem("myCat");

// 移除所有的 localStorage 数据项
localStorage.clear();
```

但需要注意的是，在移动设备上的浏览器或各 Native App 用到的 WebView 里，localStorage 都是不可靠的，可能会因为各种原因（比如说退出 App、网络切换、内存不足等原因）被清空。

## sessionStorage(会话存储)

当页面被关闭时,数据存储在 sessionStorage 会被清除

```javascript
// 增加了一个 sessionStorage ‘key’ 数据项
sessionStorage.setItem("key", "value");

// 读取 sessionStorage ‘key’ 数据项
let data = sessionStorage.getItem("key");

// 移除 sessionStorage ‘key’ 数据项
sessionStorage.removeItem("key");

//移除所有的 sessionStorage 数据项
sessionStorage.clear();
```

## localStorage 一些不为人知的方法

localStorage.hasOwnProperty() 检查 localStorage 中存储的数据里是否保存某个值

```javascript
localStorage.setItem("myCat", "Tom");
localStorage.hasOwnProperty("myCat"); // true
localStorage.hasOwnProperty("youCat"); // false
```

## storage 事件

当存储数据发生变化时，会触发 storage 事件。值得特别注意的是，该事件不在导致数据变化的当前页面触发。如果浏览器同时打开一个域名下面的多个页面，当其中的一个页面改变 sessionStorage 或 localStorage 的数据时，其他所有页面的 storage 事件会被触发，而原始页面并不触发 storage 事件。可以通过这种机制，实现多个窗口之间的通信。（当然 ie 这个特例除外，它包含自己本事也会触发 storage 事件）。

```javascript
window.addEventListener("storage", function onStorageChange(event) {});
```

event.key 属性：属性值为在 session 或 localStorage 中被修改的数据键值。
event.oldValue 属性：属性值为在 sessionStorage 或 localStorage 中被修改的值。
event.newValue 属性：属性值为在 sessionStorage 或 localStorage 中被修改后的值
event.url 属性：属性值为修改 sessionStorage 或 localStorage 中值的页面的 URL 地址
event.storageArea 属性 : 属性值为被变动的 sessionStorage 对象或 localStorage 对象

## 原理

在 HTML5 中，本地储存是一个 window 的属性，包括 localStrong 和 sessionStrong。localStrong 和 sessionStrong 都是储存在 window 里的 strong 实例对象，我们对 Window.sessionStorage 和 Window.localStorage 属性使用其实就是改变了 window 本地存储的对象。
Window 对象表示一个浏览器窗口或一个框架。在客户端 JavaScript 中，Window 对象是全局对象，所有的表达式都在当前的环境中计算。
