# Highlight

[![Version](https://img.shields.io/npm/v/@tiptap/extension-highlight.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-highlight)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-highlight.svg)](https://npmcharts.com/compare/@tiptap/extension-highlight?minimal=true)

使用此扩展程序使用 `<mark>` 实现高亮文本。您只能使用默认的 `<mark>` HTML 标记，默认情况下具有黄色背景色，或者应用不同的颜色。

输入 `==两个等号==` 它会自动转换为<mark>高亮</mark>文本。

## 安装

```bash
npm install @tiptap/extension-highlight
```

## 设置

### HTML Attributes

添加要添加到呈现的 HTML 标记的自定义 HTML 属性。

```js
Highlight.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

### Multicolor

添加对多个颜色的支持。

默认值：`false`

```js
Highlight.configure({
  multicolor: true,
})
```

## 命令

### setHighlight()

将文本标记为高亮。

```js
editor.commands.setHighlight()
editor.commands.setHighlight({ color: '#ffcc00' })
```

### toggleHighlight()

切换文本高亮。

```js
editor.commands.toggleHighlight()
editor.commands.toggleHighlight({ color: '#ffcc00' })
```

### unsetHighlight()

删除高亮。

```js
editor.commands.unsetHighlight()
```

## 键盘快捷键

| 命令             | Windows/Linux                   | macOS                       |
| ----------------- | ------------------------------- | --------------------------- |
| toggleHighlight() | `Control`&nbsp;`Shift`&nbsp;`H` | `Cmd`&nbsp;`Shift`&nbsp;`H` |

## 源代码

[packages/extension-highlight/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-highlight/)

## 使用方法

https://embed.tiptap.dev/preview/Marks/Highlight