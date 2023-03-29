# Focus

[![版本](https://img.shields.io/npm/v/@tiptap/extension-focus.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-focus)
[![下载量](https://img.shields.io/npm/dm/@tiptap/extension-focus.svg)](https://npmcharts.com/compare/@tiptap/extension-focus?minimal=true)

Focus 扩展会为聚焦的节点添加 CSS 类。默认情况下，它会添加 `.has-focus`，但是可以更改。

请注意，这只是一个类，样式完全由你自己设置。下面的用法示例包含一些 CSS 代码来应用该类。

## 安装

```bash
npm install @tiptap/extension-focus
```

## 配置项

### className

应用于聚焦元素的类名。

默认值：`'has-focus'`

```js
Focus.configure({
  className: 'focus',
})
```

### mode

将类应用于 `'all'`、`'shallowest'` 或 `'deepest'` 节点。

默认值：`'all'`

```js
Focus.configure({
  mode: 'deepest',
})
```

## 源代码

[packages/extension-focus/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-focus/)

## 用法

https://embed.tiptap.dev/preview/Extensions/Focus