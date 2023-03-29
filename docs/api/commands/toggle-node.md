# toggleNode
`toggleNode` 方法用于切换节点的类型。

## 参数
`typeOrName: string | NodeType`

需要被切换的节点类型。

`toggleTypeOrName: string | NodeType`

用于切换的节点类型。

`attributes?: Record<string, any>`

应用于节点的属性。**可选的。**

## 使用方法
```js
// 将段落节点切换为标题节点
editor.commands.toggleNode('paragraph', 'heading', { level: 1 })

// 将段落节点切换为图像节点
editor.commands.toggleNode('paragraph', 'image', { src: 'https://example.com/image.png' })
```