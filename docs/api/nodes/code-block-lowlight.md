# CodeBlockLowlight
[![Version](https://img.shields.io/npm/v/@tiptap/extension-code-block-lowlight.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-code-block-lowlight)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-code-block-lowlight.svg)](https://npmcharts.com/compare/@tiptap/extension-code-block-lowlight?minimal=true)

使用 CodeBlockLowlight 扩展，你可以在你的文档中添加 fenced code block。它会把代码放在 `<pre>` 和 `<code>` 的 HTML 标签中。

::: warning 依赖语法高亮库
本扩展依赖 [lowlight](https://github.com/wooorm/lowlight) 库来对代码块的内容进行语法高亮。
:::

输入 <code>&grave;&grave;&grave;&nbsp;</code>（三个反引号和一个空格） 或 <code>&Tilde;&Tilde;&Tilde;&nbsp;</code>（三个波浪线和一个空格）即可快速添加代码块。你甚至可以指定语言类型，例如输入 <code>&grave;&grave;&grave;css&nbsp;</code>，即可在 `<code>` 标签中添加 `language-css` 类。

## 安装
```bash
npm install lowlight @tiptap/extension-code-block-lowlight
```

## 配置

### lowlight

你需要为这个扩展提供 `lowlight` 模块。将 `lowlight` 包与扩展解耦，使客户端应用程序可以控制使用哪个版本的 `lowlight`，以及需要加载哪些编程语言包。

```js
import { lowlight } from 'lowlight/lib/core'

CodeBlockLowlight.configure({
  lowlight,
})
```

### HTMLAttributes
应该添加到渲染 HTML 标记的自定义 HTML 属性。

```js
CodeBlockLowlight.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

### languageClassPrefix
向应用于代码标记的语言类添加前缀。

默认值：`'language-'`

```js
CodeBlockLowlight.configure({
  languageClassPrefix: 'language-',
})
```

### defaultLanguage
指定默认语言，而不是使用 lowlight 自动检测语言。

默认值：`null`

```js
CodeBlockLowlight.configure({
  defaultLanguage: 'plaintext',
})
```

## 命令

### setCodeBlock()
将内容包装在代码块中。

```js
editor.commands.setCodeBlock()
```

### toggleCodeBlock()
切换代码块。

```js
editor.commands.toggleCodeBlock()
```

## 快捷键
| 命令           | Windows/Linux                 | macOS                     |
| --------------- | ----------------------------- | ------------------------- |
| toggleCodeBlock | `Control`&nbsp;`Alt`&nbsp;`C` | `Cmd`&nbsp;`Alt`&nbsp;`C` |

## 源代码
[packages/extension-code-block-lowlight/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-code-block-lowlight/)

## 用法
https://embed.tiptap.dev/preview/Nodes/CodeBlockLowlight