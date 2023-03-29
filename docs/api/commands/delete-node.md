# deleteNode

`deleteNode` 命令用于删除当前选区内的节点。它需要一个 `typeOrName` 参数，可以是一个字符串或 `NodeType`，用于找到需要删除的节点。删除节点后，视图会自动滚动到光标位置。

## 参数

```
typeOrName: string | NodeType
```

## 用法

```js
// 删除一个段落节点
editor.commands.deleteNode('paragraph')

// 或者

// 删除一个自定义节点
editor.commands.deleteNode(MyCustomNode)
```
