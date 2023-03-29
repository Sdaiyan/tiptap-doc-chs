# 协作

[![Version](https://img.shields.io/npm/v/@tiptap/extension-collaboration.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-collaboration)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-collaboration.svg)](https://npmcharts.com/compare/@tiptap/extension-collaboration?minimal=true)

Collaboration 扩展允许你与其他人在同一文档中合作。实现是基于 [Kevin Jahns 的 Y.js](https://github.com/yjs/yjs)。要在项目中集成协作编辑，这是最酷的工具之一。

在协作编辑设置中，历史记录完全不同。如果你撤销了一个更改，你不希望撤销其他用户的更改。为了处理这种行为，该扩展提供了自己的 `undo` 和 `redo` 命令。不要与 Collaboration 扩展一起加载默认的 [`History`](/api/extensions/history) 扩展，以避免冲突。

:::pro Pro 扩展
当你在生产中使用该扩展时，我们请求你对我们的工作进行[赞助](/sponsor)。
:::

## 安装
```bash
npm install @tiptap/extension-collaboration yjs y-websocket y-prosemirror
```

## 设置

### document
一个已初始化的 Y.js 文档。

默认值：`null`

```js
Collaboration.configure({
  document: new Y.Doc(),
})
```

### field
Y.js fragment 名称，可以更改为同步一个 Y.js 文档中的多个 fragment。

默认值：`'default'`

```js
Collaboration.configure({
  document: new Y.Doc(),
  field: 'title',
})
```

### fragment
原始的 Y.js fragment，可以代替 `document` 和 `field` 使用。

默认值：`null`

```js
Collaboration.configure({
  fragment: new Y.Doc().getXmlFragment('body'),
})
```

## 命令
`Collboration` 扩展自带自己的历史记录扩展。如果你正在使用 `StarterKit`，请确保禁用默认扩展。

### undo()
撤销上一次更改。

```js
editor.commands.undo()
```

### redo()
重做上一次更改。

```js
editor.commands.redo()
```

## 快捷键
| 命令   | Windows/Linux            | macOS             |
| ------ | ------------------------ | ----------------- |
| undo() | `Control`&nbsp;`Z`       | `Cmd`&nbsp;`Z`    |
| redo() | `Shift`&nbsp;`Control`&nbsp;`Z`<br>`Control`&nbsp;`Y` | `Shift`&nbsp;`Cmd`&nbsp;`Z`<br>`Cmd`&nbsp;`Y` |

## 源代码
[packages/extension-collaboration/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-collaboration/)

## 用法
:::warning Public
此编辑器的内容与其他用户共享。
:::

https://embed.tiptap.dev/preview/Extensions/Collaboration?hideSource

https://embed.tiptap.dev/preview/Extensions/Collaboration