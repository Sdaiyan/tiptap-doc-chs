---
tableOfContents: true
---

# 命令

## 简介

编辑器提供了大量的命令，用于编程添加或更改内容或更改选择。如果您想构建自己的编辑器，您肯定想要更多地了解它们。

## 执行命令

所有可用命令都可以通过编辑器实例访问。假设您想在用户单击按钮时使文本加粗。那么它看起来就像这样：

```js
editor.commands.setBold()
```

虽然这很好，确实可以将所选文字加粗，但您可能想要在一次运行中更改多个命令。让我们看看它是如何工作的。

### 链接命令

大多数命令可以组合成一个调用。这比大多数情况下的单独函数调用要短。以下是使所选文本加粗的示例：

```js
editor
  .chain()
  .focus()
  .toggleBold()
  .run()
```

`.chain()` 必须用于启动新的链式命令，`.run()` 用于实际执行中间的所有命令。

在上面的示例中，同时执行了两个不同的命令。当用户单击内容之外的按钮时，编辑器不再处于焦点状态。因此，您可能想在大多数命令中添加一个 `.focus()` 调用。它将焦点带回到编辑器，以便用户可以继续输入。

所有链接命令都会排队等待。它们组合成一个单一的事务。这意味着，内容只更新一次，`update` 事件也只触发一次。

#### 在自定义命令中链接

在链接命令时，事务会被暂停。如果你想在自定义命令中链接命令，你需要使用该事务并在其中添加命令。以下是如何实现：

```js
addCommands() {
  return {
    customCommand: attributes => ({ chain }) => {
      // 不起作用:
      // return editor.chain() …

      // 起作用:
      return chain()
        .insertContent('foo!')
        .insertContent('bar!')
        .run()
    },
  }
}
```

### 内联命令

在某些情况下，在命令中添加一些逻辑很有帮助。这就是为什么你可以在命令中执行命令。我知道，听起来很疯狂，但是让我们看一个例子：

```js
editor
  .chain()
  .focus()
  .command(({ tr }) => {
    // 操作事务
    tr.insertText('嘿，这很酷！')

    return true
  })
  .run()
```

### 命令的模拟运行

有时候，你并不想真正地运行命令，而只是想知道是否可以运行命令，例如在菜单中显示或隐藏按钮。这就是我们添加 `.can()` 方法的原因。这个方法之后的所有内容都会被执行，但不会将更改应用到文档中：

```js
editor
  .can()
  .toggleBold()
```

你也可以与 `.chain()` 一起使用。下面是一个检查是否可以应用所有命令的示例：

```js
editor
  .can()
  .chain()
  .toggleBold()
  .toggleItalic()
  .run()
```

如果可以应用命令，这两个调用都会返回 `true`，否则返回 `false`。

为了使自定义命令也能够工作，不要忘记返回 `true` 或 `false`。

对于一些自己的命令，你可能希望使用原始的 [transaction](https://tiptap.dev/api/introduction)。为了让它们与 `.can()` 一起工作，你应该检查是否应该分发事务。下面是一个简单的 `.insertText()` 命令的示例：

```js
export default (value) => ({ tr, dispatch }) => {
  if (dispatch) {
    tr.insertText(value)
  }

  return true
}
```

如果你只是包装另一个 Tiptap 命令，你不需要检查它，我们会替你检查。

```js
addCommands() {
  return {
    bold: () => ({ commands }) => {
      return commands.toggleMark('bold')
    },
  }
}
```

如果你只是包装一个普通的 ProseMirror 命令，你仍然需要传递 `dispatch`。然后也没有必要检查它：

```js
import { exitCode } from '@tiptap/pm/commands'

export default () => ({ state, dispatch }) => {
  return exitCode(state, dispatch)
}
```

### 尝试命令

如果你想运行一系列命令，但只希望第一个成功的命令被应用，你可以使用 `.first()` 方法来实现。这个方法依次运行一个命令，停在第一个返回 `true` 的命令处。

例如，退格键首先尝试撤销一个输入规则。如果成功，它就停在那里。如果没有应用输入规则，因此无法撤销，则运行下一个命令并删除选择（如果有的话）。下面是一个简化的示例：

```js
editor.first(({ commands }) => [
  () => commands.undoInputRule(),
  () => commands.deleteSelection(),
  // …
])
```

在命令中，你可以这样做：

```js
export default () => ({ commands }) => {
  return commands.first([
    () => commands.undoInputRule(),
    () => commands.deleteSelection(),
    // …
  ])
}
```

## 命令列表

请查看下面列出的所有核心命令。它们应该可以给您一个很好的第一印象，了解哪些操作是可能的。

### 内容

| 命令              | 描述                               | 链接                                                         |
| ----------------- | ---------------------------------- | ------------------------------------------------------------ |
| clearContent()    | 清除整个文档。                     | [更多](https://tiptap.dev/api/commands/clear-content)   |
| insertContent()   | 在当前位置插入节点或 HTML 字符串。 | [更多](https://tiptap.dev/api/commands/insert-content)  |
| insertContentAt() | 在特定位置插入节点或 HTML 字符串。 | [更多](https://tiptap.dev/api/commands/insert-content-at) |
| setContent()      | 用新内容替换整个文档。             | [更多](https://tiptap.dev/api/commands/set-content)     |

### 节点 & 标记

| 命令                  | 描述                                     | 链接                                                         |
| --------------------- | ---------------------------------------- | ------------------------------------------------------------ |
| clearNodes()          | 将节点规范化为简单的段落。               | [更多](https://tiptap.dev/api/commands/clear-nodes)     |
| createParagraphNear() | 在附近创建一个段落。                     | [更多](https://tiptap.dev/api/commands/create-paragraph-near) |
| deleteNode()          | 删除节点。                               | [更多](https://tiptap.dev/api/commands/delete-node)     |
| extendMarkRange()     | 将文本选择扩展到当前标记。               | [更多](https://tiptap.dev/api/commands/extend-mark-range) |
| exitCode()            | 从代码块中退出。                         | [更多](https://tiptap.dev/api/commands/exit-code)       |
| joinBackward()        | 将两个节点向后连接。                     | [更多](https://tiptap.dev/api/commands/join-backward)   |
| joinForward()         | 将两个节点向前连接。                     | [更多](https://tiptap.dev/api/commands/join-forward)    |
| lift()                | 删除现有包装。                           | [更多](https://tiptap.dev/api/commands/lift)            |
| liftEmptyBlock()      | 如果块为空，则提升块。                   | [更多](https://tiptap.dev/api/commands/lift-empty-block) |
| newlineInCode()       | 在代码中添加换行符。                     | [更多](https://tiptap.dev/api/commands/newline-in-code) |
| resetAttributes()     | 将某些节点或标记属性重置为默认值。       | [更多](https://tiptap.dev/api/commands/reset-attributes) |
| setMark()             | 添加具有新属性的标记。                   | [更多](https://tiptap.dev/api/commands/set-mark)        |
| setNode()             | 用节点替换给定的范围。                   | [更多](https://tiptap.dev/api/commands/set-node)        |
| splitBlock()          | 从现有节点中派生一个新节点。             | [更多](https://tiptap.dev/api/commands/split-block)     |
| toggleMark()          | 切换标记的开和关。                       | [更多](https://tiptap.dev/api/commands/toggle-mark)     |
| toggleNode()          | 切换另一个节点的节点。                   | [更多](https://tiptap.dev/api/commands/toggle-node)     |
| toggleWrap()          | 在另一个节点中包装节点，或删除现有包装。 | [更多](https://tiptap.dev/api/commands/toggle-wrap)     |
| undoInputRule()       | 撤消输入规则。                           | [更多](https://tiptap.dev/api/commands/undo-input-rule) |
| unsetAllMarks()       | 删除当前选择中的所有标记。               | [更多](https://tiptap.dev/api/commands/unset-all-marks) |
| unsetMark()           | 在当前选择中删除标记。                   | [更多](https://tiptap.dev/api/commands/unset-mark)      |
| updateAttributes()    | 更新节点或标记的属性。                   | [更多](https://tiptap.dev/api/commands/update-attributes) |

### 列表

| 命令            | 描述                           | 链接                                                         |
| --------------- | ------------------------------ | ------------------------------------------------------------ |
| liftListItem()  | 将列表项提升为包含它的列表。   | [更多](https://tiptap.dev/api/commands/lift-list-item)  |
| sinkListItem()  | 将列表项下移至内部列表中。     | [更多](https://tiptap.dev/api/commands/sink-list-item)  |
| splitListItem() | 将一个列表项拆分成两个列表项。 | [更多](https://tiptap.dev/api/commands/split-list-item) |
| toggleList()    | 在不同的列表类型之间切换。     | [更多](https://tiptap.dev/api/commands/toggle-list)     |
| wrapInList()    | 将节点包装在列表中。           | [更多](https://tiptap.dev/api/commands/wrap-in-list)    |

### 选择

| 命令                 | 描述                       | 链接                                                         |
| -------------------- | -------------------------- | ------------------------------------------------------------ |
| blur()               | 将焦点从编辑器移除。       | [更多](https://tiptap.dev/api/commands/blur)            |
| deleteRange()        | 删除给定范围内的内容。     | [更多](https://tiptap.dev/api/commands/delete-range)    |
| deleteSelection()    | 删除选中的内容（如果有）。 | [更多](https://tiptap.dev/api/commands/delete-selection) |
| enter()              | 触发回车键。               | [更多](https://tiptap.dev/api/commands/enter)           |
| focus()              | 在给定位置聚焦编辑器。     | [更多](https://tiptap.dev/api/commands/focus)           |
| keyboardShortcut()   | 触发一个键盘快捷键。       | [更多](https://tiptap.dev/api/commands/keyboard-shortcut) |
| scrollIntoView()     | 滚动选择内容到视图中。     | [更多](https://tiptap.dev/api/commands/scroll-into-view) |
| selectAll()          | 选择整个文档。             | [更多](https://tiptap.dev/api/commands/select-all)      |
| selectNodeBackward() | 向后选择一个节点。         | [更多](https://tiptap.dev/api/commands/select-node-backward) |
| selectNodeForward()  | 向前选择一个节点。         | [更多](https://tiptap.dev/api/commands/select-node-forward) |
| selectParentNode()   | 选择父节点。               | [更多](https://tiptap.dev/api/commands/select-parent-node) |
| setNodeSelection()   | 创建一个 `NodeSelection`。 | [更多](https://tiptap.dev/api/commands/set-node-selection) |
| setTextSelection()   | 创建一个 `TextSelection`。 | [更多](https://tiptap.dev/api/commands/set-text-selection) |

### 引用文本

TODO

添加一个带有指定文本的块引用，下面添加一个段落，并设置光标到该段落。

```js
// 未经测试，工作正在进行中，可能会更改
this.editor
  .chain()
  .focus()
  .createParagraphNear()
  .insertContent(text)
  .setBlockquote()
  .insertContent('<p></p>')
  .createParagraphNear()
  .unsetBlockquote()
  .createParagraphNear()
  .insertContent('<p></p>')
  .run()
```

添加一个自定义命令来插入一个节点。

```js
addCommands() {
  return {
    insertTimecode: attributes => ({ chain }) => {
      return chain()
        .focus()
        .insertContent({
          type: 'heading',
          attrs: {
            level: 2,
          },
          content: [
            {
              type: 'text',
              text: 'heading',
            },
          ],
        })
        .insertText(' ')
        .run();
    },
  }
},
```

## 自定义命令

所有扩展都可以添加额外的命令（大多数扩展都这样做），查看特定的 [节点文档](https://tiptap.dev/api/nodes)，[标记文档](https://tiptap.dev/api/marks)和[扩展文档](https://tiptap.dev/api/extensions)以了解更多信息。当然，您也可以[添加自定义扩展](https://tiptap.dev/guide/custom-extensions)，其中包括自定义命令。

但是如何编写这些命令？这需要一些学习。

:::pro 噢，这还在进行中 良好的文档需要注重细节、对项目的深入理解和编写时间。

尽管 Tiptap 被全球数千名开发人员使用，但对我们来说，它仍然是一个副业项目。让我们改变这一点，让开源成为我们的全职工作！有近 300 个赞助商，我们已经完成了一半。

加入他们并成为赞助商！让我们有更多的时间投入到开源中，我们会为您填充并更新此页面。

[在 GitHub 上成为赞助商 →](https://github.com/sponsors/ueberdosis)


