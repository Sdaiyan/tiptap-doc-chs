---
tableOfContents: true
---

# 事件

## 简介

编辑器会触发几种不同的事件，你可以在这些事件中进行操作。首先，我们来看一下所有可用的事件。

## 可用事件列表

### beforeCreate

在视图被创建之前。

### create

编辑器已准备好。

### update

内容已更改。

### selectionUpdate

选择已更改。

### transaction

编辑器状态已更改。

### focus

编辑器已聚焦。

### blur

编辑器不再聚焦。

### destroy

编辑器正在被销毁。

## 注册事件监听器

有三种方法可以注册事件监听器。

### 选项 1：配置

您可以立即在新的编辑器实例上定义事件监听器：

```js
const editor = new Editor({
  onBeforeCreate({ editor }) {
    // 在视图创建之前。
  },
  onCreate({ editor }) {
    // 编辑器已准备好。
  },
  onUpdate({ editor }) {
    // 内容已更改。
  },
  onSelectionUpdate({ editor }) {
    // 选择已更改。
  },
  onTransaction({ editor, transaction }) {
    // 编辑器状态已更改。
  },
  onFocus({ editor, event }) {
    // 编辑器已聚焦。
  },
  onBlur({ editor, event }) {
    // 编辑器不再聚焦。
  },
  onDestroy() {
    // 编辑器正在被销毁。
  },
})
```

### 选项 2：绑定

或者，您可以在正在运行的编辑器实例上注册事件监听器：

#### 绑定事件监听器

```js
editor.on('beforeCreate', ({ editor }) => {
  // 在视图创建之前。
})

editor.on('create', ({ editor }) => {
  // 编辑器已准备好。
})

editor.on('update', ({ editor }) => {
  // 内容已更改。
})

editor.on('selectionUpdate', ({ editor }) => {
  // 选择已更改。
})

editor.on('transaction', ({ editor, transaction }) => {
  // 编辑器状态已更改。
})

editor.on('focus', ({ editor, event }) => {
  // 编辑器已聚焦。
})

editor.on('blur', ({ editor, event }) => {
  // 编辑器不再聚焦。
})

editor.on('destroy', () => {
  // 编辑器正在被销毁。
})
```

#### 解除事件监听器

如果您需要在某个时刻解除这些事件监听器，您应该使用`.on()` 注册您的事件监听器，并使用 `.off()` 解除它们。

```js
const onUpdate = () => {
  // 内容已更改。
}

// 绑定 ...
editor.on('update', onUpdate)

// ...并解除绑定。
editor.off('update', onUpdate)
```

### 选项3：扩展

将事件监听器移动到自定义扩展（或节点、标记）也是可能的。这是它的代码：

```js
import { Extension } from '@tiptap/core'

const CustomExtension = Extension.create({
  onBeforeCreate({ editor }) {
    // 在视图创建之前。
  },
  onCreate({ editor }) {
    // 编辑器已准备就绪。
  },
  onUpdate({ editor }) {
    // 内容已更改。
  },
  onSelectionUpdate({ editor }) {
    // 选择已更改。
  },
  onTransaction({ editor, transaction }) {
    // 编辑器状态已更改。
  },
  onFocus({ editor, event }) {
    // 编辑器已聚焦。
  },
  onBlur({ editor, event }) {
    // 编辑器不再聚焦。
  },
  onDestroy() {
    // 编辑器正在被销毁。
  },
})
```
