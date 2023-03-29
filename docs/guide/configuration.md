# 配置

## [#](https://tiptap.dev/guide/configuration#introduction)介绍

对于大多数情况来说，只需要指定 Tiptap 应该在哪里呈现（`element`），要启用哪些功能（`extensions`），以及初始化文档内容（`content`）即可。

不过，还有一些可以配置的选项。让我们看一个完全配置好的编辑器示例。

## [#](https://tiptap.dev/guide/configuration#configure-the-editor)配置编辑器

要添加配置，将[带有设置的对象](https://tiptap.dev/api/editor)传递给 `Editor` 类，如下所示：

```javascript
import { Editor } from '@tiptap/core'
import Document from '@tiptap/extension-document'
import Paragraph from '@tiptap/extension-paragraph'
import Text from '@tiptap/extension-text'

new Editor({
  element: document.querySelector('.element'),
  extensions: [
    Document,
    Paragraph,
    Text,
  ],
  content: '<p>Example Text</p>',
  autofocus: true,
  editable: true,
  injectCSS: false,
})
```

这将执行以下操作：

1. 将 Tiptap 绑定到 `.element`，
2. 加载 `Document`、`Paragraph` 和 `Text` 扩展，
3. 设置初始内容，
4. 初始化后将光标放置在编辑器中，
5. 使文本可编辑（但这是默认设置），以及
6. 禁用加载[默认 CSS](https://github.com/ueberdosis/tiptap/tree/main/packages/core/src/style.ts)（无论如何也不是很多）。

## [#](https://tiptap.dev/guide/configuration#nodes-marks-and-extensions)节点、标记和扩展

大多数编辑功能都打包为[节点](https://tiptap.dev/api/nodes)、[标记](https://tiptap.dev/api/marks)或[扩展](https://tiptap.dev/api/extensions)。导入所需内容并将其作为数组传递给编辑器。

以下是仅使用三个扩展的最小设置：

```javascript
import { Editor } from '@tiptap/core'
import Document from '@tiptap/extension-document'
import Paragraph from '@tiptap/extension-paragraph'
import Text from '@tiptap/extension-text'

new Editor({
  element: document.querySelector('.element'),
  extensions: [
    Document,
    Paragraph,
    Text,
  ],
})
```

### 配置扩展

大多数扩展可以进行配置。添加 `.configure()` 并将对象传递给它即可。

以下示例将禁用默认的标题级别 4、5 和 6，并仅允许 1、2 和 3：

```javascript
import { Editor } from '@tiptap/core'
import Document from '@tiptap/extension-document'
import Paragraph from '@tiptap/extension-paragraph'
import Text from '@tiptap/extension-text'
import Heading from '@tiptap/extension-heading'

new Editor({
  element: document.querySelector('.element'),
  extensions: [
    Document,
    Paragraph,
    Text,
    Heading.configure({
      levels: [1, 2, 3],
    }),
  ],
})
```

请查看您使用的扩展的文档，以了解有关其设置的更多信息。

### [#](https://tiptap.dev/guide/configuration#default-extensions)默认扩展

我们将一些最常见的扩展打包到了一个 `StarterKit` 扩展中。以下是如何使用它：

```javascript
import StarterKit from '@tiptap/starter-kit'

new Editor({
  extensions: [
    StarterKit,
  ],
})
```

您甚至可以将所有包含的扩展的配置作为对象传递。只需在配置中添加扩展名前缀：

```javascript
import StarterKit from '@tiptap/starter-kit'

new Editor({
  extensions: StarterKit.configure({
    heading: {
      levels: [1, 2, 3],
    },
  }),
})
```

`StarterKit` 扩展加载了最常见的扩展，但不包含所有可用的扩展。如果您想加载其他扩展或添加自定义扩展，请将它们添加到 `extensions` 数组中：

```javascript
import StarterKit from '@tiptap/starter-kit'
import Strike from '@tiptap/extension-strike'

new Editor({
  extensions: [
    StarterKit,
    Strike,
  ],
})
```

不想从 `StarterKit` 加载特定的扩展？只需将 `false` 传递给配置即可：

```javascript
import StarterKit from '@tiptap/starter-kit'

new Editor({
  extensions: [
    StarterKit.configure({
      history: false,
    }),
  ],
})
```

您可能会在协作编辑示例中看到类似的配置。[`Collaboration`](https://tiptap.dev/api/extensions/collaboration) 自带其自己的 history 扩展。您需要删除或禁用默认的 [`History`](https://tiptap.dev/api/extensions/history) 扩展以避免冲突。

