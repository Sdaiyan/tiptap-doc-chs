# Color
[![版本](https://img.shields.io/npm/v/@tiptap/extension-color.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-color)
[![下载量](https://img.shields.io/npm/dm/@tiptap/extension-color.svg)](https://npmcharts.com/compare/@tiptap/extension-color?minimal=true)

该扩展使你可以设置编辑器中文本的颜色。它使用[`TextStyle`](/api/marks/text-style)标记，它将一个`<span>`标签渲染出来（仅仅只有这个标签）。然后将应用内联样式，例如`<span style="color: #958DF1">`。

## 安装
```bash
npm install @tiptap/extension-text-style @tiptap/extension-color
```

该扩展需要[`TextStyle`](/api/marks/text-style)标记。

## 设置

### types
颜色属性应该应用到哪些标记的列表。

默认值：`['textStyle']`

```js
Color.configure({
  types: ['textStyle'],
})
```

## 命令

### setColor()
将给定的字体颜色应用为内联样式。

```js
editor.commands.setColor('#ff0000')
```

### unsetColor()
移除任何字体颜色。

```js
editor.commands.unsetColor()
```

## 源代码
[packages/extension-color/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-color/)

## 使用
https://embed.tiptap.dev/preview/Extensions/Color