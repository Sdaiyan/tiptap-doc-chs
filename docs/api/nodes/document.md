---
description: "每个人都需要，但没有人谈论的：Document 扩展。"
icon: file-line
---

# Document
[![版本](https://img.shields.io/npm/v/@tiptap/extension-document.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-document)
[![下载量](https://img.shields.io/npm/dm/@tiptap/extension-document.svg)](https://npmcharts.com/compare/@tiptap/extension-document?minimal=true)

**`Document` 扩展是必需的**，不管你要用 Tiptap 做什么。它是所谓的“topNode”，一个包含所有其他节点的节点。可以将它视为文档的 `<body>` 标签。

该节点非常小。它定义了节点的名称(`doc`)，被配置为顶级节点 (`topNode: true`)，可以包含多个其他节点(`block+`)。这就是全部内容。但你可以自己看一下：

:::warning 从 1.x → 2.x 有一个重大变化
Tiptap 1 试图将该节点从你视线中隐藏，但它一直在那里。从现在开始，你必须明确导入它（或使用 `StarterKit`）。
:::

## 安装
```bash
npm install @tiptap/extension-document
```

## 源码
[packages/extension-document/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-document/)

## 使用
https://embed.tiptap.dev/preview/Nodes/Document