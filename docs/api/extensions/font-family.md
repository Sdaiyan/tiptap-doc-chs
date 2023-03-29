# FontFamily

这个扩展允许你在编辑器中设置字体族。它使用 [`TextStyle`](/api/marks/text-style) 标记，它会渲染出一个 `<span>` 标签。字体族会作为内联样式应用，例如 `<span style="font-family: Arial">`。

## 安装

```bash
npm install @tiptap/extension-text-style @tiptap/extension-font-family
```

这个扩展需要 [`TextStyle`](/api/marks/text-style) 标记。

## 设置

### types

应用字体族属性的标记列表。

默认值：`['textStyle']`

```js
FontFamily.configure({
  types: ['textStyle'],
})
```

## 命令

### setFontFamily()

将给定的字体族作为内联样式应用到文本。

```js
editor.commands.setFontFamily('Inter')
```

### unsetFontFamily()

移除任何字体族。

```js
editor.commands.unsetFontFamily()
```

## 源码

[packages/extension-font-family/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-font-family/)

## 用法

https://embed.tiptap.dev/preview/Extensions/FontFamily