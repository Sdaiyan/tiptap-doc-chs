---
description: 控制文字的排版，让它们居左或居中或居右或两端对齐。
icon: align-left
---

# TextAlign
[![Version](https://img.shields.io/npm/v/@tiptap/extension-text-align.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-text-align)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-text-align.svg)](https://npmcharts.com/compare/@tiptap/extension-text-align?minimal=true)

这个扩展为指定的节点添加文本对齐属性。此属性用于对齐文本。

:::warning 火狐浏览器的bug
在火狐浏览器中，`text-align:justify` 和 `white-space: pre-wrap` 无法一起使用，[这是已知的问题](https://bugzilla.mozilla.org/show_bug.cgi?id=1253840)。
:::

## 安装
```bash
npm install @tiptap/extension-text-align
```

## 设置

### types
适用于添加了文本对齐属性的节点列表。通常类似于`['heading', 'paragraph']`。

默认值：`[]`

```js
TextAlign.configure({
  types: ['heading', 'paragraph'],
})
```

### alignments
文本对齐属性的可用选项列表。

默认值：`['left', 'center', 'right', 'justify']`

```js
TextAlign.configure({
  alignments: ['left', 'right'],
})
```

### defaultAlignment
默认的文本对齐方式。

默认值：`'left'`

```js
TextAlign.configure({
  defaultAlignment: 'right',
})
```


## 命令

### setTextAlign()
将文本对齐设置为指定的值。

```js
editor.commands.setTextAlign('right')
```

### unsetTextAlign()
删除文本对齐值。

```js
editor.commands.unsetTextAlign()
```

## 快捷键
| 命令                 | Windows/Linux                | macOS                       |
| ----------------------- | ---------------------------- | --------------------------- |
| setTextAlign('left')    | `Ctrl`&nbsp;`Shift`&nbsp;`L` | `Cmd`&nbsp;`Shift`&nbsp;`L` |
| setTextAlign('center')  | `Ctrl`&nbsp;`Shift`&nbsp;`E` | `Cmd`&nbsp;`Shift`&nbsp;`E` |
| setTextAlign('right')   | `Ctrl`&nbsp;`Shift`&nbsp;`R` | `Cmd`&nbsp;`Shift`&nbsp;`R` |
| setTextAlign('justify') | `Ctrl`&nbsp;`Shift`&nbsp;`J` | `Cmd`&nbsp;`Shift`&nbsp;`J` |

## 源代码
[packages/extension-text-align/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-text-align/)

## 用法
https://embed.tiptap.dev/preview/Extensions/TextAlign