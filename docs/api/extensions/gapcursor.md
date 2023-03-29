# Gapcursor

[![版本](https://img.shields.io/npm/v/@tiptap/extension-gapcursor.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-gapcursor)
[![下载量](https://img.shields.io/npm/dm/@tiptap/extension-gapcursor.svg)](https://npmcharts.com/compare/@tiptap/extension-gapcursor?minimal=true)

这个扩展加载了 Marijn Haverbeke 的 [ProseMirror Gapcursor 插件](https://github.com/ProseMirror/prosemirror-gapcursor)，它可以在不允许正常选择的地方为光标添加间隔。例如，文档末尾的表格之后。

需要注意的是，Tiptap 是 Headless 的，但 Gapcursor 需要 CSS 来进行样式呈现。[默认 CSS](https://github.com/ueberdosis/tiptap/tree/main/packages/core/src/style.ts) 通过 Editor 类加载。

## 安装

```bash
npm install @tiptap/extension-gapcursor
```

## 源码

[packages/extension-gapcursor/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-gapcursor/)

## 使用方法

https://embed.tiptap.dev/preview/Extensions/Gapcursor