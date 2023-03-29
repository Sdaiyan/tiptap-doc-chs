# TableHeader

[![版本](https://img.shields.io/npm/v/@tiptap/extension-table-header.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-table-header)
[![下载量](https://img.shields.io/npm/dm/@tiptap/extension-table-header.svg)](https://npmcharts.com/compare/@tiptap/extension-table-header?minimal=true)

表格头是可选的。但是，说实话：有$header看起来更好看，不是吗？如果你不想要header，可以像这样更新[`TableRow`](/api/nodes/table-row)插件的`content`属性：

```js
// 不要表格头的Table rows
TableRow.extend({
  content: 'tableCell*',
})
```

这是默认值，允许表头：

```js
// 含表格头的Table rows（默认）
TableRow.extend({
  content: '(tableCell | tableHeader)*',
})
```

## 安装
```bash
npm install @tiptap/extension-table @tiptap/extension-table-row @tiptap/extension-table-header @tiptap/extension-table-cell
```

此插件需要 [`Table`](/api/nodes/table)、[`TableRow`](/api/nodes/table-row) 和 [`TableCell`](/api/nodes/table-cell) 节点。

## 源码
[packages/extension-table-header/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-table-header/)

## 用法
https://embed.tiptap.dev/preview/Nodes/Table