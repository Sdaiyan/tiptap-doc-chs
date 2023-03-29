# 文本
[![版本号](https://img.shields.io/npm/v/@tiptap/extension-text.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-text)
[![下载量](https://img.shields.io/npm/dm/@tiptap/extension-text.svg)](https://npmcharts.com/compare/@tiptap/extension-text?minimal=true)

**`Text` 扩展是必需的**，至少如果你想编辑任何类型的文本的话，那是非常可能的。这个扩展有点不同，它甚至不会呈现 HTML。它只是纯文本，仅此而已。

:::warning 从 1.x → 2.x 的破坏性修改
Tiptap 1 尝试隐藏这个节点不让你看到，但它一直存在。现在，你必须显式地从现在开始导入它（或者使用 `StarterKit`）。
:::

## 安装
```bash
npm install @tiptap/extension-text
```

## 源代码
[packages/extension-text/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-text/)

## 用法
https://embed.tiptap.dev/preview/Nodes/Text