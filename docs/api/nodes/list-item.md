# ListItem
[![版本](https://img.shields.io/npm/v/@tiptap/extension-list-item.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-list-item)
[![下载量](https://img.shields.io/npm/dm/@tiptap/extension-list-item.svg)](https://npmcharts.com/compare/@tiptap/extension-list-item?minimal=true)

ListItem 扩展增加对 `<li>` HTML 标签的支持。它用于无序和有序列表，而且不能单独使用。

## 安装
```bash
npm install @tiptap/extension-list-item
```

此扩展需要 [`BulletList`](/api/nodes/bullet-list) 或 [`OrderedList`](/api/nodes/ordered-list) 节点。

## 设置

### HTMLAttributes
应添加到渲染的 HTML 标签中的自定义 HTML 属性。

```js
ListItem.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

## 快捷键

| 命令              | Windows/Linux      | macOS              |
| --------------- | ------------------ | ------------------ |
| splitListItem() | `Enter`            | `Enter`            |
| sinkListItem()  | `Tab`              | `Tab`              |
| liftListItem()  | `Shift`&nbsp;`Tab` | `Shift`&nbsp;`Tab` |

## 源代码
[packages/extension-list-item/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-list-item/)

## 用法
https://embed.tiptap.dev/preview/Nodes/ListItem