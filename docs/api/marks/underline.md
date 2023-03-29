# 下划线

[![Version](https://img.shields.io/npm/v/@tiptap/extension-underline.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-underline)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-underline.svg)](https://npmcharts.com/compare/@tiptap/extension-underline?minimal=true)

使用这个扩展来渲染带下划线的文本。如果您传递了 `<u>` 标签或带有行内样式 `text-decoration:underline` 的文本到编辑器的初始内容，它们都会相应地呈现。

请注意，互联网上使用下划线文本通常表示它是可点击的链接。不要用下划线的方式误导您的用户。

::: 警告
当阅读 `Editor` 实例的内容时，扩展将生成相应的 `<u>` HTML 标记。所有标记了下划线的文本，无论以什么方式标记，都将归一化为 `<u>` HTML 标记。
:::

## 安装
```bash
npm install @tiptap/extension-underline
```

## 设置

### HTMLAttributes
应添加到呈现的 HTML 标记的自定义 HTML 属性。

```js
Underline.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

## 命令

### setUnderline()
将文本标记为带下划线。

```js
editor.commands.setUnderline()
```

### toggleUnderline()
切换下划线标记。

```js
editor.commands.toggleUnderline()
```

### unsetUnderline()
移除下划线标记。

```js
editor.commands.unsetUnderline()
```

## 快捷键
| 命令           | Windows/Linux      | macOS          |
| ----------------- | ------------------ | -------------- |
| toggleUnderline() | `Control`&nbsp;`U` | `Cmd`&nbsp;`U` |

## 源代码
[packages/extension-underline/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-underline/)

## 用法
https://embed.tiptap.dev/preview/Marks/Underline