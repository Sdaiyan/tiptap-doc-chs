# deleteRange
`deleteRange` 命令会删除给定范围内的所有内容。它需要一个类型为 `Range` 的 `range` 属性。

## 参数
`range: Range`

## 使用方法
```js
editor.commands.deleteRange({ from: 0, to: 12 })
```