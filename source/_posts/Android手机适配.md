---
title: Android手机适配
date: 2020-08-17 17:50:03
tags:
  - App应用
category: Java
---

## UI 设计图

<label style="background-color: #fff5f5;color:#ff502c;">推荐 1 倍效果图，即采用 720*360 大小</label>：
一倍图：720*360
二倍图：1280*720
三倍图：1920*1080
采用一倍图的主要原因是因为 1px=1dp,可以直接使用 px 值设置尺寸

## 屏幕各项参数

- <label style="background-color: #fff5f5;color:#ff502c;">手机像素（px）</label>：一个小黑点（组成屏幕显示的一个个点）就是像素；
- <label style="background-color: #fff5f5;color:#ff502c;">手机尺寸</label>：屏幕对角线的长度；
- <label style="background-color: #fff5f5;color:#ff502c;">手机分辨率</label>：整个屏幕一共有多少个点（像素）
- <label style="background-color: #fff5f5;color:#ff502c;">像素密度（dpi）</label>:
  1. 每英寸中的像素点数（假如设备分辨率为 320\*240，屏幕长 2 英寸宽 1.5 英寸，dpi=320/2 = 240/1.5 =160）;
  2. 对应 DisplayMetrics 类中属性 densityDpi 的值;
  3. 当然这种宽和高的 dpi 都相同的情况现在已经很少见，
     像素密度(dpi)、屏幕尺寸、分辨率三者关系：
     ![](/images/dpi/sin.png)
     举例说明：屏幕分辨率为：1920\*1080，屏幕尺寸为 5 吋的话，那么 dpi 为 440：
     ![](/images/dpi/sin2.png)
- <label style="background-color: #fff5f5;color:#ff502c;">密度（density）</label>：

1.  每平方英寸中的像素数（density = dpi / 160 ）；
2.  对应于 DisplayMetrics 类中属性 density 的值；
3.  可用于 px 与 px 与 dip 的互相转换 ：dp = px / density （所以具体换算就是 1dp = density px）；
    720P,和 1080P 的手机，dpi 是不同的，这也就意味着，不同的分辨率中，1dp 对应不同数量的 px(720P 中，1dp=2px，1080P 中 1dp=3px)。

- <label style="background-color: #fff5f5;color:#ff502c;">设备独立像素（dp、dip）</label>：

1. 不同设备有不同的显示效果，不依赖像素（dp = px / density = px / (dpi / 160) ）
2. dpi（像素密度）为 160 的设备上 1dp = 1px。

- <label style="background-color: #fff5f5;color:#ff502c;">放大像素（sp）</label>：用于字体显示；
- <label style="background-color: #fff5f5;color:#ff502c;">dp 转 px、px 转 dp</label>：

```java
public class Dp2Px {
    public static int dp2px(Context context, int dp) {
        return (int) (dp * context.getResources().getDisplayMetrics().density + 0.5);
    }

    public static int px2dp(Context context, int px) {
        return (int) (px / context.getResources().getDisplayMetrics().density + 0.5);
    }
}
```

## 屏幕适配

可以通过手机的分辨率设置不同的尺寸设置文件
![](/images/dpi/sin1.png)
里面内容是以 dip 为多少 px 设置，例如：

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
<dimen name="x1">1.5px</dimen>
<dimen name="x2">3.0px</dimen>
<dimen name="x3">4.5px</dimen>
<dimen name="x4">6.0px</dimen>
<dimen name="x5">7.5px</dimen>
```
