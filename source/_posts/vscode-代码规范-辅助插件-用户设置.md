---
title: VS Code 代码规范-辅助插件-用户设置
tags:
  - VS Code
  - ES Lint
date: 2018-05-22 11:16:26
updated: 2018-05-22 11:16:26
---

> 每一家技术成熟的公司都有自己的一套代码风格规范，我们必须要去遵从这些规范才能够去更好的融入团队，一个好的脚本编辑器，一个套自动化代码格式化插件及私有化配置有助于提高我们的工作效率，将更多的精力投入到主要的业务代码处理中。
> ...................................................................................................

目前刚加入一家新公司，前端技术团队定义好了一套 ES Lint 代码检查，用于统一团队的代码风格。当然，对于编辑器的选择是因人而异的，电脑高配置就上 WebStorm,电脑低配置就上 VS code.所以我选择了 VS Code o(╯□╰)o~~~

下面是目前团队的 ES Lint 检查规范

```js
// https://eslint.org/docs/user-guide/configuring
module.exports = {
  root: true,
  parser: 'babel-eslint',
  parserOptions: {
    sourceType: 'module'
  },
  env: {
    browser: true
  },
  // https://github.com/standard/standard/blob/master/docs/RULES-en.md
  extends: 'standard',
  // required to lint *.vue files
  plugins: ['html'],
  // add your custom rules here
  rules: {
    // allow async-await
    'generator-star-spacing': 'off',
    // allow debugger during development
    'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off',
    semi: [2, 'always'], // 语句强制分号结尾
    'one-var': 0, // 连续声明
    'no-unused-expressions': 0, // 禁用无效的表达式
    indent: [0, 4], // 缩进风格
    'no-use-before-define': 0, // 未定义前不能使用
    'no-unneeded-ternary': 0, // 禁止不必要的嵌套 var isYes = answer === 1 ? true : false;
    'no-tabs': 'off', // 禁止tabs键
    'no-redeclare': 0 //禁止重复声明变量
  }
};
```

前端目前使用的框架是 Vue 2+,所以在插件方面我选择了

```js
Vetur : 针对 Vue 开发提供的工具，包括函数高亮，智能提醒，格式化，代码片段，Emmet，错误检查，调试等
ESLint ：JS 代码规范提醒
Prettier ：代码格式化，支持html,css,js,ts,json等
```

VS Code 用户设置

```json
{
  "editor.multiCursorModifier": "ctrlCmd",
  "git.ignoreMissingGitWarning": true,
  "html.format.endWithNewline": true,
  "html.format.indentInnerHtml": true,
  "files.autoSave": "afterDelay",
  "editor.autoIndent": false,
  "workbench.colorTheme": "Default High Contrast",
  "workbench.editor.labelFormat": "short",
  "window.zoomLevel": 0,
  "editor.fontSize": 15,
  "git.path": "‪C:/Program Files (x86)/Git/cmd/git.exe",
  "editor.formatOnSave": true,
  "editor.formatOnType": true,
  "eslint.autoFixOnSave": true,
  "prettier.eslintIntegration": true,
  "javascript.format.insertSpaceBeforeFunctionParenthesis": true,
  "typescript.format.insertSpaceBeforeFunctionParenthesis": true,
  "vetur.format.defaultFormatter.js": "vscode-typescript",
  "prettier.singleQuote": true,
  "vetur.format.defaultFormatter.html": "js-beautify-html"
}
```
