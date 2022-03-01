---
title: css -webkit-box-reflect 倒影特效
date: 2021-03-03 18:01:18
tags:
  - HTML5
category: css
---

<label style="background-color: #fff5f5;color:#ff502c;">webkit-box-reflect</label> 是一个非常有意思的属性，它让 CSS 有能力像镜子一样，反射我们元素原本绘制的内容
上一次写它，它的兼容性还非常非常的惨淡，但是到今天，虽然还是一个 Non-standard 的语法，但是兼容性已经大有改观。
截止至 2021-02-19，它的兼容性已经达到了 91.02%，看看[CANIUSE -webkit-box-reflect:](https://caniuse.com/?search=-webkit-box-reflect)
![](/images/reflect/reflect_method.png)

## 基本用法

```css
div {
  -webkit-box-reflect: below;
}
```

below 可以是 below | above | left | right 代表下上左右，也就是有 4 个方向可以选。
![](/images/reflect/reflect_show.png)

## 设置倒影距离

在方向后面，还可以接一个具体的数值大小，表示倒影与原元素间的距离。

```css
div {
  background-image: url("https://images.pokemontcg.io/xy2/12_hires.png");
  -webkit-box-reflect: right 10px;
}
```

加上 10px 之后，倒影与原元素间将间隔 10px

## 设置倒影虚实

还有一个非常重要的功能，就是方位后面，还能再设置一个渐变值，利用这个渐变值，可以实现倒影的一个虚化效果，这一点非常重要。

```css
div {
  background-image: url("https://images.pokemontcg.io/xy2/12_hires.png");
  -webkit-box-reflect: below 2px linear-gradient(transparent, rgba(0, 0, 0, 0.5));
}
```

## 使用 -webkit-box-reflect 创造艺术图案

```
<div class="g-wrap1">
    <div class="g-wrap2">
        <div class="g-wrap3">
            <div class="g-wrap4"></div>
        </div>
    </div>
</div>
```

从最深处的子字节绘制一张图片，一层叠一层进行多次的倒影翻转,就会从
![](/images/reflect/reflect_first.png)
进过多次对称显示为
![](/images/reflect/reflect_last.png)
