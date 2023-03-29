# Dropcursor

[![Version](https://img.shields.io/npm/v/@tiptap/extension-dropcursor.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-dropcursor)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-dropcursor.svg)](https://npmcharts.com/compare/@tiptap/extension-dropcursor?minimal=true)

这个扩展加载了 Marijn Haverbeke 的 [ProseMirror Dropcursor 插件](https://github.com/ProseMirror/prosemirror-dropcursor)，当将东西拖到编辑器中时，它会在放置位置显示一个光标。

请注意，Tiptap 是无头的，但是 dropcursor 需要 CSS 来显示。您可以在其中添加自定义 CSS 类，有关颜色和宽度的设置具体见下文。

## 安装

```bash
npm install @tiptap/extension-dropcursor
```

## 配置项

### color

dropcursor 的颜色。

默认值：`'currentColor'`

```js
Dropcursor.configure({
  color: '#ff0000',
})
```

### width

dropcursor 的宽度。

默认值：`1`

```js
Dropcursor.configure({
  width: 2,
})
```

### class

应用于 dropcursor 的一个或多个 CSS 类。

```js
Dropcursor.configure({
  class: 'my-custom-class',
})
```

## 源代码

[packages/extension-dropcursor/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-dropcursor/)

## 用法

https://embed.tiptap.dev/preview/Extensions/Dropcursor