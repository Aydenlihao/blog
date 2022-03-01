---
title: VSCode合理配置ESLint+Prettier
date: 2020-11-27 14:46:31
tags:
  - 工具
category: 代码格式化
---

当前出现 VSCode 代码格式化无效问题

# 解决方案

在 vscode 上配置 Eslint+Prettier

## 安装插件

安装 eslint、prettier 插件
![](/images/vs-eslint/vs-eslint1.png)
![](/images/vs-eslint/vs-eslint2.png)

## 插件使用

这里你可以直接修改 vscode 的 setting.json 文件

```json
{
  "[vue]": {
    //这是重点，将prettier的配置用于vscode的文件
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "eslint.alwaysShowStatus": true,
  "eslint.format.enable": true,
  "eslint.packageManager": "yarn",
  "eslint.run": "onSave",
  "prettier.packageManager": "yarn",
  "eslint.validate": ["vue", "javascript", "javascriptreact"],
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "vetur.validation.template": false,
  "editor.formatOnPaste": true,
  "editor.formatOnType": true,
  "editor.formatOnSave": true,
  "files.eol": "\n"
}
```

接下来会有一个 eslint 和 prettierrc 格式化方式冲突的现象
![](/images/vs-eslint/vs-eslint3.png)
解决方案就是修改根目录下的 eslintrc.js 文件中的配置，文件中 extends（规则继承） 的默认配置是<label style="background-color: #fff5f5;color:#ff502c;">standard</label>，这是调用了https://github.com/feross/standard/blob/master/RULES.md#javascript-standard-style 中对 JavaScript 的标准样式，所以我们要添加与 prettierrc 的兼容性

```js

extends: ["plugin:prettier/recommended"],
...
将以下规则注释
 // "comma-dangle": ["error", {
        //     "imports": "never",
        //     "exports": "never",
        //     "functions": "ignore"
        // }],
...
```

这样就可以正常的使用我们的代码格式化了
