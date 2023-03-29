# toggleWrap
`toggleWrap` 用一个新节点包裹当前节点或者移除包裹的节点。

## 参数
`typeOrName: string | NodeType`

用于包裹节点的节点类型。

`attributes?: Record<string, any>`

应该应用于节点的属性。**此项为可选项。**

## 用法
```js
// 使用标题节点包裹当前选择
editor.commands.toggleWrap('heading', { level: 1 })
```