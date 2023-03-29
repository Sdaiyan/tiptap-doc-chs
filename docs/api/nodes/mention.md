---
description: @marijn @kevin 都可以接收到你的消息了
icon: at-line
---

# Mention（@提醒）
[![Version](https://img.shields.io/npm/v/@tiptap/extension-mention.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-mention)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-mention.svg)](https://npmcharts.com/compare/@tiptap/extension-mention?minimal=true)

Mention Node（节点）十分优秀。它添加了对 `@mentions`（提到）的支持，例如您可以引用用户，*并且* 提供完全控制渲染的能力。 

可以定制的东西真的非常多。您可以使用自定义组件进行渲染。所有示例都使用 `.filter()` 来搜索项，但是您可以自由地向 API 发送异步查询或向您的项目添加更高级的库（例如 [fuse.js](https://fusejs.io/)）。

## 安装
```bash
npm install @tiptap/extension-mention
```

## 依赖关系
为了正确地放置弹出窗口，我们在所有示例中都使用 [tippy.js](https://atomiks.github.io/tippyjs/)。您可以自由选择库，但是如果您愿意使用我们用的库，请安装：

```bash
npm install tippy.js
```

自 2.0.0-beta.193 版本以来，我们将 `@tiptap/suggestion` 标记为对等依赖项。这意味着您需要手动安装它。

```bash
npm install @tiptap/suggestion
```

## 设置

### HTMLAttributes
应添加到渲染的 HTML 标签的自定义 HTML 属性。

```js
Mention.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

### renderLabel
定义提及标签（mention label）应如何呈现。

```js
Mention.configure({
  renderLabel({ options, node }) {
    return `${options.suggestion.char}${node.attrs.label ?? node.attrs.id}`
  }
})
```

### suggestion
[阅读更多](/api/utilities/suggestion)

```js
Mention.configure({
  suggestion: {
    // …
  },
})
```

## 源代码
[packages/extension-mention/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-mention/)

## 用法
https://embed.tiptap.dev/preview/Nodes/Mention