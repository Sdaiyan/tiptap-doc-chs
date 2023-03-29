---
title: Vanilla JavaScript WYSIWYG
tableOfContents: true
---

# Vanilla JavaScript

## 介绍
您正在使用普通的 JavaScript 或未在此处列出的框架？不用担心，我们提供您所需的一切。

## 1. 安装依赖
对于以下示例，您将需要 `@tiptap/core`（实际编辑器）、`@tiptap/pm`（ProseMirror 库）和 `@tiptap/starter-kit`。StarterKit 不包含所有扩展，但包含最常见的扩展。

```bash
npm install @tiptap/core @tiptap/pm @tiptap/starter-kit
```

## 2. 添加标记
在要挂载编辑器的位置添加以下 HTML：

```html
<div class="element"></div>
```

## 3. 初始化编辑器
现在一切就绪，让我们设置实际编辑器。在您的 JavaScript 中添加以下代码：

```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'

new Editor({
  element: document.querySelector('.element'),
  extensions: [
    StarterKit,
  ],
  content: '<p>Hello World!</p>',
})
```

在浏览器中打开您的项目以查看 Tiptap 的效果。干得好！