# Tiptap 升级指南

## 介绍
首先，Tiptap v1 不再受支持，也不会再接受任何更新。

是的，将您最喜爱的文本编辑器升级到新的 API 是繁琐的工作，但是我们确保您有足够的理由升级到最新版本。

* 在您的 IDE 中进行自动补全 (感谢 TypeScript)
* 有 100 多页和 100 多个交互式的示例的惊人文档
* 活跃的开发，正在开发新的功能，每周发布新版本
* 大量新的扩展
* 经过良好测试的代码库

对于您来说，新的 API 看起来可能非常熟悉，不过确实有很多变化。为了使您的升级变得更加容易，这里是您需要知道的所有内容:

## 卸载 Tiptap v1
整个包的结构已经改变，我们甚至移动到另一个 npm 命名空间，因此您需要完全删除旧版本，然后升级到 Tiptap 2。

否则，您会遇到一个异常，例如“看起来加载了多个版本的 prosemirror-model”。

```bash
npm uninstall tiptap tiptap-commands tiptap-extensions tiptap-utils
```

## 安装 Tiptap v2

一旦您卸载了 Tiptap 的旧版本，请安装新的 Vue 2 包、ProseMirror 库和起始包。

```bash
npm install @tiptap/vue-2 @tiptap/pm @tiptap/starter-kit
```

## 保持 Tiptap v2 的最新状态
我们不断地发布新的 Tiptap 更新。

不幸的是，对于 npm 来说，没有集成工具可以轻松更新您的依赖项，但是您可以使用 npm-check 包：

```bash
npm install -g npm-check
npm-check -u
```

## 明确注册 Document、Text 和 Paragraph 扩展
Tiptap 1 尝试通过默认设置 `useBuiltInExtensions: true` 隐藏一些必需的扩展。该设置已被删除，您需要导入所有扩展。请务必明确导入至少 [`Document`](/api/nodes/document)、[`Paragraph`](/api/nodes/paragraph) 和 [`Text`](/api/nodes/text) 扩展。

```js
import Document from '@tiptap/extension-document'
import Paragraph from '@tiptap/extension-paragraph'
import Text from '@tiptap/extension-text'

new Editor({
  extensions: [
    Document,
    Paragraph,
    Text,
    // all your other extensions
  ],
})
```

并且我们删除了一些设置: `dropCursor`、`enableDropCursor` 和 `enableGapCursor`。这些现在是单独的插件: [`Dropcursor`](/api/extensions/dropcursor) 和 [`Gapcursor`](/api/extensions/gapcursor)。你可能想把它们都导入，但如果你不想的话，就忽略这个吧。

## 大多数扩展的新名称
我们转换为 lowerCamelCase，因此有很多类型名称发生了变化。如果您将内容存储为 JSON，需要循环遍历并重命名它们。为此我们表示歉意。

| 旧类型 | 新类型 |
| --- | --- |
| ~~`bullet_list`~~ | `bulletList` |
| ~~`code_block`~~ | `codeBlock` |
| ~~`hard_break`~~ | `hardBreak` |
| ~~`horizontal_rule`~~ | `horizontalRule` |
| ~~`list_item`~~ | `listItem` |
| ~~`ordered_list`~~ | `orderedList` |
| ~~`table_cell`~~ | `tableCell` |
| ~~`table_header`~~ | `tableHeader` |
| ~~`table_row`~~ | `tableRow` |
| ~~`todo_list`~~ | `taskList`（新名称！）|
| ~~`todo_item`~~ | `taskItem`（新名称！）|

## 已删除的方法
我们删除了`.state()` 方法。不过不要担心，仍可通过 `editor.state` 使用该方法。

## 新的扩展 API
如果您为项目构建了一些自定义扩展，那么您需要重写它们以适合新的 API。不必担心，您可以保留许多工作。`schema`、`commands`、`keys`、`inputRules` 和 `pasteRules` 与以前一样工作。只是注册它们的方式不同了。

```js
import { Node } from '@tiptap/core'

const CustomExtension = Node.create({
  name: 'custom_extension',
  addOptions() {
    …
  },
  addAttributes() {
    …
  },
  parseHTML() {
    …
  },
  renderHTML({ node, HTMLAttributes }) {
    …
  },
  addCommands() {
    …
  },
  addKeyboardShortcuts() {
    …
  },
  addInputRules() {
    …
  },
  // and more …
})
```

在我们的指南中了解有关[构建自定义扩展的所有精彩细节](/guide/custom-extensions)。

## 重命名的设置和方法
[我们重命名了很多设置和方法](/api/editor)。您可以使用搜索和替换工具进行迁移。下面是已更改的列表:

| 旧名称 | 新名称 |
| --- | --- |
| ~~`autoFocus`~~ | `autofocus` |

## 重命名的命令
所有新的扩展都提供了特定的命令来设置、取消设置和切换样式。因此，`.bold()` 现在是 `.toggleBold()`。此外，我们转换为 lowerCamelCase，以下是一些示例。哦，我们将 `todo_list` 重命名为 `taskList`，对此表示歉意。

| 旧命令 | 新命令 |
| --- | --- |
| `.redo()` | `.redo()`（无变化） |
| `.undo()` | `.undo()`（无变化）|
| ~~`.todo_list()`~~ | `.toggleTaskList()`（新名称！）|
| ~~`.blockquote()`~~ | `.toggleBlockquote()`|
| ~~`.bold()`~~ | `.toggleBold()`|
| ~~`.bullet_list()`~~ | `.toggleBulletList()`|
| ~~`.code()`~~ | `.toggleCode()`|
| ~~`.code_block()`~~ | `.toggleCodeBlock()`|
| ~~`.hard_break()`~~ | `.setHardBreak()` |
| ~~`.heading()`~~ | `.toggleHeading()`|
| ~~`.horizontal_rule()`~~ | `.setHorizontalRule()`|
| ~~`.italic()`~~ | `.toggleItalic()`|| ~~`.link()`~~            | `.toggleLink()`                 |
| ~~`.ordered_list()`~~    | `.toggleOrderedList()`          |
| ~~`.paragraph()`~~       | `.setParagraph()`               |
| ~~`.strike()`~~          | `.toggleStrike()`               |
| ~~`.underline()`~~       | `.toggleUnderline()`            |
| …                        | …                               |

## 菜单栏，气泡菜单和浮动菜单
请查看[创建菜单](/guide/menus)的专门指南来迁移您的菜单。

## 可以链式调用命令
大多数命令现在都可以组合成一个调用。这在大多数情况下要比单独的函数调用短。以下是一个使所选文本粗体的示例：

```js
editor.chain().toggleBold().focus().run()
```

`.chain()` 是启动新链的必要条件， `.run()` 是实际执行中间所有命令所必需的。有关[新 Tiptap 命令](/api/commands)的更多信息，请阅读我们的 API 文档。

## 不再在每个命令中都调用 `.focus()`
我们试图在 Tiptap 1 中为您隐藏 `.focus()` 命令，并在每个命令中执行它。在特定的用例中，这可能会导致问题，例如您想要运行命令，但不想将焦点放在编辑器上。

使用 Tiptap v2，您必须显式调用 `focus()`，并且可能希望在许多地方都这样做。以下是一个示例：

```js
editor.chain().focus().toggleBold().run()
```

## 事件回调参数更少
新的事件回调参数更少。现在应该可以通过 `this.` 获得相同的信息。[在此阅读有关事件的更多信息。](/api/events)

## 协作编辑
协作编辑的参考实现现在使用了 Y.js。这是一个完全不同的东西。您仍然可以使用 Tiptap 1 扩展，但您需要自适应新扩展 API。如果您这样做了，请不要忘记与我们分享，以便我们可以在此处链接至它！

请在我们的指南中了解有关[全新协作编辑](/guide/collaborative-editing)的信息。

## Marks 不再支持节点视图
对于 Marks，节点视图在[ProseMirror 中不受很好的支持](https://discuss.prosemirror.net/t/there-is-a-bug-in-marks-nodeview/2722/2)。这也是 Tiptap 1 的[一个相关问题](https://github.com/ueberdosis/tiptap/issues/613)。这就是为什么我们在 Tiptap 2 中将其删除的原因。

## 成为赞助商
Tiptap 并不是没有社区资助而存在的。如果您爱上了 Tiptap，请不要忘记[成为赞助商](/sponsor)，使维护、开发和支持持续。

作为回报，我们将将您加入我们的团队，邀请您访问私人代码库，为您的问题和拉取请求添加 `sponsor ♥` 标签等。