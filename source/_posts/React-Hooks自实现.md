---
title: React Hooks自实现
date: 2020-09-07 10:58:59
tags:
  - React
category: JavaScript
---

## 了解 useReducer

useReducer 是 React16.8.0 中为数不多由官方提供的之一。它接受一个 ，以及一个初始的应用程序状态，然后返回当前应用程序的状态，和一个调度函数（dispatch）。
一个简单的例子：

```javaScript
const [state, dispatch] = useReducer(reducer, initialState);
```

## 从 useState 开始
