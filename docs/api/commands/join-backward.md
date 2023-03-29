# joinBackward
`joinBackward` 命令可以将当前光标处的两个节点向后连接。如果选择为空并且在文本块的开头，`joinBackward` 将尝试减少该块与其前面块之间的距离。[另请参阅](https://prosemirror.net/docs/ref/#commands.joinBackward)

## 用法
```js
editor.commands.joinBackward()
```