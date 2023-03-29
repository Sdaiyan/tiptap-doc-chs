# setTextSelection
如果你想到编辑器中的选择，那么你很可能会想到文本选择。使用 `setTextSelection` 命令，可以控制文本选择并将其设置为指定的范围或位置。

另请参阅：[focus](/api/commands/focus)、[setNodeSelection](/api/commands/set-node-selection)、[deleteSelection](/api/commands/delete-selection)、[selectAll](/api/commands/select-all)

## 参数
`position: number | Range`

传递一个数字或范围，例如 `{ from: 5, to: 10 }`。

## 用法
```js
// 将光标设置到指定位置
editor.commands.setTextSelection(10)

// 将文本选择设置为指定范围
editor.commands.setTextSelection({ from: 5, to: 10 })
```