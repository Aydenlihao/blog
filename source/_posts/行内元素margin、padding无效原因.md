---
title: 行内元素margin、padding无效原因
date: 2020-10-30 15:59:49
tags:
  - HTML5
category: css
---

行内元素：可以一行存在多个标签，对宽高属性值不生效，完全靠内容撑开宽高！
经过验证后，发现 top/bottom(padding-top/padding-bottom)、top/bottom(margin-top/margin-bottom)这 4 个属性是可以设置的

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div class="wrap">
      <span class="inline-element"
        ><a href="">北京</a><a href="">上海</a><a href="">天津</a
        ><a href="">辽宁</a><a href="">吉林</a><a href="">黑龙江</a></span
      >
    </div>
  </body>
  <style>
    * {
      padding: 0;
      margin: 0;
    }
    div.wrap {
      width: 200px;
      height: 200px;
      border: 1px solid red;
      margin: 10px;
      word-wrap: break-word;
    }
    .inline-element a {
      margin: 20px 20px 0 0;
      padding: 5px 5px 0 0;
      height: 20px;
      line-height: 20px;
      background: #ccc;
    }
  </style>
</html>
```

查 w3c 的官方文档并没有找到这个奇葩现象解释（可能我英语比较烂，没找到），后来在一篇老外的文章里找到了答案：

> While padding can be applied to all sides of an inline element, only left and right padding will have an effect on surrounding content. In the example below, 50px of padding has been applied to all sides of the element. As you can see, it has an affect on the content on each side, but not on content above or below

翻译：
虽然内嵌元素的所有边距都可以应用，但只有左右边距对周围内容有影响。在下面的例子中，50px 的填充被应用到元素的所有边。可以看到，它对周围的内容有影响。在下面的例子中，50px 的填充被应用到元素的所有边。可以看到，它对每一边的内容都有影响，但对上面或下面的内容没有影响

上图中我们设置 margin-top 和 padding-top 的值，但在设置中由于 padding-top 虽然生效但对周围的元素没有造成影响，所以如果颜色为透明就无法看出 padding 效果。marign 因为无法撑起页面高度所以无法直接作用于元素的高度显示。
