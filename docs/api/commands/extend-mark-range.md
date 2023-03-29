# extendMarkRange
`extendMarkRange` 命令扩展当前选择以包括当前 mark。如果当前选择没有指定的 mark，则不会发生任何变化。

## 参数
`typeOrName: string | MarkType`

标记的名称或类型。

`attributes?: Record<string, any>`

可选，可以指定扩展的 mark 必须包含的属性。

## 用法
```js
// 扩展选择到链接标记
editor.commands.extendMarkRange('link')

// 扩展带有特定属性的链接标记
editor.commands.extendMarkRange('link', { href: 'https://google.com' })

// 扩展链接标记并更新属性
editor
  .chain()
  .extendMarkRange('link')
  .updateAttributes('link', {
    href: 'https://duckduckgo.com'
  })
  .run()
```