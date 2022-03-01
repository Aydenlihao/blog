---
title: 你可能还不知的 CSS 好用的属性
date: 2020-05-11 17:31:18
tags:
  - HTML5
category: css
---

在这篇文章中，向你介绍了几个比较少见且好用的 CSS 属性，希望对你有所帮助

## writing-mode

<label style="background-color: #fff5f5;color:#ff502c;">writing-mode</label>属性定义了文本水平或者垂直排布以及在哪块级元素中文本的进行方向。为整个文档设置书时，应在根元素上设置它（对于 HTML 文档应该在 HTML 元素上设置）。它采用以下值之一<label style="background-color: #fff5f5;color:#ff502c;">horizontal-tb (default) | vertical-rl | vertical-lr</label>。
<label style="background-image: -webkit-linear-gradient(bottom, red, #fd8403, yellow); 
-webkit-background-clip: text; -webkit-text-fill-color: transparent;">horizontal-tb：</label>对于左对齐(ltr)脚本，内容从左到右水平流动。对于右对齐(rtr)脚本，内容从右到左水平流动。下一水平行位于上一行下方。
<label style="background-image: -webkit-linear-gradient(bottom, red, #fd8403, yellow);  
 -webkit-background-clip: text; -webkit-text-fill-color: transparent;">vertical-rl：</label>对于左对齐(ltr)脚本，内容从上到下垂直流动，下一垂直行位于上一行左侧。对于右对齐(rtr)脚本，内容从下到上垂直流动，下一垂直行位于上一行右侧。
<label style="background-image: -webkit-linear-gradient(bottom, red, #fd8403, yellow); 
-webkit-background-clip: text; -webkit-text-fill-color: transparent;">vertical-lr：</label>对于左对齐(ltr)脚本，内容从上到下垂直流动，下一垂直行位于上一行右侧。对于右对齐(rtr)脚本，内容从上到下垂直流动，下一垂直位于上一行左侧。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="box" class="box">
      <div>1</div>
      <div>2</div>
      <div>3</div>
      <div>4</div>
    </div>
    <div>
      <button id="one">horizontal-tb</button>
      <button id="two">vertical-lr</button>
      <button id="three">vertical-rl</button>
    </div>
  </body>
  <style>
    .box {
      width: 400px;
      height: 300px;
      writing-mode: horizontal-tb;
    }
    .box div {
      background: red;
      margin: 10px;
      width: 100px;
      height: 100px;
    }
  </style>
  <script>
    var one = document.getElementById("one");
    var two = document.getElementById("two");
    var three = document.getElementById("three");
    var box = document.getElementById("box");
    one.onclick = function (params) {
      box.style.writingMode = "horizontal-tb";
    };
    two.onclick = function (params) {
      box.style.writingMode = "vertical-lr";
    };
    three.onclick = function (params) {
      box.style.writingMode = "vertical-rl";
    };
  </script>
</html>
```

## font-variant-numeric

<label style="background-color: #fff5f5;color:#ff502c;">font-variant-numeric</label>CSS 属性控制数字，分数和序号标记的替代字形的使用。
它采用余下这些值之一：<label style="background-color: #fff5f5;color:#ff502c;">normal | ordinal | slashed-zero | lining-nums | oldstyle-nums | proportional-nums | tabular-nums | diagonal-fractions | stacked-fractions</label>
此属性对于设置数字样式很有用。根据情况，你可能希望显示老式的数字或带有斜杠的零，对于这些情况，<label style="background-color: #fff5f5;color:#ff502c;">font-variant-numeric</label>很有用。
请注意，<label style="background-color: #fff5f5;color:#ff502c;">font-variant-numeric</label>是<label style="background-color: #fff5f5;color:#ff502c;">font-feature-setting</label>组属性的一部分。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="https://code.cdn.mozilla.net/fonts/fira.css" />
  </head>
  <body>
    <div id="box" class="box">
      1234567890
    </div>
    <div>
      <button id="one">normal</button>
      <button id="two">ordinal</button>
      <button id="three">slashed-zero</button>
      <button id="four">lining-nums</button>
      <button id="five">oldstyle-nums</button>
      <button id="six">proportional-nums</button>
      <button id="seven">tabular-nums</button>
      <button id="eight">diagonal-fractions</button>
      <button id="nine">stacked-fractions</button>
    </div>
  </body>
  <style type="text/css">
    body {
      font: 16px/1.5 sans-serif;
      font-family: "Fira Sans", sans-serif;
    }
  </style>
  <script>
    var one = document.getElementById("one");
    var two = document.getElementById("two");
    var three = document.getElementById("three");
    var four = document.getElementById("four");
    var five = document.getElementById("five");
    var six = document.getElementById("six");
    var seven = document.getElementById("seven");
    var eight = document.getElementById("eight");
    var nine = document.getElementById("nine");
    one.onclick = function (params) {
      box.style.fontVariantNumeric = "normal";
    };
    two.onclick = function (params) {
      box.style.fontVariantNumeric = "ordinal";
    };
    three.onclick = function (params) {
      box.style.fontVariantNumeric = "slashed-zero";
    };
    four.onclick = function (params) {
      box.style.fontVariantNumeric = "lining-nums";
    };
    five.onclick = function (params) {
      box.style.fontVariantNumeric = "oldstyle-nums";
    };
    six.onclick = function (params) {
      box.style.fontVariantNumeric = "proportional-nums";
    };
    seven.onclick = function (params) {
      box.style.fontVariantNumeric = "tabular-nums";
    };
    eight.onclick = function (params) {
      box.style.fontVariantNumeric = "diagonal-fractions";
    };
    nine.onclick = function (params) {
      box.style.fontVariantNumeric = "stacked-fractions";
    };
  </script>
</html>
```

## user-select

每当我们有不想让用户选择的文本，或者相反，如果发生了双击或上下文单击，希望选择所有文本时，<label style="background-color: #fff5f5;color:#ff502c;">user-select</label>属性将非常有用。
none:不允许选中
all:选中全部
text:可以选择文本
element：可以选择文本，但选择范围受元素边界的约束

```html
<<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <p>You should be able to select this text.</p>
    <p class="unselectable">Hey, you can't select this text!</p>
    <p class="all">Clicking once will select all of this text.</p>
    <p class="text"><img src='./round-balloon.png'/><div>Clicking once will select all of this text</div></p>
    <p class="texts"><img src='./round-balloon.png'/><div>Clicking once will select all of this text</div></p>
    <style>
      .unselectable {
        -moz-user-select: none;
        -webkit-user-select: none;
        -ms-user-select: none;
        user-select: none;
      }

      .all {
        -moz-user-select: all;
        -webkit-user-select: all;
        -ms-user-select: all;
        user-select: all;
      }
      .text {
        -moz-user-select: text;
        -webkit-user-select: text;
        -ms-user-select: text;
        user-select: text;
      }
      .texts{
        -moz-user-select: element;
        -webkit-user-select: element;
        -ms-user-select: element;
        user-select: element;
      }
    </style>
  </body>
</html>
```

## shape-outside

<label style="background-color: #fff5f5;color:#ff502c;">shape-outside</label>的 CSS 属性定义了一个可以是非矩形的形状，相邻的内联内容应该围绕该形状进行包装。默认情况下，内联内容包围其边边距框；<label style="background-color: #fff5f5;color:#ff502c;">shape-outside</label>提供了一种自定义此包装的方法，可以将文本包装在复杂对象周围而不是简单的框中。它采用与<label style="background-color: #fff5f5;color:#ff502c;">clip-path</label>相同的值。
<label style="background-color: #fff5f5;color:#ff502c;">clip-path</label>定义用户如何查看元素，<label style="background-color: #fff5f5;color:#ff502c;">shape-outside</label>定义其他 HTML 元素如何查看元素。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="https://code.cdn.mozilla.net/fonts/fira.css" />
  </head>
  <body>
    <div class="box">
      <img id="box" src="./round-balloon.png" />
      We had agreed, my companion and I, that I should call for him at his
      house, after dinner, not later than eleven o’clock. This athletic young
      Frenchman belongs to a small set of Parisian sportsmen, who have taken up
      “ballooning” as a pastime. After having exhausted all the sensations that
      are to be found in ordinary sports, even those of “automobiling” at a
      breakneck speed, the members of the “Aéro Club” now seek in the air, where
      they indulge in all kinds of daring feats, the nerve-racking excitement
      that they have ceased to find on earth.
    </div>
    <div>
      <button id="one">circle</button>
      <button id="two">ellipse</button>
      <button id="three">url</button>
      <button id="four">polygon</button>
    </div>
  </body>
  <style type="text/css">
    body {
      font: 16px/1.5 sans-serif;
      font-family: "Fira Sans", sans-serif;
    }
    .box {
      width: 300px;
    }
    .box img {
      width: 150px;
      float: left;
    }
  </style>
  <script>
    var one = document.getElementById("one");
    var two = document.getElementById("two");
    var three = document.getElementById("three");
    var four = document.getElementById("four");
    one.onclick = function (params) {
      box.style.shapeOutside = "circle(50%)";
    };
    two.onclick = function (params) {
      box.style.shapeOutside = "ellipse(130px 140px at 20% 20%)";
    };
    three.onclick = function (params) {
      box.style.shapeOutside = "url(./round-balloon.png)";
    };
    four.onclick = function (params) {
      box.style.shapeOutside = "polygon(50% 0, 100% 50%, 50% 100%, 0 50%)";
    };
  </script>
</html>
```

## background-clip

<label style="background-color: #fff5f5;color:#ff502c;">backgroundclip</label> CSS 属性设置元素的背景是否扩展到其<label style="background-color: #fff5f5;color:#ff502c;">border</label> 、<label style="background-color: #fff5f5;color:#ff502c;">padding</label> 或<label style="background-color: #fff5f5;color:#ff502c;">content</label> 框之下

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="https://code.cdn.mozilla.net/fonts/fira.css" />
  </head>
  <body>
    <div id="box" class="box">
      This is the content of the element.
    </div>
    <div>
      <button id="one">broder</button>
      <button id="two">padding</button>
      <button id="three">content</button>
      <button id="four">text</button>
    </div>
  </body>
  <style type="text/css">
    body {
      font: 16px/1.5 sans-serif;
      font-family: "Fira Sans", sans-serif;
    }
    .box {
      background-image: url("./hand.jpg");
      color: #fff;
      padding: 20px;
      border: 10px dashed #333;
      font-size: 2em;
      font-weight: 700;
    }
  </style>
  <script>
    var one = document.getElementById("one");
    var two = document.getElementById("two");
    var three = document.getElementById("three");
    var four = document.getElementById("four");
    one.onclick = function (params) {
      box.style.backgroundClip = "border-box";
      box.style.color = "#000";
    };
    two.onclick = function (params) {
      box.style.backgroundClip = "padding-box";
      box.style.color = "#000";
    };
    three.onclick = function (params) {
      box.style.backgroundClip = "content-box";
      box.style.color = "#000";
    };
    four.onclick = function (params) {
      box.style.backgroundClip = "text";
      box.style.webkitBackgroundClip = "text";
      box.style.webkitTextFillColor = "transparent";
    };
  </script>
</html>
```

## background-attachment

<label style="background-color: #fff5f5;color:#ff502c;">background-attachment</label>属性设置背景图像是否固定或者随着页面的其余部分滚动。
<label style="background-image: -webkit-linear-gradient(bottom, red, #fd8403, yellow);  
 -webkit-background-clip: text; -webkit-text-fill-color: transparent;">scroll(default)：</label>背景图像会随着页面其余部分的滚动而移动。
<label style="background-image: -webkit-linear-gradient(bottom, red, #fd8403, yellow);  
 -webkit-background-clip: text; -webkit-text-fill-color: transparent;">fixed：</label>当页面的其余部分滚动时，背景图像不会移动。
<label style="background-image: -webkit-linear-gradient(bottom, red, #fd8403, yellow);  
 -webkit-background-clip: text; -webkit-text-fill-color: transparent;">inherit：</label>规定应该从父元素继承属性设置值。

```html
<html>
  <head>
    <style type="text/css">
      body {
        background-image: url("./hand.jpg");
        background-repeat: no-repeat;
        background-attachment: fixed;
      }
    </style>
  </head>

  <body>
    <p>图像不会随页面的其余部分滚动。</p>
    <p>A</p>
    <p>B</p>
    <p>C</p>
    <p>D</p>
    <p>E</p>
    <p>F</p>
    <p>G</p>
    <p>H</p>
    <p>I</p>
    <p>J</p>
    <p>K</p>
    <p>L</p>
    <p>M</p>
    <p>N</p>
    <p>O</p>
    <p>P</p>
    <p>Q</p>
    <p>R</p>
    <p>S</p>
    <p>T</p>
    <p>W</p>
    <p>X</p>
    <p>Y</p>
    <p>Z</p>
    <p>1</p>
    <p>2</p>
    <p>3</p>
    <p>4</p>
    <p>5</p>
    <p>6</p>
    <p>7</p>
    <p>8</p>
    <p>9</p>
  </body>
</html>
```

## outline

<label style="background-color: #fff5f5;color:#ff502c;">outline</label>是绘制于元素周围的一条线，位于边框边缘的外围，可以起到突出元素的作用。<label style="background-color: #fff5f5;color:#ff502c;">outline</label>中有设置所有的轮廓属性，属性如下：outline-color、outline-style、outline-width。
outline-color：设置轮廓颜色
outline-style：设置轮廓样式
outline-width：设置轮廓的宽度
<label style="background-image: -webkit-linear-gradient(bottom, red, #fd8403, yellow);  
 -webkit-background-clip: text; -webkit-text-fill-color: transparent;">outline-style：</label>

- dotted:点状
- dashed:虚线
- solid: 实线
- double:双线
- groove: 凹槽(3d)
- ridge: 山脊(3d)
- inset: 内凹(3d)
- outset: 外凸(3d)

```html
<html>
  <head>
    <style type="text/css">
      p {
        border: red solid thin;
        outline: #00ff00 dotted thick;
      }
    </style>
  </head>

  <body>
    <p>
      <b>注释：</b>只有在规定了 !DOCTYPE 时，Internet Explorer 8
      （以及更高版本） 才支持 outline 属性。
    </p>
  </body>
</html>
```
