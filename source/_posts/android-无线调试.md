---
title: android 无线调试
date: 2022-05-31 10:21:40
tags:
  - App应用
category: Java
---

传统 APP 调试方法都是 usb 有线调试，这种方式不仅限制的 APP 测试的有线范围，也同样影响开发效率

## APP 无线调试

要确保手机和电脑在同一局域网下，这样的两台设置才能建立有线的 ADB 连接

### 下载 ADB 测试插件

```JavaScript
brew install --cask android-platform-tools
```

### 连接 APP 工具

使用 USB 连接手机

```JavaScript
//检测连接设备列表
adb devices
```

出现下提示说明设备连接成功
![](/images/android/device.png)

### 开启无线连接

```JavaScript
//开启连接端口，这里我所用的端口时5555
adb tcpip 5555
```

接下来需要知道手机在局域网中的 IP,一般手机可以在设置 → 关于手机 →IP 中查看到

```JavaScript
//连接移动端
adb connect 172.10.56.93:5555
//断开连接
adb disconnect 172.10.56.93:5555
```

当端口或者服务被阻塞、占用时，可以杀死进程进行重启

```JavaScript
//查看所有服务
 adb server
//杀死对应服务，这里的阻塞服务IP是45142
adb kill-server 45142
```

## APP 文件读取工具

用于 PC 端直接操作移动端文件，在做一下文件管理功能时十分有效

### 安装插件

```javaScript
 brew install --cask android-file-transfer
```

![](/images/android/flie.png)
