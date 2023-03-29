# 自定义扩展

## 简介

Tiptap 的一个优点是它的可扩展性。你不必依赖提供的扩展，可以根据自己的喜好来扩展编辑器。

通过自定义扩展，你可以添加新的内容类型和新的功能，以扩展已有的或从头开始。让我们从几个常见的例子开始，看看如何扩展现有的节点、标记和扩展。

在最后，你将学习如何从头开始，但你需要相同的知识来扩展现有的和创建新的扩展。

## [#](https://tiptap.dev/guide/custom-extensions#扩展现有扩展)扩展现有扩展

每个扩展都有一个`extend()`方法，它接受一个对象，包含您要更改或添加的所有内容。

假设您想更改项目符号列表的键盘快捷键。您应该先查看扩展的源代码，在这种情况下是[ `BulletList` 节点](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-bullet-list/src/bullet-list.ts)。 对于覆盖键盘快捷键的自定义示例，您的代码可能如下所示：

```javascript
// 1. 导入扩展
import BulletList from '@tiptap/extension-bullet-list'

// 2. 覆盖键盘快捷键
const CustomBulletList = BulletList.extend({
  addKeyboardShortcuts() {
    return {
      'Mod-l': () => this.editor.commands.toggleBulletList(),
    }
  },
})

// 3. 将自定义扩展添加到编辑器
new Editor({
  extensions: [
    CustomBulletList(),
    // …
  ],
})
```

同样的方法适用于扩展现有扩展的每个方面，除了名称。 让我们查看您可以通过扩展方法更改的所有内容。 我们在每个示例中关注一个方面，但是您也可以组合所有这些示例，并在一个 `extend()` 调用中更改多个方面。

### [#](https://tiptap.dev/guide/custom-extensions#名称)名称

扩展名在许多地方使用，更改它并不容易。 如果您想更改现有扩展的名称，可以复制整个扩展并在所有出现的位置更改名称。

扩展名也是 JSON 的一部分。 如果您[将内容存储为 JSON](https://tiptap.dev/guide/output#option-1-json)，则还需要在那里更改名称。

### [#](https://tiptap.dev/guide/custom-extensions#priority)优先级

优先级定义了扩展注册的顺序。默认优先级是 `100`，大多数扩展都是这样的。具有更高优先级的扩展将会更早地被加载。

```javascript
import Link from '@tiptap/extension-link'

const CustomLink = Link.extend({
  priority: 1000,
})
```

扩展加载的顺序会影响两件事：

1. #### [#](https://tiptap.dev/guide/custom-extensions#plugin-order)插件顺序

   具有更高优先级的扩展的 ProseMirror 插件将会先运行。

2. #### [#](https://tiptap.dev/guide/custom-extensions#schema-order)模式顺序

   例如，[`Link`](https://tiptap.dev/api/marks/link) 标记具有更高的优先级，这意味着它将被呈现为 `<a href="…"><strong>Example</strong></a>`，而不是 `<strong><a href="…">Example</a></strong>`。

### [#](https://tiptap.dev/guide/custom-extensions#settings)设置

所有设置都可以通过扩展进行配置，但如果您想更改默认设置，例如为其他开发人员提供 Tiptap 上的库，则可以这样做：

```javascript
import Heading from '@tiptap/extension-heading'

const CustomHeading = Heading.extend({
  addOptions() {
    return {
      ...this.parent?.(),
      levels: [1, 2, 3],
    }
  },
})
```

### [#](https://tiptap.dev/guide/custom-extensions#storage)存储

在某些时候，您可能想要在扩展实例中保存一些数据。这些数据是可变的。您可以在扩展内部通过 `this.storage` 访问它。

```javascript
import { Extension } from '@tiptap/core'

const CustomExtension = Extension.create({
  name: 'customExtension',

  addStorage() {
    return {
      awesomeness: 100,
    }
  },

  onUpdate() {
    this.storage.awesomeness += 1
  },
})
```

在扩展之外，您可以通过 `editor.storage` 访问它。请确保每个扩展都有一个唯一的名称。

```javascript
const editor = new Editor({
  extensions: [
    CustomExtension,
  ],
})

const awesomeness = editor.storage.customExtension.awesomeness
```

### [#](https://tiptap.dev/guide/custom-extensions#schema)模式

Tiptap 使用一个严格的模式来配置内容如何结构化、嵌套，以及它的行为和许多其他方面。您可以[更改现有扩展的模式的所有方面](https://tiptap.dev/api/schema)。我们来看一些常见的用例。

默认的 `Blockquote` 扩展可以包装其他节点，例如标题。如果您想在块引用中仅允许段落，请相应地设置 `content` 属性：

```javascript
// 块引用只能包含段落
import Blockquote from '@tiptap/extension-blockquote'

const CustomBlockquote = Blockquote.extend({
  content: 'paragraph*',
})
```

模式甚至允许使您的节点可拖动，这就是 `draggable` 选项的作用。它的默认值为 `false`，但您可以覆盖它。

```javascript
// 可拖动的段落
import Paragraph from '@tiptap/extension-paragraph'

const CustomParagraph = Paragraph.extend({
  draggable: true,
})
```

这只是两个微小的示例，但是[基础的 ProseMirror 模式](https://prosemirror.net/docs/ref/#model.SchemaSpec)非常强大。

### [#](https://tiptap.dev/guide/custom-extensions#attributes)属性

您可以使用属性在内容中存储附加信息。假设您想扩展默认的 `Paragraph` 节点以具有不同的颜色：

```javascript
const CustomParagraph = Paragraph.extend({
  addAttributes() {
    // 返回一个带有属性配置的对象
    return {
      color: {
        default: 'pink',
      },
    },
  },
})

// 结果：
// <p color="pink">Example Text</p>
```

这已经足够告诉 Tiptap 关于新属性，并将 `'pink'` 设置为默认值。所有属性默认情况下都将呈现为 HTML 属性，并在启动时从内容中解析。

让我们继续使用颜色示例，并假设您想添加一个内联样式来实际着色文本。使用 `renderHTML` 函数，您可以返回将在输出中呈现的 HTML 属性。

此示例基于 `color` 的值添加样式 HTML 属性：

```javascript
const CustomParagraph = Paragraph.extend({
  addAttributes() {
    return {
      color: {
        default: null,
        // 使用属性值
        renderHTML: attributes => {
          // ... 并返回一个带有 HTML 属性的对象。
          return {
            style: `color: ${attributes.color}`,
          }
        },
      },
    }
  },
})

// 结果：
// <p style="color: pink">Example Text</p>
```

您还可以控制如何从 HTML 中解析属性。也许您想将颜色存储在名为 `data-color`（而不仅仅是 `color`）的属性中，以下是如何实现：

```javascript
const CustomParagraph = Paragraph.extend({
  addAttributes() {
    return {
      color: {
        default: null,
        // 自定义 HTML 解析（例如，加载初始内容）
        parseHTML: element => element.getAttribute('data-color'),
        // ... 并自定义 HTML 呈现。
        renderHTML: attributes => {
          return {
            'data-color': attributes.color,
            style: `color: ${attributes.color}`,
          }
        },
      },
    }
  },
})

// 结果：
// <p data-color="pink" style="color: pink">Example Text</p>
```

您可以使用 `rendered: false` 完全禁用属性的呈现。

#### [#](https://tiptap.dev/guide/custom-extensions#extend-existing-attributes)扩展现有属性

如果要向扩展中添加属性并保留现有属性，可以通过 `this.parent()` 访问它们。

在某些情况下，它未定义，因此请确保检查该情况，或使用可选链接 `this.parent?.()`：

```javascript
const CustomTableCell = TableCell.extend({
  addAttributes() {
    return {
      ...this.parent?.(),
      myCustomAttribute: {
        // ...
      },
    }
  },
})
```

### 全局属性

属性可以应用于多个扩展。这对于文本对齐、行高、颜色、字体族以及其他样式相关属性非常有用。

查看[`TextAlign`](https://tiptap.dev/api/extensions/text-align)扩展的[完整源代码](https://github.com/ueberdosis/tiptap/tree/main/packages/extension-text-align)以查看更复杂的示例。但是这里是简单的工作原理：

```javascript
import { Extension } from '@tiptap/core'

const TextAlign = Extension.create({
  addGlobalAttributes() {
    return [
      {
        // 扩展以下扩展
        types: [
          'heading',
          'paragraph',
        ],
        // … 使用这些属性
        attributes: {
          textAlign: {
            default: 'left',
            renderHTML: attributes => ({
              style: `text-align: ${attributes.textAlign}`,
            }),
            parseHTML: element => element.style.textAlign || 'left',
          },
        },
      },
    ]
  },
})
```

### 渲染 HTML

使用`renderHTML`函数，可以控制如何将扩展渲染为 HTML。我们向其传递一个属性对象，其中包含所有局部属性、全局属性和已配置的 CSS 类。以下是`Bold`扩展的示例：

```javascript
renderHTML({ HTMLAttributes }) {
  return ['strong', HTMLAttributes, 0]
},
```

数组中的第一个值应该是 HTML 标记的名称。如果第二个元素是一个对象，则被解释为一组属性。之后的任何元素都作为子元素呈现。

数字零（表示空洞）用于指示应将内容插入到哪里。让我们来看看`CodeBlock`扩展的呈现，它具有两个嵌套标记：

```javascript
renderHTML({ HTMLAttributes }) {
  return ['pre', ['code', HTMLAttributes, 0]]
},
```

如果要在那里添加一些特定的属性，请从`@tiptap/core`中导入`mergeAttributes`辅助函数：

```javascript
import { mergeAttributes } from '@tiptap/core'

// ...

renderHTML({ HTMLAttributes }) {
  return ['a', mergeAttributes(HTMLAttributes, { rel: this.options.rel }), 0]
},
```

### [#](https://tiptap.dev/guide/custom-extensions#parse-html)解析 HTML

`parseHTML()` 函数尝试从 HTML 加载编辑器文档。该函数获取作为参数传递的 HTML DOM 元素，并期望返回一个带有属性及其值的对象。以下是来自 [`Bold`](https://tiptap.dev/api/marks/bold) 标记的简化示例：

```javascript
parseHTML() {
  return [
    {
      tag: 'strong',
    },
  ]
},
```

这定义了一个规则，将所有 `<strong>` 标签转换为 `Bold` 标记。但您可以通过以下方式更高级：

```javascript
parseHTML() {
  return [
    // <strong>
    {
      tag: 'strong',
    },
    // <b>
    {
      tag: 'b',
      getAttrs: node => node.style.fontWeight !== 'normal' && null,
    },
    // <span style="font-weight: bold"> 和 <span style="font-weight: 700">
    {
      style: 'font-weight',
      getAttrs: value => /^(bold(er)?|[5-9]\d{2,})$/.test(value as string) && null,
    },
  ]
},
```

这将检查 `<strong>` 和 `<b>` 标签，以及任何将 `font-weight` 设置为粗体的内联样式的 HTML 标记。

如您所见，您可以选择传递 `getAttrs` 回调，以添加更复杂的检查，例如针对特定的 HTML 属性。回调获取传递的 HTML DOM 节点，但在检查 `style` 属性时，则是其值。

您可能会想知道 `&& null` 是做什么用的？[ProseMirror 期望检查成功时返回 `null` 或 `undefined`](https://prosemirror.net/docs/ref/version/0.18.0.html#model.ParseRule.getAttrs)。

[通过 `priority` 来设置规则的优先级](https://prosemirror.net/docs/ref/version/0.18.0.html#model.ParseRule.priority)，以解决与其他扩展程序的冲突，例如，如果您构建了一个自定义扩展程序，该程序查找具有类属性的段落，但您已经使用了默认段落扩展程序。

#### [#](https://tiptap.dev/guide/custom-extensions#using-get-attrs)使用 getAttrs

你可能已经在示例中注意到了 `getAttrs` 函数，它有两个用途：

1. 检查 HTML 属性以决定规则是否匹配（并从 HTML 创建一个 mark 或 node）。当函数返回 `false` 时，它不匹配。
2. 获取 DOM 元素并使用 HTML 属性来相应地设置您的 mark 或 node 属性：

```javascript
parseHTML() {
  return [
    {
      tag: 'span',
      getAttrs: element => {
        // 检查元素是否具有属性
        element.hasAttribute('style')
        // 获取内联样式
        element.style.color
        // 获取特定属性
        element.getAttribute('data-color')
      },
    },
  ]
},
```

您可以返回一个对象，属性作为键，解析值用于设置您的 mark 或 node 属性。我们建议在 `addAttributes()` 中使用 `parseHTML`。这将使您的代码更加简洁。

```javascript
addAttributes() {
  return {
    color: {
      // 根据 `data-color` 属性的值设置颜色属性
      parseHTML: element => element.getAttribute('data-color'),
    }
  }
},
```

在 [ProseMirror 参考文档](https://prosemirror.net/docs/ref/#model.ParseRule) 中阅读有关 `getAttrs` 和所有其他 `ParseRule` 属性的更多信息。

### [#](https://tiptap.dev/guide/custom-extensions#commands)命令

```javascript
import Paragraph from '@tiptap/extension-paragraph'

const CustomParagraph = Paragraph.extend({
  addCommands() {
    return {
      paragraph: () => ({ commands }) => {
        return commands.setNode('paragraph')
      },
    }
  },
})
```

## 在 `addCommands` 中使用 `commands` 参数

如果要在 `addCommands` 中访问其他命令，可以使用传递给它的 `commands` 参数。

### [#](https://tiptap.dev/guide/custom-extensions#keyboard-shortcuts)键盘快捷键

大多数核心扩展都有合理的键盘快捷键默认设置。但是根据您想要构建的内容，您可能希望进行更改。使用 `addKeyboardShortcuts()` 方法，您可以覆盖预定义的快捷键映射：

```javascript
// 更改项目符号列表键盘快捷键
import BulletList from '@tiptap/extension-bullet-list'

const CustomBulletList = BulletList.extend({
  addKeyboardShortcuts() {
    return {
      'Mod-l': () => this.editor.commands.toggleBulletList(),
    }
  },
})
```

### [#](https://tiptap.dev/guide/custom-extensions#input-rules)输入规则

使用输入规则，您可以定义正则表达式以监听用户输入。它们用于 Markdown 快捷方式，或例如使用 [`Typography`](https://tiptap.dev/api/extensions/typography) 扩展将文本转换为像 `©` 这样的字符（还有更多）。使用 `markInputRule` 助手函数进行标记，使用 `nodeInputRule` 进行节点。

默认情况下，两个波浪线之间的文本会被转换为 ~~删除线文本~~。如果您想要仅使用每侧一个波浪线，请按如下所示覆盖输入规则：

```javascript
// 使用 ~单个波浪线~ markdown 快捷方式
import Strike from '@tiptap/extension-strike'
import { markInputRule } from '@tiptap/core'

// 默认：
// const inputRegex = /(?:^|\s)((?:~~)((?:[^~]+))(?:~~))$/

// 新的：
const inputRegex = /(?:^|\s)((?:~)((?:[^~]+))(?:~))$/

const CustomStrike = Strike.extend({
  addInputRules() {
    return [
      markInputRule({
        find: inputRegex,
        type: this.type,
      }),
    ]
  },
})
```

### [#](https://tiptap.dev/guide/custom-extensions#paste-rules)粘贴规则

粘贴规则和输入规则（见上文）类似，但不是监听用户输入，而是应用于粘贴的内容。

正则表达式有一个微小的区别。输入规则通常以 `$` 结尾（表示“断言在行末的位置”），而粘贴规则通常遍历所有内容，并且不包含 `$`。

将上文的示例应用于粘贴规则的示例如下：

```javascript
// 检查粘贴的内容是否符合单波浪线标记
import Strike from '@tiptap/extension-strike'
import { markPasteRule } from '@tiptap/core'

// 默认：
// const pasteRegex = /(?:^|\s)((?:~~)((?:[^~]+))(?:~~))/g

// 新：
const pasteRegex = /(?:^|\s)((?:~)((?:[^~]+))(?:~))/g

const CustomStrike = Strike.extend({
  addPasteRules() {
    return [
      markPasteRule({
        find: pasteRegex,
        type: this.type,
      }),
    ]
  },
})
```

### [#](https://tiptap.dev/guide/custom-extensions#events)事件

您甚至可以将 [事件监听器](https://tiptap.dev/api/events) 移动到一个单独的扩展中。下面是一个监听所有事件的示例：

```javascript
import { Extension } from '@tiptap/core'

const CustomExtension = Extension.create({
  onCreate() {
    // 编辑器已准备好。
  },
  onUpdate() {
    // 内容已更改。
  },
  onSelectionUpdate({ editor }) {
    // 选择已更改。
  },
  onTransaction({ transaction }) {
    // 编辑器状态已更改。
  },
  onFocus({ event }) {
    // 编辑器获取焦点。
  },
  onBlur({ event }) {
    // 编辑器失去焦点。
  },
  onDestroy() {
    // 编辑器正在被销毁。
  },
})
```

### [#](https://tiptap.dev/guide/custom-extensions#whats-available-in-this)这里有什么可用的内容？

这些扩展并不是类，但你在扩展中仍然可以在 `this` 中访问一些重要的东西。

```javascript
// 扩展的名称，例如 'bulletList'
this.name

// 编辑器实例
this.editor

// ProseMirror 类型
this.type

// 包含所有设置的对象
this.options

// 扩展中包含的所有内容
this.parent
```

### [#](https://tiptap.dev/guide/custom-extensions#prosemirror-plugins)ProseMirror 插件（高级）

毕竟，Tiptap 是基于 ProseMirror 构建的，而 ProseMirror 也拥有相当强大的插件 API。要直接访问它，请使用 `addProseMirrorPlugins()`。

#### [#](https://tiptap.dev/guide/custom-extensions#existing-plugins)现有插件

你可以像下面的例子一样，将现有的 ProseMirror 插件包装在 Tiptap 扩展中。

```javascript
import { history } from '@tiptap/pm/history'

const History = Extension.create({
  addProseMirrorPlugins() {
    return [
      history(),
      // …
    ]
  },
})
```

#### [#](https://tiptap.dev/guide/custom-extensions#access-the-prosemirror-api)访问 ProseMirror API

要挂钩事件，例如单击、双击或粘贴内容时，你可以将 [事件处理程序](https://prosemirror.net/docs/ref/#view.EditorProps) 传递给编辑器的 [editorProps](https://tiptap.dev/api/editor#editor-props)。

或者，你可以将它们添加到 Tiptap 扩展中，如下面的示例所示。

```javascript
import { Extension } from '@tiptap/core'
import { Plugin, PluginKey } from '@tiptap/pm/state'

export const EventHandler = Extension.create({
  name: 'eventHandler',

  addProseMirrorPlugins() {
    return [
      new Plugin({
        key: new PluginKey('eventHandler'),
        props: {
          handleClick(view, pos, event) { /* … */ },
          handleDoubleClick(view, pos, event) { /* … */ },
          handlePaste(view, event, slice) { /* … */ },
          // … 还有许多许多。
          // 这里是完整列表：https://prosemirror.net/docs/ref/#view.EditorProps
        },
      }),
    ]
  },
})
```

### [#](https://tiptap.dev/guide/custom-extensions#node-views)节点视图（高级）

对于高级用例，例如需要在节点内执行 JavaScript 来渲染图像周围的复杂界面，您需要了解节点视图。

它们非常强大，但也非常复杂。简而言之，您需要返回一个父级 DOM 元素和一个应在其中呈现内容的 DOM 元素。看下面这个简化的示例：

```javascript
import Image from '@tiptap/extension-image'

const CustomImage = Image.extend({
  addNodeView() {
    return () => {
      const container = document.createElement('div')

      container.addEventListener('click', event => {
        alert('clicked on the container')
      })

      const content = document.createElement('div')
      container.append(content)

      return {
        dom: container,
        contentDOM: content,
      }
    }
  },
})
```

关于节点视图，有很多要学习的内容，所以请前往我们的指南中[专门介绍节点视图的部分](https://tiptap.dev/guide/node-views)获取更多信息。如果您正在寻找一个真实的例子，请查看 [`TaskItem`](https://tiptap.dev/api/nodes/task-item) 节点的源代码。它使用了一个节点视图来渲染复选框。

## [#](https://tiptap.dev/guide/custom-extensions#create-new-extensions)创建新扩展

您可以从头开始构建自己的扩展，而且您知道吗？这与上面描述的扩展现有扩展的扩展语法相同。

### [#](https://tiptap.dev/guide/custom-extensions#create-a-node)创建一个节点

如果您将文档视为一棵树，则 [节点](https://tiptap.dev/api/nodes) 只是该树中的一种内容类型。好的示例包括 [`Paragraph`](https://tiptap.dev/api/nodes/paragraph)、[`Heading`](https://tiptap.dev/api/nodes/heading) 或 [`CodeBlock`](https://tiptap.dev/api/nodes/code-block)。

```javascript
import { Node } from '@tiptap/core'

const CustomNode = Node.create({
  name: 'customNode',

  // Your code goes here.
})
```

节点不一定是块级元素。它们也可以与文本一起内联呈现，例如用于[@mentions](https://tiptap.dev/api/nodes/mention)。

### [#](https://tiptap.dev/guide/custom-extensions#create-a-mark)创建标记

可以将一个或多个标记应用于[节点](https://tiptap.dev/api/nodes)，例如添加内联格式。学习的好例子包括[`Bold`](https://tiptap.dev/api/marks/bold)，[`Italic`](https://tiptap.dev/api/marks/italic)和[`Highlight`](https://tiptap.dev/api/marks/highlight)。

```javascript
import { Mark } from '@tiptap/core'

const CustomMark = Mark.create({
  name: 'customMark',

  // Your code goes here.
})
```

### [#](https://tiptap.dev/guide/custom-extensions#create-an-extension)创建扩展

扩展为Tiptap添加新功能，您会经常在此处阅读扩展这个词，即使是对于节点和标记也是如此。但是也有字面意义上的扩展。这些无法添加到模式中（像标记和节点一样），但可以添加功能或更改编辑器的行为。

学习的好例子可能是[`TextAlign`](https://tiptap.dev/api/extensions/text-align)。

```javascript
import { Extension } from '@tiptap/core'

const CustomExtension = Extension.create({
  name: 'customExtension',

  // Your code goes here.
})
```

## [#](https://tiptap.dev/guide/custom-extensions#creating-and-publishing-standalone-extensions)创建和发布独立扩展

如果您想为Tiptap创建和发布自己的扩展，可以使用我们的CLI工具来引导您的项目。只需运行`npm init tiptap-extension`并按照说明操作。CLI将为您创建一个新的文件夹，其中包含一个在Rollup上运行的预配置项目的构建脚本。

如果您想在本地测试扩展，可以在项目文件夹中运行`npm link`，然后在您的项目（例如一个Vite应用程序）中运行`npm link YOUR_EXTENSION`。

## [#](https://tiptap.dev/guide/custom-extensions#sharing)共享

当一切都运行良好时，不要忘记与社区共享它，可以在我们的[awesome-tiptap](https://github.com/ueberdosis/awesome-tiptap)存储库或[GitHub Issues](https://github.com/ueberdosis/tiptap/issues/819)上分享。