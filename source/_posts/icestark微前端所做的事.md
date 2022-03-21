---
title: icestark微前端所做的事
date: 2022-03-21 20:49:54
tags:
  - 工具
category: JavaScript
---

_icestark_ 是一个面向大型系统的微前端解决方案

## 项目初始化

### 初始化主应用

```shell
$ npm init ice icestark-layout @icedesign/stark-layout-scaffold
# 或者基于 Vue 的主应用
$ npm init ice icestark-layout @vue-materials/icestark-layout-app

$ cd icestark-layout
$ npm install
$ npm start
```

### 初始化子应用

```shell
# 基于 React 的微应用
$ npm init ice icestark-child @icedesign/stark-child-scaffold
# 基于 Vue 的微应用
$ npm init ice icestark-child @vue-materials/icestark-child-app

$ cd icestark-child
$ npm install
$ npm run start

```

## 兼容性

现代浏览器和 IE11 及以上

## icestark 与 qiankun 的爱恨情仇

icestark 与 qiankun 同为阿里开发的微前端方案，其中就存在着很多故事，qiankun 是基于 single-spa 而封装了隔离及共享机制的框架，其简化了 single-spa 的相关生命周期，并且提供了沙箱隔离机制及共享机制。icestark 是淘系团队的一个全流程前端框架，拥有强大的生态系统。
当然其中两者也存在着弊端
qiankun:

- 对于混合微前端方式不友好，如跨标签页、iframe 内嵌通讯
- 对于事件不能自定义，单一应用只有一个回调可用
- 不可剥离微前端框架
  icestark:
- window 对象托管 store 不安全，易被数据劫持和篡改

## 相关文件

[github](https://github.com/ice-lab/icestark)
[icestark](https://icestark.gitee.io/)
