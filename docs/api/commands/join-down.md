# joinDown（向下合并）
`joinDown` 命令可以将选中的块与它下面的兄弟节点进行合并，或者将最接近选中节点的祖先块与其下方的兄弟节点进行合并（如果选中的是文本）。[更多信息](https://prosemirror.net/docs/ref/#commands.joinDown)

## 使用方法
```js
editor.commands.joinDown()
```