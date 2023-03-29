# Table

## Introduction
在文本编辑器中添加表格是一件非常严肃的事情，并且若使用好旧的 HTML 表格一定也不无趣。`Table` 扩展使您可以向编辑器中添加所谓的所谓的 WYSIWYG 编辑器的终极目标。

别忘了添加 `spacer.gif`。（开玩笑，如果您不知道这是什么，请忽略）。

## 安装
```bash
npm install @tiptap/extension-table @tiptap/extension-table-row @tiptap/extension-table-header @tiptap/extension-table-cell
```

此扩展需要 [`TableRow`](/api/nodes/table-row), [`TableHeader`](/api/nodes/table-header) 和 [`TableCell`](/api/nodes/table-cell) 节点。

## 设置

### HTMLAttributes
自定义应添加到呈现的 HTML 标记的 HTML 属性。

```js
Table.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

### 可调整大小（resizable）
默认：`false`

### handleWidth
默认：`5`

### cellMinWidth
默认：`25`

### View
默认：`TableView`

### lastColumnResizable
默认：`true`

### allowTableNodeSelection
默认：`false`

## 命令

### 插入表格（insertTable）
创建一个新表格，指定行数和列数，并带有标题行（如果您这样告诉它）。

```js
editor.commands.insertTable()
editor.commands.insertTable({ rows: 3, cols: 3, withHeaderRow: true })
```

### 在当前列前添加列（addColumnBefore）
在当前列前添加一列。

```js
editor.commands.addColumnBefore()
```

### 在当前列后添加列（addColumnAfter）
在当前列后添加一列。

```js
editor.commands.addColumnAfter()
```

### 删除当前列（deleteColumn）
删除当前列。

```js
editor.commands.deleteColumn()
```

### 在当前行前添加行（addRowBefore）
在当前行前添加一行。

```js
editor.commands.addRowBefore()
```

### 在当前行后添加行（addRowAfter）
在当前行后添加一行。

```js
editor.commands.addRowAfter()
```

### 删除当前行（deleteRow）
删除当前行。

```js
editor.commands.deleteRow()
```

### 删除整个表格（deleteTable）
删除整个表格。

```js
editor.commands.deleteTable()
```

### 合并所有选定的单元格（mergeCells）
将所有选定的单元格合并到一个单元格中。

```js
editor.commands.mergeCells()
```

### 分裂当前单元格（splitCell）
将当前单元格分裂成两个单元格。

```js
editor.commands.splitCell()
```

### 将当前列变为标题列（toggleHeaderColumn）
使当前列成为标题列。

```js
editor.commands.toggleHeaderColumn()
```

### 将当前行变为标题行（toggleHeaderRow）
使当前行成为标题行。

```js
editor.commands.toggleHeaderRow()
```

### 将当前单元格变为标题单元格（toggleHeaderCell）
使当前单元格成为标题单元格。

```js
editor.commands.toggleHeaderCell()
```

### 合并或分裂单元格（mergeOrSplit）
如果选择了多个单元格，则将它们合并。如果选择了单个单元格，则将该单元格分裂为两个单元格。

```js
editor.commands.mergeOrSplit()
```

### 设置单元格属性（setCellAttribute）
设置当前单元格的给定属性。它可以是您在 [`TableCell`](/api/nodes/table-cell) 扩展中定义的任何内容，例如背景颜色。只需确保首先注册 [您的自定义属性](/guide/custom-extensions#attributes)。

```js
editor.commands.setCellAttribute('customAttribute', 'value')
editor.commands.setCellAttribute('backgroundColor', '#000')
```

### 前往下一个单元格（goToNextCell）
前往下一个单元格。

```js
editor.commands.goToNextCell()
```

### 前往上一个单元格（goToPreviousCell）
前往上一个单元格。

```js
editor.commands.goToPreviousCell()
```

### 修复表格（fixTables）
检查文档中的所有表格并在必要时修复它们。

```js
editor.commands.fixTables()
```

## 源代码
[packages/extension-table/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-table/)

## 用法
https://embed.tiptap.dev/preview/Nodes/Table