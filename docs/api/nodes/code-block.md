# CodeBlock

使用 CodeBlock 扩展可以在文档中添加带有围栏的代码块。它会在 `<pre>` 和 `<code>` HTML 标签中包装代码。

输入 <code>&grave;&grave;&grave;&nbsp;</code> （三个反引号和一个空格）或 <code>&Tilde;&Tilde;&Tilde;&nbsp;</code> （三个波浪线和一个空格），就会自动添加代码块。你甚至可以指定语言，试试输入 <code>&grave;&grave;&grave;css&nbsp;</code>，这样就会在 `<code>`-标签中添加 `language-css` 类。

::: warning 没有语法高亮
CodeBlock 扩展不带有样式，也没有内置的语法高亮。如果你需要带有语法高亮的代码块，请尝试使用 [CodeBlockLowlight](/api/nodes/code-block-lowlight) 扩展。
:::

## 安装
```bash
npm install @tiptap/extension-code-block
```

## 配置

### languageClassPrefix
将应用于代码标记的语言类添加前缀。

默认值：`'language-'`

```js
CodeBlock.configure({
  languageClassPrefix: 'language-',
})
```

### exitOnTripleEnter
定义是否要在按下三次回车后退出节点。

默认值：`true`

```js
CodeBlock.configure({
  exitOnTripleEnter: false,
})
```

### exitOnArrowDown
定义是否要在向下箭头后没有节点时退出节点。

默认值：`true`

```js
CodeBlock.configure({
  exitOnArrowDown: false,
})
```

### HTMLAttributes
应该添加到呈现的 HTML 标记的自定义 HTML 属性。

```js
CodeBlock.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
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

## 键盘快捷键
| 命令            | Windows/Linux                 | macOS                     |
| --------------- | ----------------------------- | ------------------------- |
| toggleCodeBlock | `Control`&nbsp;`Alt`&nbsp;`C` | `Cmd`&nbsp;`Alt`&nbsp;`C` |

## 源代码
[packages/extension-code-block/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-code-block/)

## 用法
https://embed.tiptap.dev/preview/Nodes/CodeBlock