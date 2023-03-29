# lift
`lift` 命令将给定节点提升到其父节点。 **提升** 意味着，该块将移动到其当前所在块的父级。

## 参数
`typeOrName: String | NodeType`

应该被提升的节点。如果该节点在当前选择中未找到，则忽略该命令。

`attributes: Record<string, any>`

节点应该具有的属性以进行提升。这是 **可选的**。

## 用法
```js
// 提升任何标题
editor.commands.lift('headline')

// 仅提升 h2
editor.commands.lift('headline', { level: 2 })
```