# 图片
[![Version](https://img.shields.io/npm/v/@tiptap/extension-image.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-image)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-image.svg)](https://npmcharts.com/compare/@tiptap/extension-image?minimal=true)

使用此扩展可以渲染`<img>`HTML标签。默认情况下，这些图片是块级元素。如果您想将图片与文本放在同一行，请将 `inline` 选项设置为 `true`。

:::warning 限制条件
此扩展仅负责图片的渲染。它不会上传图片到您的服务器，这是另一回事。
:::

## 安装
```bash
npm install @tiptap/extension-image
```

## 设置

### inline
内联渲染图片节点，例如在段落标签中：`<p><img src="spacer.gif"></p>`。默认情况下，图像与段落在同一级别上。

这完全取决于您想要的编辑体验类型，但如果您（例如）从 Quill 切换到 Tiptap，则可能会很有用。

默认值: `false`

```js
Image.configure({
  inline: true,
})
```

### allowBase64
允许将图像解析为base64字符串`<img src="data:image/jpg;base64...">`。

默认值: `false`

```js
Image.configure({
  allowBase64: true,
})
```

### HTMLAttributes
应添加到渲染 HTML 标记的自定义 HTML 属性。

```js
Image.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

## 命令

### setImage()
将当前节点设置为图片。

```js
editor.commands.setImage({ src: 'https://example.com/foobar.png' })
editor.commands.setImage({ src: 'https://example.com/foobar.png', alt: 'A boring example image', title: 'An example' })
```

## 源代码
[packages/extension-image/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-image/)

## 用法
https://embed.tiptap.dev/preview/Nodes/Image