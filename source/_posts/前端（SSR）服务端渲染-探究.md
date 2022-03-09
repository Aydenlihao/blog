---
title: 前端（SSR）服务端渲染-探究
date: 2022-03-09 09:53:31
tags:
  - 技术动态
category: JavaScript
---

SSR 是 Service Side Render 简称，页面上的内容是通过服务端渲染生成，游览器直接显示服务端返回的 HTML 就可以了。

## 一、 使用 SSR 的利弊

### SSR 的优势

1.更利于 SEO

2.更利于首屏渲染

### SSR 的局限

1.服务端压力较大

2.开发条件受限

3.学习成本相对较高

## 二、使用架构

### Vue 可使用 [Nuxt.js](https://www.nuxtjs.cn/)

- 基于 Vue.js
- 自动代码分层
- 服务端渲染
- 强大的路由功能，支持异步数据
- 静态文件服务
- ES6/ES7 语法支持
- 打包和压缩 JS 和 css
- HTML 头部标签管理
- 本地开发支持热加载
- 集成 ESLint
- 支持各种样式预处理器： SASS、LESS、 Stylus 等等

### React 可使用 [Next.js](https://www.nextjs.cn/)

- 直观的、 基于页面 的路由系统（并支持 动态路由）
- 预渲染。支持在页面级的 静态生成 (SSG) 和 服务器端渲染 (SSR)
- 自动代码拆分，提升页面加载速度
- 具有经过优化的预取功能的 客户端路由
- 内置 CSS 和 Sass 的支持，并支持任何 CSS-in-JS 库
- 开发环境支持 快速刷新
- 利用 Serverless Functions 及 API 路由 构建 API 功能
- 完全可扩展
