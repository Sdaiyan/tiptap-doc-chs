# wrapInList
`wrapInList` 将会把当前选择中的节点包装成一个列表。

## 参数
`typeOrName: string | NodeType`

要包装成列表的节点类型。

`attributes?: Record<string, any>`

应用于列表的属性。**可选。**

## 用法
```js
// 将段落包装在无序列表中
editor.commands.wrapInList('paragraph')
```