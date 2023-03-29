---
tableOfContents: true
---

# 节点

## 简介

如果你将文档想象成一棵树，那么节点只是树中一种内容类型。节点的例子有段落、标题或者代码块。但节点不一定只是块状的，它们也可以和文本一起被渲染成行内的形式，比如 **@mentions**。

## 支持的节点列表

| Title                                        | StarterKit ([view](/api/extensions/starter-kit)) | Source Code                                                                                  |
| -------------------------------------------- | ------------------------------------------------ | -------------------------------------------------------------------------------------------- |
| [Blockquote](/api/nodes/blockquote)          | Included                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-blockquote/)      |
| [BulletList](/api/nodes/bullet-list)         | Included                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-bullet-list/)     |
| [CodeBlock](/api/nodes/code-block)           | Included                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-code-block/)      |
| [Document](/api/nodes/document)              | Included                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-document/)        |
| [Emoji](/api/nodes/emoji)                    | –                                                | Requires a Tiptap Pro subscription                                                           |
| [HardBreak](/api/nodes/hard-break)           | Included                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-hard-break/)      |
| [Hashtag](/api/nodes/hashtag)                | –                                                |                                                                                              |
| [Heading](/api/nodes/heading)                | Included                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-heading/)         |
| [HorizontalRule](/api/nodes/horizontal-rule) | Included                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-horizontal-rule/) |
| [Image](/api/nodes/image)                    | –                                                | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-image/)           |
| [ListItem](/api/nodes/list-item)             | Included                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-list-item/)       |
| [Mention](/api/nodes/mention)                | Included                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-mention/)         |
| [OrderedList](/api/nodes/ordered-list)       | Included                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-ordered-list/)    |
| [Paragraph](/api/nodes/paragraph)            | Included                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-paragraph/)       |
| [Table](/api/nodes/table)                    | –                                                | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-table/)           |
| [TableRow](/api/nodes/table-row)             | –                                                | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-table-row/)       |
| [TableCell](/api/nodes/table-cell)           | –                                                | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-table-cell/)      |
| [TaskList](/api/nodes/task-list)             | –                                                | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-task-list/)       |
| [TaskItem](/api/nodes/task-item)             | –                                                | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-task-item/)       |
| [Text](/api/nodes/text)                      | Included                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-text/)            |
| [YouTube](/api/nodes/youtube)                | –                                                | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-youtube/)         |

## 创建新的节点

您可以自由地为 Tiptap 创建自己的节点。以下是创建和注册自定义节点所需的样板代码：

```js
import { Node } from '@tiptap/core'

const CustomNode = Node.create({
  // 您的代码在这里
})

const editor = new Editor({
  extensions: [
    // 使用编辑器注册您的自定义节点
    CustomNode,
    // …并不要忘记所有其他扩展
    Document,
    Paragraph,
    Text,
    // …
  ],
})
```

在我们的指南中了解[有关自定义扩展的更多信息](https://tiptap.dev/guide/custom-extensions)。
