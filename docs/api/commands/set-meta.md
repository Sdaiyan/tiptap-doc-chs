# setMeta
在当前事务中存储元数据属性。

## 参数
`key: string`

元数据的名称。您可以随时使用[getMeta](https://prosemirror.net/docs/ref/#state.Transaction.getMeta)来获取它的值。

`value: any`

在您的元数据中存储任何值。

## 用法
```js
// 防止触发更新事件
editor.commands.setMeta('preventUpdate', true)

// 在当前事务中存储任何值
// 您随时可以通过tr.getMeta('foo')获取该值。
editor.commands.setMeta('foo', 'bar')
```