# setMark
`setMark` 命令将在当前选择位置添加一个新的 mark。

## 参数

`typeOrName: string | MarkType`

要添加的 mark 的类型。可为字符串或 MarkType。

`attributes: Record<string, any>`

应用于 mark 的属性。 **此为可选项。**

## 用法
```js
editor.commands.setMark("bold", { class: 'bold-tag' })
```