# 链接

[![Version](https://img.shields.io/npm/v/@tiptap/extension-link.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-link)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-link.svg)](https://npmcharts.com/compare/@tiptap/extension-link?minimal=true)

链接扩展为编辑器添加对 `<a>` 标签的支持。此扩展也是无界面的，没有实际的界面来添加、修改或删除链接。下面的使用示例使用本机 JavaScript 提示符以展示如何工作。

在实际的应用程序中，您可能会添加更复杂的用户界面。

粘贴的 URL 将自动转换为链接。

## 安装 

```bash
npm install @tiptap/extension-link
```

## 设置

### protocols

您想要识别为链接的其他自定义协议。

默认值：`[]`

```js
Link.configure({
  protocols: ['ftp', 'mailto'],
})
```

默认情况下，[linkify](https://linkify.js.org/docs/) 在协议末尾添加了 `//`，但可以通过传递` optionalSlashes` 选项来更改此行为。

```js
Link.configure({
  protocols: [
    {
      scheme: 'tel',
      optionalSlashes: true
    }
  ]
})
```

### autolink

启用后，您可以在输入时添加链接。

默认值：`true`

```js
Link.configure({
  autolink: false,
})
```

### openOnClick
启用后，单击链接将打开链接。

默认值：`true`

```js
Link.configure({
  openOnClick: false,
})
```

### linkOnPaste

如果粘贴的内容只包含 URL，则将链接添加到当前选择。

默认值：`true`

```js
Link.configure({
  linkOnPaste: false,
})
```

### HTMLAttributes

应添加到呈现的 HTML 标记的自定义 HTML 属性。

```js
Link.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

#### 删除和覆盖现有的 HTML 属性

您可以将 `rel: null` 添加到 HTMLAttributes 中，以删除默认的 `rel="noopener noreferrer nofollow"`。您还可以使用 `rel:“your-value”` 覆盖默认值。

这也可用于将 `target` 从 `_blank` 的默认值更改。

```js
Link.configure({
  HTMLAttributes: {
    // 将 rel 更改为不同的值
    // 允许搜索引擎遵循链接（删除 nofollow）
    rel: 'noopener noreferrer',
    // 完全删除 target，以便链接在当前标签页中打开
    target: null,
  },
})
```

### 验证

验证每个自动链接的函数。如果存在，则将其调用，并将链接 href 作为参数传递。如果返回 `false`，则链接将被删除。

可以用于设置规则，例如排除或包括某些域、tld 等。

```js
// 仅自动链接具有协议的 url
Link.configure({
  validate: href => /^https?:\/\//.test(href),
})
```

## 命令

### setLink()

将选定文本设置为链接。

```js
editor.commands.setLink({ href: 'https://example.com' })
editor.commands.setLink({ href: 'https://example.com', target: '_blank' })
```

### toggleLink()

向选定文本添加或删除链接。

```js
editor.commands.toggleLink({ href: 'https://example.com' })
editor.commands.toggleLink({ href: 'https://example.com', target: '_blank' })
```

### unsetLink()

删除链接。

```js
editor.commands.unsetLink()
```

## 快捷键

:::warning 没有快捷键
此扩展没有绑定特定的快捷键。您可能会在 `Mod-k` 上打开自定义 UI。
:::

## 获取当前值

您是否知道您可以使用 [`getAttributes`](/api/editor#get-attributes) 来查找当前设置了哪些属性，例如哪个的 href ？不要将其与 [command](/api/commands) 混淆（它会更改状态），它只是一种方法。这是它的样子：

```js
this.editor.getAttributes('link').href
```

## 源代码

[packages/extension-link/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-link/)

## 用法：
https://embed.tiptap.dev/preview/Marks/Link