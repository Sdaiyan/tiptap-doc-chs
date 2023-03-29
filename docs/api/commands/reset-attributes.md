# resetAttributes
`resetAttributes` 会将某些节点的属性重置为默认属性。

## 参数
`typeOrName: string | Node`

应该被重置的节点。可以是字符串或 Node。

`attributes: string | string[]`

一个字符串或字符串数组，定义应该被重置的属性。

## 用法
```js
// 重置当前选中段落节点的样式和 class 属性
editor.commands.resetAttributes('paragraph', ['style', 'class'])
```