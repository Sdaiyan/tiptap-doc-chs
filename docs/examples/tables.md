# 表格

https://embed.tiptap.dev/preview/Examples/Tables

## 简介

Tiptap 提供了一个简单易用的 table 插件，用来创建和编辑表格。

## 安装

```bash
npm install @tiptap/starter-kit
```

```javascript
import StarterKit from '@tiptap/starter-kit'
import Table from '@tiptap/extension-table'
import TableCellMenu from '@tiptap/extension-table-cell-menu'

const editor = new Editor({
  extensions: [
    StarterKit,
    Table.configure({
      resizable: true,
    }).anywhere(),
    TableCellMenu.configure({
      verticalAlign: 'center',
      content: ({ cell }) => {
        const html = `<p>${cell.attrs.label}</p>`

        return {
          dom: {
            getBoundingClientRect: () => cell.dom.getBoundingClientRect(),
          },
          html,
        }
      },
    }).anywhere(),
  ],
})
```

## 使用

### 添加表格

要添加表格，请使用以下命令：

```javascript
editor.commands.table({
  rows: 3,
  cols: 3,
})
```

这将在当前光标位置插入一个具有 3 行，3 列的表格。你可以传递其他选项来自定义表格。

### 编辑表格

单击表格，然后使用提示菜单中的选项编辑表格。你可以添加或删除行和列、改变表格宽度和高度等。

### 移动和复制行列

要移动或复制行或列，请将鼠标悬停在单元格上，点击“行”或“列”图标并将其拖动到所需位置。松开鼠标后，该行或列将移动或复制到该位置。

## 选项

```javascript
Table.configure({
  resizable: false, // 是否允许用户手动调整单元格大小
  cellAttributes: {}, // 单元格属性
  defaultColumnsWidth: 'auto', // 默认列宽度
  columnHeader: null, // 列标题
  rowHeader: null, // 行标题
  handleWidth: '6px', // 调整大小的句柄宽度和高度
}).anywhere()
```

```javascript
TableCellMenu.configure({
  verticalAlign: 'top', // 垂直排列方式
  content: ({ cell, tr }) => {}, // 菜单内容
}).anywhere()
```