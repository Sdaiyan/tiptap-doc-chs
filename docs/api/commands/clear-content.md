# clearContent

`clearContent` 命令可以删除当前文档。

请注意，编辑器将强制执行已配置的模式，并且文档不会变成 `null`。默认的 [`Document`](https://tiptap.dev/api/nodes/document) 需要至少一个块级节点，它默认为段落。换句话说：即使运行该命令后，文档仍将至少有一个（空）段落。

另请参阅：[setContent](https://tiptap.dev/api/commands/set-content)、[insertContent](https://tiptap.dev/api/commands/insert-content)

## 参数

```
emitUpdate: boolean (false)
```

默认情况下，它不会触发更新事件。传递 `true` 不会阻止触发更新事件。

## 用法

```js
// 删除文档中的所有内容
editor.commands.clearContent()

// 删除所有内容，并触发 `update` 事件
editor.commands.clearContent(true)
```
