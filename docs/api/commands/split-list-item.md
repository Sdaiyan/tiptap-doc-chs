# splitListItem
`splitListItem` 方法将一个列表项拆成两个独立的列表项。如果这是一个嵌套列表，则包装该列表项应该被拆分。

## 参数
`typeOrName: string | NodeType`
要拆分成两个独立列表项的节点类型。

## 用法
```js
editor.commands.splitListItem('bullet_list')
```