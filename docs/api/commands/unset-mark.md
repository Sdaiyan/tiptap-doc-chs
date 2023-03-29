# unsetMark
`unsetMark`将从当前选择中移除标记。也可以移除当前选择区域内的所有标记。

## 参数
`typeOrName: string | MarkType`

应该被移除的标记类型。

`options?: Record<string, any>`

* `extendEmptyMarkRange?: boolean` - 即使在当前选择区域内也移除标记。默认值为 `false`。

## 用法
```js
// 移除粗体标记
editor.commands.unsetMark('bold')

// 在当前选择区域内移除粗体标记
editor.commands.unsetMark('bold', { extendEmptyMarkRange: true })
```