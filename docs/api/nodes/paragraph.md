# 段落

[![Version](https://img.shields.io/npm/v/@tiptap/extension-paragraph.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-paragraph)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-paragraph.svg)](https://npmcharts.com/compare/@tiptap/extension-paragraph?minimal=true)

是的，tiptap 的 schema 很严格，如果你没有安装这个扩展程序，你甚至无法在编辑器中使用段落。

:::warning 从 1.x → 2.x 的重大变化
Tiptap 1 试图为你隐藏一些节点，但它们一直都在那里。从现在开始，你必须明确地导入它们（或使用 “StarterKit”）。
:::

## 安装
```bash
npm install @tiptap/extension-paragraph
```

## 配置

### HTMLAttributes
要添加到呈现 HTML 标签的自定义 HTML 属性。

```js
Paragraph.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

## 命令

### setParagraph()
将所有所选节点转换为段落。

```js
editor.commands.setParagraph()
```

## 快捷键

| 命令           | Windows/Linux                 | macOS                     |
| -------------- | ----------------------------- | ------------------------- |
| setParagraph() | `Control`&nbsp;`Alt`&nbsp;`0` | `Cmd`&nbsp;`Alt`&nbsp;`0` |

## 源代码
[packages/extension-paragraph/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-paragraph/)

## 用法
https://embed.tiptap.dev/preview/Nodes/Paragraph