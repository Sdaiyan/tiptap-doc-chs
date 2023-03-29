# 标题

[![版本](https://img.shields.io/npm/v/@tiptap/extension-heading.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-heading)
[![下载量](https://img.shields.io/npm/dm/@tiptap/extension-heading.svg)](https://npmcharts.com/compare/@tiptap/extension-heading?minimal=true)

标题扩展会添加支持不同级别的标题。标题会使用 `<h1>`、`<h2>`、`<h3>`、`<h4>`、`<h5>` 或 `<h6>` HTML 标签进行呈现。默认情况下，六个标题级别（或样式）都是启用的，但是你可以传递一个数组以仅允许几个级别。请查看用法示例以了解如何执行此操作。

在一行的开始处输入 `<code>#&nbsp;</code>`，它会神奇地转换为标题，输入 `<code>##&nbsp;</code>`、`<code>###&nbsp;</code>`、`<code>####&nbsp;</code>`、`<code>#####&nbsp;</code>` 和 `<code>######&nbsp;</code>` 也是同理。

## 安装
```bash
npm install @tiptap/extension-heading
```

## 设置

### HTMLAttributes
应添加到呈现的 HTML 标签的自定义 HTML 属性。

```js
Heading.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

### levels
指定支持哪些标题级别。

默认值：`[1, 2, 3, 4, 5, 6]`

```js
Heading.configure({
  levels: [1, 2],
})
```

## 命令

### setHeading()
创建一个带有指定级别的标题节点。

```js
editor.commands.setHeading({ level: 1 })
```

### toggleHeading()
切换一个带有指定级别的标题节点。

```js
editor.commands.toggleHeading({ level: 1 })
```

## 快捷键
| 命令                       | Windows/Linux                 | macOS                     |
| --------------------------- | ----------------------------- | ------------------------- |
| toggleHeading({ level: 1 }) | `Control`&nbsp;`Alt`&nbsp;`1` | `Cmd`&nbsp;`Alt`&nbsp;`1` |
| toggleHeading({ level: 2 }) | `Control`&nbsp;`Alt`&nbsp;`2` | `Cmd`&nbsp;`Alt`&nbsp;`2` |
| toggleHeading({ level: 3 }) | `Control`&nbsp;`Alt`&nbsp;`3` | `Cmd`&nbsp;`Alt`&nbsp;`3` |
| toggleHeading({ level: 4 }) | `Control`&nbsp;`Alt`&nbsp;`4` | `Cmd`&nbsp;`Alt`&nbsp;`4` |
| toggleHeading({ level: 5 }) | `Control`&nbsp;`Alt`&nbsp;`5` | `Cmd`&nbsp;`Alt`&nbsp;`5` |
| toggleHeading({ level: 6 }) | `Control`&nbsp;`Alt`&nbsp;`6` | `Cmd`&nbsp;`Alt`&nbsp;`6` |

## 源代码
[packages/extension-heading/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-heading/)

## 用法
https://embed.tiptap.dev/preview/Nodes/Heading