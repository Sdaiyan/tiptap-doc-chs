# Code

[![版本号](https://img.shields.io/npm/v/@tiptap/extension-code.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-code) [![下载数](https://img.shields.io/npm/dm/@tiptap/extension-code.svg)](https://npmcharts.com/compare/@tiptap/extension-code?minimal=true)

Code 扩展允许您在编辑器中使用 `<code>` HTML 标记。如果您粘贴带有 `<code>` 标记的文本，它将被正确呈现。

在输入时，将某些文本用 <code>\`反引号\`</code> 包括起来即可自动转换成 `行内代码`。

## 安装
```bash
npm install @tiptap/extension-code
```

## 设置

### HTMLAttributes
应添加到呈现的 HTML 标记中的自定义 HTML 属性。

```js
Code.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

## 命令

### setCode()
将文本标记为行内代码。

```js
editor.commands.setCode()
```

### toggleCode()
切换行内代码标记。

```js
editor.commands.toggleCode()
```

### unsetCode()
删除行内代码标记。

```js
editor.commands.unsetCode()
```

## 快捷键
| 命令 | Windows/Linux | macOS |
| ------------ | ------------------ | -------------- |
| toggleCode() | `Control`&nbsp;`E` | `Cmd`&nbsp;`E` |

## 源代码
[packages/extension-code/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-code/)

## 用法
https://embed.tiptap.dev/preview/Marks/Code