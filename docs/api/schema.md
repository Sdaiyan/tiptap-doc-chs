# Schema

## 简介
与许多其他编辑器不同，Tiptap 基于定义如何构造内容的 [schema](https://prosemirror.net/docs/guide/#schema)。这使您可以定义可能出现在文档中的节点类型、其属性以及可以嵌套的方式。

这个 schema 是非常严格的, 您不能使用任何在 schema 中没有定义的 HTML 元素或属性。

让我举一个例子: 如果您将类似 `This is <strong>important</strong>` 粘贴到 Tiptap 中，但没有处理 `strong` 标签的任何扩展，您将仅看到 `This is important` - 没有加粗的标签。

## schema 长成什么样子
当您只使用提供的扩展时，不必太关心架构。 如果您正在构建自己的扩展，了解 schema 如何工作可能很有帮助。让我们首先看一个类型化的 ProseMirror 编辑器的简单架构示例：

```js
 // 基于 ProseMirror 的 schema
{
  nodes: {
    doc: {
      content: 'block+',
    },
    paragraph: {
      content: 'inline*',
      group: 'block',
      parseDOM: [{ tag: 'p' }],
      toDOM: () => ['p', 0],
    },
    text: {
      group: 'inline',
    },
  },
}
```

我们在这里注册了三个节点。 `doc`、`paragraph` 和 `text`。`doc` 是允许一个或多个块节点为子节点(`content: 'block+'`)的根节点。由于 `paragraph` 在块节点组中(`group: 'block'`)，因此我们的文档只能包含段落。我们的段落允许零个或多个 inline 节点作为子节点 (`content: 'inline*'`)，所以只能包含 `text`。`parseDOM` 定义了从粘贴的 HTML 中解析节点的方式，`toDOM` 定义了它在 DOM 中呈现的方式。

在 Tiptap 中，每个节点、标记和扩展都位于其自己的文件中。这使我们可以将逻辑拆分。在底层，整个 schema 将被合并在一起：

```js 
// Tiptap schema API
import { Node } from '@tiptap/core'

const Document = Node.create({
  name: 'doc',
  topNode: true,
  content: 'block+',
})

const Paragraph = Node.create({
  name: 'paragraph',
  group: 'block',
  content: 'inline*',
  parseHTML() {
    return [
      { tag: 'p' },
    ]
  },
  renderHTML({ HTMLAttributes }) {
    return ['p', HTMLAttributes, 0]
  },
})

const Text = Node.create({
  name: 'text',
  group: 'inline',
})
``` 

## 节点和标记

### 差异
节点就像内容块，例如段落、标题、代码块、引用等等。

标记可以应用于节点的特定部分。这适用于粗体、斜体或删除的文本。[链接](#) 也是标记。

### 节点架构

#### 内容
内容属性定义节点可以拥有的确切内容类型。ProseMirror 在这方面非常严格。这意味着不符合 schema 的内容会被丢弃。它希望作为字符串的名称或组。这里有一些例子：

```js
Node.create({
  // 必须具有一个或多个块
  content: 'block+',

  // 必须具有零个或多个块
  content: 'block*',

  // 允许所有类型的包含 line，text 或 hard breaks
  content: 'inline*',

  // 除了 'text' 不能有其他任何内容
  content: 'text*', 

  //可以包含一个或多个段落，或列表（如果使用列表）
  content: '(paragraph|list?)+',

  // 必须准确地在顶部有一个标题，在下面有一个或多个块
  content: 'heading block+'
})
```

#### 标记
您可以使用模式的 `marks` 设置定义哪些标记允许嵌套在节点中。添加一个或多个标记名称或组，允许所有标记或禁止所有标记，就像这样：

```js
Node.create({
  // 仅允许 'bold' 标记
  marks: 'bold',

  // 仅允许 'bold' 和 'italic' 标记
  marks: 'bold italic',

  // 允许所有标记
  marks: '_',

  // 禁止所有标记
  marks: '',
})
```

#### 群组
将此节点添加到一组扩展中，可以在 schema 的 [content](#content) 属性中引用该组。

```js
Node.create({
  // 添加到 'block' 组中
  group: 'block',

  // 添加到 'inline' 组中
  group: 'inline',

  // 添加到 'block' 和 'list' 组中
  group: 'block list',
})
```

#### 内联
节点也可以作为内联呈现。当设置 `inline: true` 时，节点将与文本一行呈现。这适用于提及。结果更像一个标记，但具有节点的功能。一个区别是生成的 JSON 文档。多个标记一次应用，内联节点将导致嵌套结构。

```js
Node.create({
  // 以行内文本形式呈现节点,例如:
  inline: true,
})
```

对于一些您希望具备标记中不可用的特性的情况，例如节点视图，请尝试内联节点是否有效：

```js
Node.create({
  name: 'customInlineNode',
  group: 'inline',
  inline: true,
  content: 'text*',
})
```

#### Atom
具有 `atom: true` 的节点不可直接编辑，应将其视为单个单位。在编辑器上下文中不太可能使用它，但是这就像是：

```js
Node.create({
  atom: true,
})
```

一个例子是 [`Mention`](/api/nodes/mention) 扩展，它看起来像文本，但更像单个单位。由于这没有可编辑的文本内容，因此在复制此类节点时，它是空的。不过值得一提的是，您可以控制它。这是 [`Mention`](/api/nodes/mention) 扩展的示例：

```js
// 用于将原子节点转换为纯文本
renderText({ node }) {
  return `@${node.attrs.id}`
},
```

#### 可选择的
除了已经可见的文本选区，还有一个不可见的节点选区。如果要使节点可选择，可以像这样进行配置：

```js
Node.create({
  selectable: true,
})
```

#### 可拖动的所有的节点都可以通过如下设置进行配置以便拖动（默认不可拖动）:

```js
Node.create({
  draggable: true,
})
```

#### 代码
用户希望代码的表现方式有所不同。对于包含代码的所有类型的节点，您可以设置 `code: true` 以将其考虑在内。

```js
Node.create({
  code: true,
})
```

#### 空格
控制此节点中的空格解析方式。

```js
Node.create({
  whitespace: 'pre',
})
```

#### 定义
默认情况下，当节点的整个内容被替换时（例如，当粘贴新内容时），节点会被删除。如果节点应保留这些替换操作，则将其配置为 `defining`。

通常，这适用于 [`Blockquote`](/api/nodes/blockquote)、[`CodeBlock`](/api/nodes/code-block)、[`Heading`](/api/nodes/heading) 和 [`ListItem`](/api/nodes/list-item)。

```js
Node.create({
  defining: true,
})
```

#### 隔离
对于需要对常规编辑操作（如回退）进行分隔的节点，例如 TableCell，设置 `isolating: true`。

```js
Node.create({
  isolating: true,
})
```

#### 允许间隙光标
[`Gapcursor`](/api/extensions/gapcursor) 扩展注册了一个新的模式属性，用于控制是否在该节点的任何位置都允许插入光标。

```js
Node.create({
  allowGapCursor: false,
})
```

#### 表格角色
[`Table`](/api/nodes/table) 扩展注册了一个新的模式属性，用于配置节点具有哪种角色。 允许的值为 `table`、`row`、`cell` 和 `header_cell`。

```js
Node.create({
  tableRole: 'cell',
})
```

### 标记模式
#### 包含
如果不希望光标处于其末尾时激活标记，请将 inclusive 设置为 `false`。例如，对于 [`Link`](/api/marks/link) 标记，就是这样配置的：

```js
Mark.create({
  inclusive: false,
})
```

#### 排除
默认情况下，所有节点都可以同时应用。使用 `excludes` 属性可以定义不能与该标记共存的标记。例如，行内代码标记排除任何其他标记（粗体、斜体和所有其他标记）。

```js
Mark.create({
  // 不能与粗体标记共存
  excludes: 'bold'
  // 排除任何其他标记
  excludes: '_',
})
```

#### 可退出
默认情况下，标记将“陷阱”光标，这意味着除了向左移动光标进入没有标记的文本之外，光标无法离开标记。如果设置为 true，则标记将在节点的末尾处可退出。例如，使用代码标记时很方便。

```js
Mark.create({
  // 使此标记可退出，默认为 false
  exitable: true,
})
```

#### 分组
将此标记添加到扩展组中，可以在模式的内容属性中引用该组。

```js
Mark.create({
  // 将此标记添加到“basic”组中
  group: 'basic',
  // 将此标记添加到“basic”和“foobar”组中
  group: 'basic foobar',
})
```

#### 代码
用户希望代码的表现方式有所不同。对于包含代码的所有类型的标记，您可以设置 `code: true` 以将其考虑在内。

```js
Mark.create({
  code: true,
})
```

#### 跨度
默认情况下，标记在呈现为 HTML 时可以跨越多个节点。设置 `spanning: false` 表示标记不能跨越多个节点。

```js
Mark.create({
  spanning: false,
})
```

## 获取底层的 ProseMirror 模式
有几种使用情况需要使用底层模式。如果您使用 Tiptap 协作文本编辑功能或者想手动将内容呈现为 HTML，则需要使用底层模式。

### 选项 1：使用编辑器
如果您需要在客户端上进行此操作并且仍需要编辑器实例，则可以通过编辑器访问：

```js
import { Editor } from '@tiptap/core'
import Document from '@tiptap/extension-document'
import Paragraph from '@tiptap/extension-paragraph'
import Text from '@tiptap/extension-text'

const editor = new Editor({
  extensions: [
    Document,
    Paragraph,
    Text,
    // 在此处添加更多扩展
  ])
})

const schema = editor.schema
```

### 选项 2：不使用编辑器
如果您只想拥有底层模式并且 *不* 初始化实际编辑器，则可以使用 `getSchema` 辅助函数。 它需要一组可用扩展程序，并为您方便地生成 ProseMirror 模式：

```js
import { getSchema } from '@tiptap/core'
import Document from '@tiptap/extension-document'
import Paragraph from '@tiptap/extension-paragraph'
import Text from '@tiptap/extension-text'

const schema = getSchema([
  Document,
  Paragraph,
  Text,
  // 在此处添加更多扩展
])
```