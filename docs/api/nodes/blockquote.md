# 引用

块引用（Blockquote）扩展让你在编辑器中使用 `<blockquote>` HTML 标签。这对于展示引用非常有用，你知道的。

在新的一行最开始处输入 `<code>>&nbsp;</code>`，它会自动转换为块引用。

## 安装

```bash
npm install @tiptap/extension-blockquote
```

## 设置

### HTMLAttributes

自定义 HTML 属性，将添加到渲染的 HTML 标签中。

```js
Blockquote.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

## 命令

### setBlockquote()

把内容包裹在块引用中。

```js
editor.commands.setBlockquote()
```

### toggleBlockquote()

包裹或解除包裹块引用。

```js
editor.commands.toggleBlockquote()
```

### unsetBlockquote()

解除块引用。

```js
editor.commands.unsetBlockquote()
```

## 快捷键

| 命令             | Windows/Linux                  | macOS                      |
| ---------------- | ------------------------------ | -------------------------- |
| 切换块引用       | `Control`&nbsp;`Shift`&nbsp;`B` | `Cmd`&nbsp;`Shift`&nbsp;`B` |

## 源代码

[packages/extension-blockquote/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-blockquote/)

## 用法

https://embed.tiptap.dev/preview/Nodes/Blockquote