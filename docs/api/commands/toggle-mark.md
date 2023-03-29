# toggleMark
`toggleMark` 命令可以在当前选择处开关一个特定的 mark 。

## 参数
`typeOrName: string | MarkType`

应该被开关的 mark 的类型。

`attributes?: Record<string, any>`

应该应用于 mark 的属性。**这是可选的。**

`options?: Record<string, any>`
* `extendEmptyMarkRange: boolean` - 即使跨越当前选择，也会移除 mark。默认为 `false`。

## 用法
```js
// 开关粗体 mark
editor.commands.toggleMark('bold')

// 开关具有颜色属性的粗体标记
editor.commands.toggleMark('bold', { color: 'red' })

// 开关具有颜色属性的粗体标记，并跨越当前选择移除 mark
editor.commands.toggleMark('bold', { color: 'red' }, { extendEmptyMarkRange: true })
```