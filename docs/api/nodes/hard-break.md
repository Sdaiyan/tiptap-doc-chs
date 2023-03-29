# HardBreak
[![版本](https://img.shields.io/npm/v/@tiptap/extension-hard-break.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-hard-break)
[![下载量](https://img.shields.io/npm/dm/@tiptap/extension-hard-break.svg)](https://npmcharts.com/compare/@tiptap/extension-hard-break?minimal=true)

HardBreak 扩展支持使用`<br>`HTML 标签来强制换行。

## 安装
```bash
npm install @tiptap/extension-hard-break
```

## 参数

### HTMLAttributes
自定义属性将在渲染 HTML 标签时添加。

```js
HardBreak.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

### keepMarks
决定是否在换行后保留标记。基于标记的 `keepOnSplit` 选项。

默认：`true`

```js
HardBreak.configure({
  keepMarks: false,
})
```

## 命令

### setHardBreak()
添加一个硬换行符。

```js
editor.commands.setHardBreak()
```

## 快捷键
| 命令          | Windows/Linux                               | macOS                                    |
| ------------- | ------------------------------------------- | ---------------------------------------- |
| setHardBreak  | `Shift`&nbsp;`Enter`<br>`Control`&nbsp;`Enter` | `Shift`&nbsp;`Enter`<br>`Cmd`&nbsp;`Enter` |

## 源代码
[packages/extension-hard-break/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-hard-break/)

## 使用方法
https://embed.tiptap.dev/preview/Nodes/HardBreak