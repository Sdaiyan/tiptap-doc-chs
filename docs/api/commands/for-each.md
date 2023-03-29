# forEach
遍历一个数组中的元素。

## 参数
`items: any[]`

一个包含元素的数组。

`fn: (item: any, props: CommandProps & { index: number }) => boolean`

一个用来处理每个元素的函数。

## 用法
```js
const items = ['foo', 'bar', 'baz']

editor.commands.forEach(items, (item, { commands }) => {
  return commands.insertContent(item)
})
```