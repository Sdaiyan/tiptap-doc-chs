---
description: 这是一个无用的扩展，只会添加 <span> 标签（虽然其他扩展需要它）。
icon: palette-line
---

# TextStyle
[![Version](https://img.shields.io/npm/v/@tiptap/extension-text-style.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-text-style)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-text-style.svg)](https://npmcharts.com/compare/@tiptap/extension-text-style?minimal=true)

这个 mark 渲染一个 `<span>` HTML 标签，使您可以添加一系列与样式相关的属性，例如字体、字号或颜色。该扩展默认不添加任何样式属性，但其他扩展可将其用作基础，例如 [`FontFamily`](/api/extensions/font-family) 或 [`Color`](/api/extensions/color)。

## 安装
```bash
npm install @tiptap/extension-text-style
```

## Commands

### removeEmptyTextStyle()
删除没有内联样式的 `<span>` 标签。

```js
editor.command.removeEmptyTextStyle()
```

## 源码
[packages/extension-text-style/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-text-style/)

## 用法
https://embed.tiptap.dev/preview/Marks/TextStyle