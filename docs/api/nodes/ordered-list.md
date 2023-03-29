# OrderedList

这个扩展可以让您在编辑器中使用有序列表，它们渲染为 `<ol>` HTML 标签。

在新行的开头输入 `<code>1.&nbsp;</code>`（或任何其他数字加上点），它会神奇地变成有序列表。

## 安装

```bash
npm install @tiptap/extension-ordered-list @tiptap/extension-list-item
```

此扩展需要 [`ListItem`](/api/nodes/list-item) 节点。

## 设置

### HTMLAttributes

应添加到渲染的 HTML 标签的自定义 HTML 属性。

```js
OrderedList.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

### itemTypeName

指定列表项名称。

默认值：`'listItem'`

```js
OrderedList.configure({
  itemTypeName: 'listItem',
})
```

### keepMarks

决定在使用 `inputRule` 或使用按钮切换列表后是否保留来自上一行的标记。

默认值：`false`

```js
OrderedList.configure({
  keepMarks: true,
})
```

### keepAttributes

决定在使用 `inputRule` 或使用按钮切换列表后是否保留来自上一行的属性。

默认值：`false`

```js
OrderedList.configure({
  keepAttributes: true,
})
```

## 命令

### toggleOrderedList()

切换有序列表。

```js
editor.commands.toggleOrderedList()
```

## 快捷键

| 命令             | Windows/Linux                   | macOS                       |
| ----------------- | ------------------------------- | --------------------------- |
| toggleOrderedList | `Control`&nbsp;`Shift`&nbsp;`7` | `Cmd`&nbsp;`Shift`&nbsp;`7` |

## 源代码

[packages/extension-ordered-list/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-ordered-list/)

## 用法

https://embed.tiptap.dev/preview/Nodes/OrderedList