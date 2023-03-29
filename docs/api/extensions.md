---
tableOfContents: true
---

# 扩展

## 简介

扩展可以为 Tiptap 添加新的功能，你会经常在这里读到“扩展”这个词。实际上，有一些字面上的扩展，它们不能添加到 schema，但可以添加功能或改变编辑器的行为。

还有一些更强大的扩展，我们称它们为 [nodes](https://tiptap.dev/api/nodes) 和 [marks](https://tiptap.dev/api/marks)，它们可以在编辑器中呈现内容。

## 提供的扩展列表

| 标题                                                         | StarterKit（[查看](https://tiptap.dev/api/extensions/starter-kit)） | 源代码                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [BubbleMenu](https://tiptap.dev/api/extensions/bubble-menu) | –                                                            | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-bubble-menu/) |
| [CharacterCount](https://tiptap.dev/api/extensions/character-count) | –                                                            | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-character-count/) |
| [Collaboration](https://tiptap.dev/api/extensions/collaboration) | –                                                            | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-collaboration/) |
| [CollaborationCursor](https://tiptap.dev/api/extensions/collaboration-cursor) | –                                                            | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-collaboration-cursor/) |
| [Color](https://tiptap.dev/api/extensions/color)        | –                                                            | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-color/) |
| [Dropcursor](https://tiptap.dev/api/extensions/dropcursor) | 包含                                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-dropcursor/) |
| [FloatingMenu](https://tiptap.dev/api/extensions/floating-menu) | –                                                            | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-floating-menu/) |
| [Focus](https://tiptap.dev/api/extensions/focus)        | –                                                            | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-focus/) |
| [FontFamily](https://tiptap.dev/api/extensions/font-family) | –                                                            | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-font-family/) |
| [Gapcursor](https://tiptap.dev/api/extensions/gapcursor) | 包含                                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-gapcursor/) |
| [History](https://tiptap.dev/api/extensions/history)    | 包含                                                         | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-history/) |
| [Placeholder](https://tiptap.dev/api/extensions/placeholder) | –                                                            | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-placeholder/) |
| [StarterKit](https://tiptap.dev/api/extensions/starter-kit) | –                                                            | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/starter-kit/) |
| [TextAlign](https://tiptap.dev/api/extensions/text-align) | –                                                            | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-text-align/) |
| [Typography](https://tiptap.dev/api/extensions/typography) | –                                                            | [GitHub](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-typography/) |
| [UniqueID](https://tiptap.dev/api/extensions/unique-id) | –                                                            | 需要 Tiptap Pro 订阅                                         |

你不必使用它，但我们准备了一个 `@tiptap/starter-kit`，其中包括最常见的扩展。了解更多关于[`StarterKit`](https://tiptap.dev/guide/configuration#default-extensions)的信息。

同时，[Awesome Tiptap 仓库](https://github.com/ueberdosis/awesome-tiptap#community-extensions)中有一个社区扩展的列表。还有一个关于社区扩展的 [讨论主题](https://github.com/ueberdosis/tiptap/discussions/2973)。

## 扩展的工作原理

尽管 Tiptap 尽力隐藏 ProseMirror 的大部分复杂性，但它是建立在其 API 之上的，我们建议您阅读 [ProseMirror 指南](https://prosemirror.net/docs/guide/) 以了解高级用法。这样，您就可以更好地理解底层的工作原理，并熟悉 Tiptap 使用的许多术语和行话。

现有的 [节点](https://tiptap.dev/api/nodes)、[标记](https://tiptap.dev/api/marks) 和 [扩展](https://tiptap.dev/api/extensions) 可以让您了解如何处理自己的扩展。为了方便在文档和源代码之间切换，我们在每个扩展文档页面上都链接到了 GitHub 上的文件。

我们建议您首先从定制现有扩展开始，然后使用获得的知识创建自己的扩展。这就是为什么下面的所有示例都是扩展现有的扩展，但所有示例也将适用于新创建的扩展。

## 创建新的扩展

您可以自由地为 Tiptap 创建自己的扩展。下面是创建和注册自己的扩展所需的样板代码：

```js
import { Extension } from '@tiptap/core'

const CustomExtension = Extension.create({
  // 在这里写入您的代码
})

const editor = new Editor({
  extensions: [
    // 将您的自定义扩展注册到编辑器。
    CustomExtension,
    // ... 不要忘记所有其他扩展。
    Document,
    Paragraph,
    Text,
    // ...
  ],
})
```

您可以通过我们的 CLI 轻松地引导新的扩展。

```bash

npm init tiptap-extension
```

在我们的指南中了解[更多关于自定义扩展的内容](https://tiptap.dev/guide/custom-extensions)。
