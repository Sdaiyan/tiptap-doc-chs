---
tableOfContents: true
---

# 编辑器

## 简介

这个类是 Tiptap 的中心构建块。它完成了创建一个可用的 [ProseMirror](https://prosemirror.net/) 编辑器的大部分重要工作，比如创建 [`EditorView`](https://prosemirror.net/docs/ref/#view.EditorView)、设置初始的 [`EditorState`](https://prosemirror.net/docs/ref/#state.Editor_State) 等等。

## 方法

编辑器实例提供了一系列公共方法。这些方法是普通函数，可以返回任何内容。它们将帮助你使用编辑器。

不要把方法和 [commands](https://tiptap.dev/api/commands) 搞混。命令用于更改编辑器的状态（内容、选择等），仅返回 `true` 或 `false`。

### can()

检查一个命令或一个命令链是否可以执行，但不会实际执行。它可以非常有帮助地启用/禁用或显示/隐藏按钮。

```js
// 如果可以执行撤销命令，则返回 `true`
editor.can().undo()
```

### chain()

创建一个命令链，一次调用多个命令。

```js
// 一次执行两个命令
editor.chain().toggleBold().focus().run()
```

### destroy()

停止编辑器实例并解除所有事件绑定。

```js
// 再见了，宝贝！
editor.destroy()
```

### getHTML()

以 HTML 的形式返回当前编辑器文档

```js
editor.getHTML()
```

### getJSON()

返回当前编辑器文档的 JSON 格式。

```js
editor.getJSON()
```

### getText()

返回当前编辑器文档的纯文本格式。

| 参数    | 类型                                                         | 描述         |
| ------- | ------------------------------------------------------------ | ------------ |
| options | { blockSeparator?: string, textSerializers?: Record<string, TextSerializer>} | 序列化选项。 |

```js
// 给我纯文本！
editor.getText()
// 在节点之间添加两个换行符
editor.getText({ blockSeparator: "\n\n" })
```

### getAttributes()

获取当前选中节点或标记的属性。

| 参数       | 类型                           | 描述             |
| ---------- | ------------------------------ | ---------------- |
| typeOrName | string \| NodeType \| MarkType | 节点或标记的名称 |

```js
editor.getAttributes('link').href
```

### isActive()

返回当前选中的节点或标记是否处于激活状态。

| 参数       | 类型                | 描述             |
| ---------- | ------------------- | ---------------- |
| name       | string \| null      | 节点或标记的名称 |
| attributes | Record<string, any> | 节点或标记的属性 |

```js
// 检查是否为标题
editor.isActive('heading')
// 检查是否为具有特定属性值的标题
editor.isActive('heading', { level: 2 })
// 检查是否具有特定属性值，不管是哪个节点/标记
editor.isActive({ textAlign: 'justify' })
```

### registerPlugin()

注册一个 ProseMirror 插件。

| 参数           | 类型                                               | 描述                           |
| -------------- | -------------------------------------------------- | ------------------------------ |
| plugin         | Plugin                                             | 一个 ProseMirror 插件          |
| handlePlugins? | (newPlugin: Plugin, plugins: Plugin[]) => Plugin[] | 控制如何将插件合并到现有插件中 |

### setOptions()

更新编辑器选项。

| 参数    | 类型                   | 描述     |
| ------- | ---------------------- | -------- |
| options | Partial<EditorOptions> | 选项列表 |

```js
// 为现有的编辑器实例添加类
editor.setOptions({
  editorProps: {
    attributes: {
      class: 'my-custom-class',
    },
  },
})
```

### setEditable()

更新编辑器的可编辑状态。

| 参数       | 类型    | 描述                                          |
| ---------- | ------- | --------------------------------------------- |
| editable   | boolean | 当用户应该能够在编辑器中写入时为 `true`。     |
| emitUpdate | boolean | 默认为 `true`。确定是否触发 `onUpdate` 事件。 |

```js
// 将编辑器设为只读
editor.setEditable(false)
```

### unregisterPlugin()

注销 ProseMirror 插件。

| 参数            | 类型                | 描述                   |
| --------------- | ------------------- | ---------------------- |
| nameOrPluginKey | string \| PluginKey | 插件的名称或 PluginKey |

## 获取器

### isEditable

返回编辑器是否可编辑或只读。

```js
editor.isEditable
```

### isEmpty

检查是否有内容。

```js
editor.isEmpty
```

## 设置

### element

`element` 属性指定编辑器将绑定到的 HTML 元素。以下代码将使 Tiptap 与具有 `.element` 类的元素集成：

```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'

new Editor({
  element: document.querySelector('.element'),
  extensions: [
    StarterKit,
  ],
})
```

您甚至可以在将其挂载到元素之前初始化编辑器。这在您的 DOM 尚不可用时非常有用。只需省略 `element`，我们会为您创建一个元素。稍后将其附加到容器中，如下所示：

```js
yourContainerElement.append(editor.options.element)
```

### extensions

必须将扩展列表传递给 `extensions` 属性，即使您只想允许段落也是如此。

```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'
import Document from '@tiptap/extension-document'
import Paragraph from '@tiptap/extension-paragraph'
import Text from '@tiptap/extension-text'
import Highlight from '@tiptap/extension-highlight'

new Editor({
  // 使用默认扩展
  extensions: [
    StarterKit,
  ],

  // … 或使用特定扩展
  extensions: [
    Document,
    Paragraph,
    Text,
  ],

  // … 或同时使用
  extensions: [
    StarterKit,
    Highlight,
  ],
})
```

### content

使用 `content` 属性，您可以为编辑器提供初始内容。这可以是 HTML 或 JSON。

```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'

new Editor({
  content: `<p>Example Text</p>`,
  extensions: [
    StarterKit,
  ],
})
```

### editable

`editable` 属性用于决定用户是否可以在编辑器中输入文字。

```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'

new Editor({
  content: `<p>示例文本</p>`,
  extensions: [
    StarterKit,
  ],
  editable: false,
})
```

### autofocus

使用 `autofocus` 属性可以在编辑器初始化时强制光标跳转到指定位置。

| 值        | 描述                           |
| --------- | ------------------------------ |
| `'start'` | 设置光标到文档开头。           |
| `'end'`   | 设置光标到文档结尾。           |
| `'all'`   | 选中整个文档。                 |
| `Number`  | 将光标设置到文档中的特定位置。 |
| `true`    | 启用 autofocus。               |
| `false`   | 禁用 autofocus。               |
| `null`    | 禁用 autofocus。               |

```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'

new Editor({
  extensions: [
    StarterKit,
  ],
  autofocus: false,
})
```

### enableInputRules

默认情况下，Tiptap 启用所有[输入规则](https://tiptap.dev/guide/custom-extensions/#input-rules)。使用 `enableInputRules` 可以控制它。

```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'

new Editor({
  content: `<p>Example Text</p>`,
  extensions: [
    StarterKit,
  ],
  enableInputRules: false,
})
```

或者你可以仅允许特定的输入规则。

```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'
import Link from '@tiptap/extension-link'

new Editor({
  content: `<p>Example Text</p>`,
  extensions: [
    StarterKit,
    Link,
  ],
  // 传入扩展或扩展名称的数组，以允许特定的输入规则
  enableInputRules: [Link, 'horizontalRule'],
})
```

### enablePasteRules

默认情况下，Tiptap 启用所有 [paste rules](https://tiptap.dev/guide/custom-extensions/#paste-rules)。使用 `enablePasteRules` 可以进行控制。

```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'

new Editor({
  content: `<p>Example Text</p>`,
  extensions: [
    StarterKit,
  ],
  enablePasteRules: false,
})
```

或者，您可以只允许特定的 paste rules。

```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'
import Link from '@tiptap/extension-link'

new Editor({
  content: `<p>Example Text</p>`,
  extensions: [
    StarterKit,
    Link,
  ],
  // 传入一个扩展名或扩展名数组，以允许特定的 paste rules
  enablePasteRules: [Link, 'horizontalRule'],
})
```



### injectCSS

默认情况下，Tiptap 会注入[少量的 CSS](https://github.com/ueberdosis/tiptap/tree/main/packages/core/src/style.ts)。使用 `injectCSS` 可以禁用它。

```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'

new Editor({
  extensions: [
    StarterKit,
  ],
  injectCSS: false,
})
```

### injectNonce

当您使用 [Content-Security-Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) 时，可以指定要添加到动态创建的元素中的 `nonce`。下面是一个例子：

```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'

new Editor({
  extensions: [
    StarterKit,
  ],
  injectCSS: true,
  injectNonce: "your-nonce-here"
})
```

### editorProps

对于高级用例，您可以传递 `editorProps`，它将由 [ProseMirror](https://prosemirror.net/docs/ref/#view.EditorProps) 处理。您可以使用它来重写各种编辑器事件或更改编辑器 DOM 元素属性，例如添加一些 Tailwind 类。下面是一个例子：

```js
new Editor({
  // Learn more: https://prosemirror.net/docs/ref/#view.EditorProps
  editorProps: {
    attributes: {
      class: 'prose prose-sm sm:prose lg:prose-lg xl:prose-2xl mx-auto focus:outline-none',
    },
    transformPastedText(text) {
      return text.toUpperCase()
    }
  }
})
```

您可以使用它来钩入事件处理程序并传递-例如-自定义粘贴处理程序。

### parseOptions

传递的内容将被 ProseMirror 解析。要钩入解析，可以传递 `parseOptions`，然后由 [ProseMirror](https://prosemirror.net/docs/ref/#model.ParseOptions) 处理。

```js
new Editor({
  // 了解更多信息：https://prosemirror.net/docs/ref/#model.ParseOptions
  parseOptions: {
    preserveWhitespace: 'full',
  },
})
```
