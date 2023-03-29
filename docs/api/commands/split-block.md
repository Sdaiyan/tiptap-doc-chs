# splitBlock
`splitBlock`将在当前[NodeSelection](https://prosemirror.net/docs/ref/#state.NodeSelection)处将当前节点分割成两个节点。如果当前选择不可分割，则命令将被忽略。

## 参数
`options: Record<string, any>`

* `keepMarks: boolean` - 定义是否保留或移除标记。默认为`true`。

## 用法
```js
// 分割当前节点并保留标记
editor.commands.splitBlock()

// 分割当前节点并不保留标记
editor.commands.splitBlock({ keepMarks: false })
```