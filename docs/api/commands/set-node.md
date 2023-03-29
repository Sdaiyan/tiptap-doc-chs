# setNode
`setNode` 命令会将给定范围替换为给定节点。该范围取决于当前的选择。 **重要提示：** 目前 `setNode` 仅支持文本块节点。

## 参数

`typeOrName：string | NodeType`

将替换范围的节点的类型。可以是字符串或 NodeType。

`attributes？：Record<string，any>`

应该应用于节点的属性。 **这是可选的。**

## 用法
```js
editor.commands.setNode("paragraph", { id: "paragraph-01" })
```