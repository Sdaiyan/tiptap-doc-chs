# toggleList
`toggleList` 可以切换不同类型的列表。

## 参数
`listTypeOrName: string | NodeType`

用于包装列表的结点的类型。

`itemTypeOrName: string | NodeType`

用于列表项的结点的类型。

`keepMarks?: boolean`

是否保留标记作为列表项。

`attributes?: Record<string, any>`

应用于列表的属性。**这是可选的。**

## 用法
```js
// 使用指定的列表项切换一个带有项目符号的列表
editor.commands.toggleList('bullet_list', 'list_item')

// 使用指定的列表项切换一个带有编号的列表
editor.commands.toggleList('ordered_list', 'list_item')
```