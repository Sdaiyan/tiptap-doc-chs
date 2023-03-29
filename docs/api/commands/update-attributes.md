# updateAttributes
`updateAttributes` 命令将节点或标记的属性设置为新值。未传递属性将不会被更改。

另请参阅：[extendMarkRange](/api/commands/extend-mark-range)

## 参数
`typeOrName: string | NodeType | MarkType`

传递要更新的类型，例如`'heading'`。

`attributes: Record<string, any>`

这需要一个包含需要更新的属性的对象。它不需要所有属性。

## 用法
```js
// 更新节点属性
editor.commands.updateAttributes('heading', { level: 1 })

// 更新标记属性
editor.commands.updateAttributes('highlight', { color: 'pink' })
```