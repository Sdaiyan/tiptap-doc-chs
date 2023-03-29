# insertContentAt

`insertContentAt` 方法会在给定位置或范围内插入一段 HTML 字符串或节点。如果给出范围，新的内容将用新内容替换给定范围内的内容。

## 参数
`position: number | Range`

要插入内容的位置或范围。

`value: Content`

要插入的内容。可以是 HTML 字符串或节点。

`options: Record<string, any>`

* updateSelection：控制插入内容后新焦点位置，是否落在插入的内容之后。
* parseOptions：传递的内容由 ProseMirror 解析。为了挂接解析，你可以传递 `parseOptions`，然后由 [ProseMirror](https://prosemirror.net/docs/ref/#model.ParseOptions) 处理。

## 用法
```js
editor.commands.insertContentAt(12, '<p>Hello world</p>', {
  updateSelection: true,
  parseOptions: {
    preserveWhitespace: 'full',
  }
})
```