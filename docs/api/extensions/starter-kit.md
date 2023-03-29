# StarterKit

[![Version](https://img.shields.io/npm/v/@tiptap/starter-kit.svg?label=version)](https://www.npmjs.com/package/@tiptap/starter-kit)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/starter-kit.svg)](https://npmcharts.com/compare/@tiptap/starter-kit?minimal=true)

`StarterKit` 是一组最受欢迎的 Tiptap 扩展，如果你刚刚开始使用，这个扩展非常适合你。

## 安装

```bash
npm install @tiptap/starter-kit
```

## 包含的扩展

### 节点

* [`Blockquote`](/api/nodes/blockquote)
* [`BulletList`](/api/nodes/bullet-list)
* [`CodeBlock`](/api/nodes/code-block)
* [`Document`](/api/nodes/document)
* [`HardBreak`](/api/nodes/hard-break)
* [`Heading`](/api/nodes/heading)
* [`HorizontalRule`](/api/nodes/horizontal-rule)
* [`ListItem`](/api/nodes/list-item)
* [`OrderedList`](/api/nodes/ordered-list)
* [`Paragraph`](/api/nodes/paragraph)
* [`Text`](/api/nodes/text)

### 标记

* [`Bold`](/api/marks/bold)
* [`Code`](/api/marks/code)
* [`Italic`](/api/marks/italic)
* [`Strike`](/api/marks/strike)

### 扩展

* [`Dropcursor`](/api/extensions/dropcursor)
* [`Gapcursor`](/api/extensions/gapcursor)
* [`History`](/api/extensions/history)

## 源代码

[packages/starter-kit/](https://github.com/ueberdosis/tiptap/blob/main/packages/starter-kit/)

## 用法

将 `StarterKit` 传递给编辑器，一次性加载所有包含的扩展。

```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'

const editor = new Editor({
  content: '<p>Example Text</p>',
  extensions: [
    StarterKit,
  ],
})
```

您可以配置包含的扩展，甚至禁用其中一些，如下所示。

```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'

const editor = new Editor({
  content: '<p>Example Text</p>',
  extensions: [
    StarterKit.configure({
      // 禁用一个包含的扩展
      history: false,

      // 配置一个包含的扩展
      heading: {
        levels: [1, 2],
      },
    }),
  ],
})
```