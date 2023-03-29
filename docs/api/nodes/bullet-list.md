# BulletList
[![Version](https://img.shields.io/npm/v/@tiptap/extension-bullet-list.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-bullet-list)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-bullet-list.svg)](https://npmcharts.com/compare/@tiptap/extension-bullet-list?minimal=true)

这个扩展能够让你在编辑器中使用无序列表，它们会被渲染成 HTML 标签`<ul>`。

在新行的开头输入<code>*&nbsp;</code>、<code>-&nbsp;</code> 或 <code>+&nbsp;</code> ，它会自动转换为无序列表。

## 安装
```bash
npm install @tiptap/extension-bullet-list @tiptap/extension-list-item
```

此扩展需要 [`ListItem`](/api/nodes/list-item) 节点。

## 配置

### HTMLAttributes
应将其添加到渲染的 HTML 标签的自定义 HTML 属性。

```js
BulletList.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

### itemTypeName
指定列表项名称。

默认值：`'listItem'`

```js
BulletList.configure({
  itemTypeName: 'listItem',
})
```

### keepMarks
决定在使用 `inputRule` 或按钮切换列表时是否保留前一个行的标记

默认值：`false`

```js
BulletList.configure({
  keepMarks: true,
})
```

### keepAttributes
决定在使用 `inputRule` 或按钮切换列表时是否保留前一个行的属性

默认值：`false`

```js
BulletList.configure({
  keepAttributes: true,
})
```

## 命令

### toggleBulletList()
切换无序列表。

```js
editor.commands.toggleBulletList()
```

## 快捷键
| 命令             | Windows/Linux                   | macOS                       |
| ---------------- | ------------------------------- | --------------------------- |
| toggleBulletList | `Control`&nbsp;`Shift`&nbsp;`8` | `Cmd`&nbsp;`Shift`&nbsp;`8` |

## 源代码
[packages/extension-bullet-list/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-bullet-list/)

## 用法
https://embed.tiptap.dev/preview/Nodes/BulletList