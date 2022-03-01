---
title: BFC(Block Fommatting context)
date: 2020-04-23 10:59:28
tags:
  - 视图
category: HTML5
---

## 什么是 BFC?

W3C 对 BFC 的定义如下： 浮动元素和绝对定位元素，非块级盒子的块级容器（例如 inline-blocks, table-cells, 和 table-captions），以及 overflow 值不为"visiable"的块级盒子，都会为他们的内容创建新的 BFC（Block Fromatting Context， 即块级格式上下文）。

**块格式化上下文（Block Formatting Context，BFC）** 是 Web 页面的可视化 CSS 渲染的一部分，是块盒子的布局过程发生的区域，也是浮动元素与其他元素交互的区域。

FC 是 formatting context 的首字母缩写，直译过来是格式化上下文，它是**页面中的一块渲染区域**，有一套渲染规则，决定了其**子元素如何布局，以及和其他元素之间的关系和作用**。

## 触发条件

一个 HTML 元素要创建 BFC，则满足下列的任意一个或多个条件即可： 下列方式会创建块格式化上下文：

- 根元素()
- 浮动元素（元素的 float 不是 none）
- 绝对定位元素（元素的 position 为 absolute 或 fixed）
- 行内块元素（元素的 display 为 inline-block）
- 表格单元格（元素的 display 为 table-cell，HTML 表格单元格默认为该值）
- 表格标题（元素的 display 为 table-caption，HTML 表格标题默认为该值）
- 匿名表格单元格元素（元素的 display 为 table、table-row、 table-row-group、table-header-group、table-footer-group（分别是 HTML table、row、tbody、thead、tfoot 的默认属性）或 inline-table）
- overflow 值不为 visible 的块元素 -弹性元素（display 为 flex 或 inline-flex 元素的直接子元素）
- 网格元素（display 为 grid 或 inline-grid 元素的直接子元素） 等等。

## BFC 渲染规则

1. BFC 垂直方向边距重叠
2. BFC 的区域不会与浮动元素的 box 重叠
3. BFC 是一个独立的容器，外面的元素不会影响里面的元素
4. 计算 BFC 高度的时候浮动元素也会参与计算

## 应用场景

1. 防止浮动导致父元素高度塌陷
   现有如下页面代码:

```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <style>
      .container {
        border: 10px solid red;
      }
      .inner {
        background: #08bdeb;
        height: 100px;
        width: 100px;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <div class="inner"></div>
    </div>
  </body>
</html>
```

![](/images/bfc1.png)
接下来将 inner 元素设为浮动:

```css
.inner {
  float: left;
  background: #08bdeb;
  height: 100px;
  width: 100px;
}
```

![](/images/bfc2.png)
但如果我们对父元素设置 BFC 后, 这样的问题就解决了:

```css
.container {
  border: 10px solid red;
  overflow: hidden;
}
```

2. 避免外边距折叠
   两个块同一个 BFC 会造成外边距折叠，但如果对这两个块分别设置 BFC，那么边距重叠的问题就不存在了。

现有代码如下:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <style>
      .container {
        background-color: green;
        overflow: hidden;
      }

      .inner {
        background-color: lightblue;
        margin: 10px 0;
      }
    </style>
  </head>

  <body>
    <div class="container">
      <div class="inner">1</div>
      <div class="inner">2</div>
      <div class="inner">3</div>
    </div>
  </body>
</html>
```

![](/images/bfc3.png)
此时三个元素的上下间隔都是 10px, 因为三个元素同属于一个 BFC。 现在我们做如下操作:

```html
<div class="container">
  <div class="inner">1</div>
  <div class="bfc">
    <div class="inner">2</div>
  </div>
  <div class="inner">3</div>
</div
```

style 增加:

```css
.bfc {
  overflow: hidden;
}
```

效果如下:
![](/images/bfc4.png)
可以明显地看到间隔变大了，而且是原来的两倍，符合我们的预期。

3. 相关链接
   https://juejin.im/post/5909db2fda2f60005d2093db
