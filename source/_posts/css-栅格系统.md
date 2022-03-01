---
title: css 栅格系统
date: 2020-11-13 16:42:31
tags:
  - HTML5
category: css
---

## Grid

CSS 栅格布局中最重要的两个元素是 wrapper（parent） 和 items（children）。wrapper 实际上就是栅格，而 items 就是栅格里面的元素。
以下面的代码为例：

```Html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div class="wrapper">
        <div class='item1'>1</div>
        <div class='item2'>2</div>
        <div class='item3'>3</div>
        <div class='item4'>4</div>
        <div class='item5'>5</div>
        <div class='item6'>6</div>
      </div>
</body>
<style>
    .wrapper{
        display: grid;
    }
</style>
</html>
```

让这个 div 标签成为栅格，我们只需将他的 display 属性设置为 grid：

```css
.wrapper {
  display: grid;
}
```

在我们还未做任何后续操作的时候它看起来是这样的：
![](/images/grid/grid1.png)

## Columns and rows

我们需要为这个容器定义行和列，现在将这个容器分割成两行三列，需要用到 grid-template-row 和 grid-template-column 属性：

```css
.wrapper {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 50px 50px;
}
```

当我们这样去定义 grid-template-columns 时，我们将得到三列，列长就是我们设置的大小，同理 grid-template-rows 也是一样。
于是我们得到下面的结果：
![](/images/grid/grid2.png)
为了看清楚他们之间的关系，我们修改下代码再看看结果：

```css
.wrapper {
  display: grid;
  grid-template-columns: 200px 50px 100px;
  grid-template-rows: 100px 30px;
}
```

会得到以下样式：
![](/images/grid/grid3.png)

## Item

接下来需要了解的是，在栅格系统中的元素是如何放置的。

我们创建一个 3\*3 的栅格，HTML 仍然使用前面的：

```css
.wrapper {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
}
```

会出现：
![](/images/grid/grid4.png)
你会发现我们的结果中展示的是 3*2 的栅格，而我们在 CSS 代码中定义的是 3*3 的栅格，那是因为我们的容器中只有六个元素，如果我们在 HTML 中定义了 9 个元素，那么结果就会是一个 3\*3 的栅格

为了重新定位并调整这些元素的大小，我们要对该元素使用 grid-column 和 grid-row 属性

```css
.item1 {
  grid-column-start: 1;
  grid-column-end: 4;
}
```

上面的代码意图是，我们想让 item1 的起点在第一列并且终止在第四列，也就是说，我们想让它独占一行，下面是运行的结果：
![](/images/grid/grid5.png)
前面代码中的 grid-column-end: 4; 可能会让人产生困惑，因为我们实际结果中只得到了三列，但是看看下面的图片就能明白了：
![](/images/grid/grid6.png)
当第一个元素占满第一行时，其他的元素将向下顺延。
上面那段代码其实还有一种更简单的写法：

```css
.item1 {
  grid-column: 1 / 4;
}
```

接下来我们来做一些更复杂一点的操作：

```css
.item1 {
  grid-column-start: 1;
  grid-column-end: 3;
}
.item3 {
  grid-row-start: 2;
  grid-row-end: 4;
}
.item4 {
  grid-column-start: 2;
  grid-column-end: 4;
}
```

![](/images/grid/grid7.png)
