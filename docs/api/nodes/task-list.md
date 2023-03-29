# 任务列表

该扩展使编辑器支持任务列表。在渲染时，它们会被呈现为 `<ul data-type="taskList">`。这个实现不需要任何框架，仅使用纯 JavaScript 。

在新行的开头输入<code>[ ]&nbsp;</code>或<code>[x]&nbsp;</code>，它将自动转换为任务列表。

## 安装

```bash
npm install @tiptap/extension-task-list @tiptap/extension-task-item
```

此扩展需要 [`TaskItem`](/api/nodes/task-item) 扩展。

## 设置

### HTMLAttributes

应添加到呈现的HTML标签中的自定义HTML属性。

```js
TaskList.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

### itemTypeName

指定列表项目名称。

默认值：`'taskItem'`

```js
TaskList.configure({
  itemTypeName: 'taskItem',
})
```

## 命令

# toggleTaskList()

切换任务列表。

```js
editor.commands.toggleTaskList()
```

## 快捷键

| 命令               | Windows/Linux                   | macOS                       |
| ------------------ | ------------------------------- | --------------------------- |
| toggleTaskList() | `Control`&nbsp;`Shift`&nbsp;`9` | `Cmd`&nbsp;`Shift`&nbsp;`9` |

## 源代码

[packages/extension-task-list/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-task-list/)

## 用法

https://embed.tiptap.dev/preview/Nodes/TaskList