---
title: Taro特色UI vant-ui
date: 2021-07-11 09:43:47
tags:
  - 工具
category: 小程序
---

## 引入 vant-ui 到 taro 中

### 配置 vant-ui 中项目的尺寸的转换

将下列代码加入项目的 config/index.js 文件中

```js
// config/index.js
const config = {
  // ...
  mini: {
    postcss: {
      pxtransform: {
        enable: true,
        config: {
          selectorBlackList: [/van-/],
        },
      },
    },
  },
};
```

### 配置小程序原生组件文件

由于 vant 的有些组件依赖于小程序的原生组件，所以要对这些组件进行本地文件的添加
[下载地址]('https://github.com/NervJS/taro3-vant-sample/tree/react/src')
下载好文件后添加项目下的 component 文件夹下
将下列代码加入项目的 config/index.js 文件中

```js
// config/index.js
const config = {
  // ...
  copy: {
    patterns: [
      {
        from: "src/components/vant-weapp/dist/wxs",
        to: "dist/components/vant-weapp/dist/wxs",
      },
      {
        from: "src/components/vant-weapp/dist/common/style",
        to: "dist/components/vant-weapp/dist/common/style",
      },
      {
        from: "src/components/vant-weapp/dist/common/index.wxss",
        to: "dist/components/vant-weapp/dist/common/index.wxss",
      },
      {
        from: "src/components/vant-weapp/dist/calendar/index.wxs",
        to: "dist/components/vant-weapp/dist/calendar/index.wxs",
      },
      {
        from: "src/components/vant-weapp/dist/calendar/utils.wxs",
        to: "dist/components/vant-weapp/dist/calendar/utils.wxs",
      },
      {
        from: "src/components/vant-weapp/dist/calendar/calendar.wxml",
        to: "dist/components/vant-weapp/dist/calendar/calendar.wxml",
      },
      {
        from: "src/components/vant-weapp/dist/calendar/components/month/index.wxs",
        to: "dist/components/vant-weapp/dist/calendar/components/month/index.wxs",
      },
    ],
    options: {},
  },
};
```

### 引用 vant 组件

首先需要在 **app** 的 config 或页面的 config 文件中配置 **usingComponents** 字段

```js
export default {
  navigationBarTitleText: "首页",
  usingComponents: {
    "van-button": "../../components/vant-weapp/dist/button/index",
  },
};
```

### 使用 vant 组件

#### React

```jsx
import React, { Component } from "react";
import { View } from "@tarojs/components";

export default class Index extends Component {
  render() {
    return (
      <View>
        <van-button type="primary" loading loading-text="ing">
          Button
        </van-button>
      </View>
    );
  }
}
```

#### Vue

```jsx
<template>
  <view>
    <van-button type='primary' :loading='true' loading-text='ing'>Button</van-button>
  </view>
</template>

<script>
export default {
  name: 'index'
}
</script>
```

**注意：如果组件的某些属性在 vant 文档里写着带有默认值 true，在 Taro 中使用时仍然需要显式设置为 true。**
