# Markdown 快捷键

https://embed.tiptap.dev/preview/Examples/MarkdownShortcuts

## 概述

Tiptap 可以通过编写特殊的 `keymap` 使它支持 Markdown 快捷键。这意味着你可以在编辑器中使用 Markdown 标记，例如 `#`、`*` 等等，以更加方便快捷地编辑内容。

## 如何使用

你可以参考以下示例代码，它提供了一组常用的 Markdown 快捷键。具体来说，这些快捷键主要包括：

- `Enter` 在新行上加入 `*` 标记（列表项）
- `Tab` 增加缩进
- `Shift` + `Tab` 减少缩进
- `Ctrl` + `B` 加粗选定的文本
- `Ctrl` + `I` 斜体选定的文本
- `Ctrl` + `K` 添加链接

```javascript
import { keymap } from 'prosemirror-keymap'
import { baseKeymap } from 'prosemirror-commands'

const markdownKeymap = keymap({
  'Enter': (state, dispatch) => {
    const node = state.schema.nodes.list_item.create()
    const transaction = state.tr.replaceSelectionWith(node)
    dispatch(transaction)
    return true
  },
  'Tab': (state, dispatch) => {
    const { $from, $to } = state.selection
    const range = $from.blockRange($to)
    if (!range) return false
    const { startIndex } = range
    const indentation = $from.depth - startIndex
    const transaction = state.tr.wrap(range, state.schema.nodes.blockquote.create())
    transaction.setMeta('indentation', indentation + 1)
    dispatch(transaction)
    return true
  },
  'Shift-Tab': (state, dispatch) => {
    const { $from, $to } = state.selection
    const range = $from.blockRange($to)
    if (!range) return false
    const { startIndex } = range
    const indentation = $from.depth - startIndex
    if (indentation === 0) return false
    const transaction = state.tr.unwrap(range)
    transaction.setMeta('indentation', indentation - 1)
    dispatch(transaction)
    return true
  },
  'Mod-b': toggleMark(schema.marks.strong),
  'Mod-i': toggleMark(schema.marks.em),
  'Mod-k': addLink,
})

const editor = new Editor({
  // ...
  extensions: [
    markdownKeymap,
    baseKeymap,
    // ...
  ],
})
```

## 注意事项

请注意，示例代码中使用到了 `schema`、`toggleMark` 和 `addLink` 等等，这些变量需要你自己定义和处理。你可以参考 Tiptap 官方文档中的其他例子，了解更多有关这些变量的信息。同时，如果你发现无法使用某些快捷键，请确认其是否与当前浏览器中其他插件或快捷键有冲突。