---
title: VSCode工作区配置-代码统一格式化
date: 2020-12-25 15:33:19
tags:
  - 工具
category: 代码格式化
---

问题原因：
解决前端项目格式化文件不统一问题
小程序使用 prettier 后报错：
![300*300](/images/vs-eslint/vs-eslint4.png)
解决问题可以直接修改 prettier 配置，但其他项目可能用不到其中的配置，这样提高了格式化配置项的耦合性，所以我们可以通过配置不同的项目格式化规范来减少我的配置次数。

## VSCode 层次关系

系统默认设置（不可修改）-用户设置-工作区设置-文件夹设置。
后者的设置会覆盖前者的设置，若没有设置某一项，将继续使用前者的设置。
用户设置即全局设置，用户自行设定好后，每次打开 VSCode 即使用的此设定，若某项无设定即使用默认设置。

工作区设置即工作环境设置，可对不同的工作环境是用不同的工作环境，若某项无设定，即使用上一层设置。

文件夹设置即为项目设置，将一个文件夹当成一个项目，对同一个工作环境下的不同项目，使用不同的设置，若某项无设定，即使用上一层设置。

## 如何新建一个工作区

大家应该都发现了，文件中没有“新建工作区”的选项。
打开文件会看到“将工作区另存为…”选项，这就代替了“新建工作区”，再不打开任何工作区、文件夹及文件的清空下，这个选项都可以使用。
![300*300](/images/vs-eslint/vs-eslint5.png)
如果在打开的文件夹的情况下保存工作区，会自动将此文件夹放入工作区，也建议这样使用。
工作区你可以把它想象成一个空间，创建一个有规则的空间进行代码的操作。
由于要上传到 git 远程仓库，所以要是你的项目中的.gitignore 文件中将.vscode 忽略了，记得将对应忽略项删除。

## 添加工作区中的配置

不同项目可以添加不同的配置，小程序项目中的配置是

```json
{
  // 配置文件关联，以便启用对应的智能提示
  "files.associations": {
    "*.wpy": "vue",
    "*.wxml": "wxml"
  },
  // 设置文字大小
  "editor.fontSize": 16,
  // 换行
  "editor.wordWrap": "on",
  // vetur中的首行缩进
  "vetur.format.options.tabSize": 2,
  // 用鼠标添加多个光标的修饰符。 “转到定义”和“打开链接”鼠标手势将进行调整，以使其与多光标修改器不冲突。
  "editor.multiCursorModifier": "ctrlCmd",
  // 控制片段是否与其他建议一起显示以及它们的排序方式。
  "editor.snippetSuggestions": "top",
  // 每次保存的时候将代码按eslint格式进行修复
  "eslint.autoFixOnSave": true,
  // eslint验证
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    {
      "language": "html",
      "autoFix": true
    },
    {
      "language": "vue",
      "autoFix": true
    },
    {
      "language": "wpy",
      "autoFix": true
    },
    {
      "language": "js",
      "autoFix": true
    },
    {
      "language": "jsx",
      "autoFix": true
    }
  ],
  // 格式化.vue中html
  "vetur.format.defaultFormatter.html": "js-beautify-html",
  // 控制通过垃圾箱删除文件时浏览器是否应要求确认。
  "explorer.confirmDelete": false,
  // 调整窗口的缩放级别
  "window.zoomLevel": 0,
  // 细节,配置gitlen中git提交历史记录的信息显示情况
  "gitlens.advanced.messages": {
    "suppressShowKeyBindingsNotice": true
  },
  // 控制资源管理器是否应请求确认以通过拖放移动文件和文件夹
  "explorer.confirmDragAndDrop": false,
  // 定义一个优先于所有其他格式化程序设置的默认格式化程序。必须是提供格式化程序的扩展名的标识符。
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  // 每次保存自动格式化
  "editor.formatOnSave": true,
  //
  "gitlens.views.lineHistory.enabled": true,
  // 在VS Code中重命名或移动文件时，启用/禁用导入路径的自动更新。
  "javascript.updateImportsOnFileMove.enabled": "always",
  // 保存时运行的代码操作类型
  "editor.codeActionsOnSave": {
    "source.fixAll": true
  },
  // 关闭liveserver提示
  "liveServer.settings.donotShowInfoMsg": true,
  // 覆盖当前所选颜色主题中的icon
  "workbench.iconTheme": "material-icon-theme",
  // 控制在显示建议列表时如何预选建议
  "editor.suggestSelection": "first",
  // 控制Visual Studio IntelliCode是否修改“编辑器”。suggestSelection '如果它被设置为一个值('最近使用的')，将导致IntelliCode建议的完成项不可见。
  "vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",
  // 覆盖当前所选颜色主题中的颜色
  "workbench.colorCustomizations": {},
  // prettier结束语末尾是否添加分号
  "prettier.trailingComma": "none",
  "prettier.printWidth": 200
}
```

当然由于小程序使用了 prettier，所以要在根目录下创建.prettierrc 文件，添加以下配置解决与 ESlint 的冲突和小程序格式化问题

```json
{
  "trailingComma": "none",
  "singleQuote": true,
  "printWidth": 80
}
```

当我们提交后 git 远端仓库的项目就有.vscode 文件夹存在，当我 clone 项目时就可以使用工作区的格式化配置，前提你的本地用户配置不会太精细导致重复覆盖。
