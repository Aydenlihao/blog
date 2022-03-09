---
title: PC小程序的认真一拳
date: 2021-07-11 09:49:20
tags:
  - 工具
category: 小程序
---

自从微信 PC 端 2.7.0 版本以后，PC 端开始支持打开小程序，随之而来的技术的进步总是有问题的产生，PC 端与移动端显而易见的有了兼容性的问题。

## PC 端小程序

小程序的跨端功能是它的优势，正是因为它的跨度功能导致小程序在各端总会出现一些不能兼容各端功能的问题，不仅是移动端和 PC 端，还有 IOS 和 Android 端也会时常有问题发生。

## 差异

PC 端和移动端的主要差异在于微信 API 对后台系统的调用，所以框架上就有了不同：

- PC 端现在最流行框架 vue 开发,但 vue 不兼容 ie8 以下,,,,,,jquery 是没有兼容性,专门兼容 ie8，而移动端开发考虑的是更多的是手机兼容性,因为目前不管是 android 手机还是 IOS 手机,一般浏览器使用都是 webkit 内核;
- 一般 pc 端使用 jquery,,移动端一般使用 zepto,因为移动端的流量还是比较重要,所以引入的资源能小则小.

## 问题案例

[PC 端小程序图片上传](https://developers.weixin.qq.com/community/develop/doc/000c08d0408688c6594a08efb5b400)
在图片上传过程中小程序无法获取到 PC 端中的图片地址，导致图片无法获取

## 案例解决方案

这个问题的主要原因是在于 wx.uploadFile 中定义的 Content-type

```javaScript
wx.chooseImage({
    success(res){
        wx.uploadFile({
            url:'',//上传图片URL
            filePath:res.tempFilePaths[0],
            name:'file',
            formData:{},
            header:{
                //去掉这里的定义PC端和移动端就都没问题了
                //"Content-type":'multipart/form-data'
                // 'token':wx.getStorageSync('token')
            },
            success:(){

            }
        })
    }
});
```
