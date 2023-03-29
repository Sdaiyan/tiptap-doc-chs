# HorizontalRule

[![Version](https://img.shields.io/npm/v/@tiptap/extension-horizontal-rule.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-horizontal-rule)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-horizontal-rule.svg)](https://npmcharts.com/compare/@tiptap/extension-horizontal-rule?minimal=true)

使用此扩展程序以呈现一个 `<hr>` HTML 标签。如果在编辑器的初始内容中传递了 `<hr>`，它将被相应地呈现。

在新行的开头键入三个破折号 (<code>---</code>) 或三个下划线和一个空格 (<code>___ </code>)，它会神奇地变成一个横线。

## 安装
```bash
npm install @tiptap/extension-horizontal-rule
```

## 设置

### HTMLAttributes
应添加到呈现的 HTML 标签的自定义 HTML 属性。

```js
HorizontalRule.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

## 命令

### setHorizontalRule()
创建一条水平线。

```js
editor.commands.setHorizontalRule()
```

## 源代码
[packages/extension-horizontal-rule/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-horizontal-rule/)

## 用法
https://embed.tiptap.dev/preview/Nodes/HorizontalRule