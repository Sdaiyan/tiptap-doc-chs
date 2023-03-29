# TaskItem

[![版本](https://img.shields.io/npm/v/@tiptap/extension-task-item.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-task-item)
[![下载量](https://img.shields.io/npm/dm/@tiptap/extension-task-item.svg)](https://npmcharts.com/compare/@tiptap/extension-task-item?minimal=true)

该扩展渲染任务项列表元素，即设置了 `data-type` 属性为 `taskItem` 的 `<li>` 标签。它还在列表元素中渲染复选框，可以更新 `checked` 属性。

该扩展不需要任何 JavaScript 框架，它基于纯 JavaScript。

## 安装

```bash
npm install @tiptap/extension-task-list @tiptap/extension-task-item
```

该扩展需要 [`TaskList`](/api/nodes/task-list) 节点。

## 设置

### HTMLAttributes

应添加到渲染的 HTML 标签的自定义 HTML 属性。

```js
TaskItem.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

### nested

是否允许任务项在彼此之间嵌套。

```js
TaskItem.configure({
  nested: true,
})
```

### onReadOnlyChecked

在编辑器处于 `readOnly` 模式时，当任务项被选中或取消选中，它的处理程序。
如果没有提供此函数，则在编辑器处于 `readOnly` 时任务项是不可变的。
如果此函数返回 false，则将保存选中状态 (`readOnly`)。

```js
TaskItem.configure({
  onReadOnlyChecked: (node, checked) => {
    // do something
  },
})
```

## 键盘快捷键

| Command         | Windows/Linux      | macOS              |
| --------------- | ------------------ | ------------------ |
| splitListItem() | `Enter`            | `Enter`            |
| sinkListItem()  | `Tab`              | `Tab`              |
| liftListItem()  | `Shift`&nbsp;`Tab` | `Shift`&nbsp;`Tab` |

## 源代码

[packages/extension-task-item/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-task-item/)

## 用法

https://embed.tiptap.dev/preview/Nodes/TaskItem