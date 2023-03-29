# 覆写和扩展

Tiptap is built to be easily extendable and customizable. There are multiple ways to overwrite, extend or modify its behavior to fit your needs.

Tiptap 的设计是易于扩展和自定义的。有多种方式来覆写、扩展或修改它的行为，以满足您的需求。

## Overwriting the default extensions

默认地，Tiptap 是使用多个 extensions 来扩展它的核心功能。这些 extensions 有一些默认选项，可以用来快速使用它。如果您需要完全控制一个 extension 的行为，那么您可以对它进行覆写。

```js
import Placeholder from '@tiptap/extension-placeholder'

export default CustomPlaceholder extends Placeholder {
  get defaultOptions() {
    return {
      ...super.defaultOptions,
      placeholder: 'Type your custom placeholder here',
    }
  }
}
```

这是一个您可以用来覆写 `@tiptap/extension-placeholder` 的示例。首先我们需要从这个 extension 中导入它的类 `Placeholder`。接下来，我们定义一个新的类 `CustomPlaceholder` 并在其内部实现一些新逻辑。在 `defaultOptions` 属性中，我们可以继承 `Placeholder` 的默认选项，同时也可以定义我们的新选项。最后，你可以将你的新 extension 传递给 Tiptap。

```js
import { Editor } from '@tiptap/core'
import CustomPlaceholder from './CustomPlaceholder'

const editor = new Editor({
  extensions: [
    CustomPlaceholder,
    // ...
  ],
})
```

## Extending extensions

如果您只需要对一个 extension 进行轻微更改，而不是完全重写它，您也可以通过扩展该 extension 的方式来实现。

```js
import Placeholder from '@tiptap/extension-placeholder'

export default CustomPlaceholder extends Placeholder {
  get defaultOptions() {
    return {
      ...super.defaultOptions,
      placeholder: 'Type your custom placeholder here',
    }
  }
}
```

这个例子与覆写 extension 类似，但是这次我们想对现有的 extension 进行扩展。我们定义一个新的 extension `CustomPlaceholder` 并继承 `Placeholder`。我们同样重写了 `defaultOptions`，同时保持了大部分继承自 `Placeholder` 的其他行为。

## Custom commands

Tiptap 包含许多默认命令。如果您需要扩展这些命令，或者如果您想创建一些自定义的命令，可以尝试自定义命令。

例如，`toggleWrap` 命令是一个默认的命令，用于将选定的文本包装到指定的 HTML 元素中。这是一个重写 `toggleWrap` 命令的例子，它会使用自定义配置输出一个自定义的 HTML 元素：

```js
import { toggleWrap } from '@tiptap/core'

export default function CustomToggleWrap() {
  return toggleWrap('my_custom_element', {
    HTMLAttributes: {
      class: 'my-custom-class',
    },
  })
}
```

## Custom Mark

Tiptap 内置了一些常见的 Mark，但是您也可以轻松地创建自己的 Mark：

```js
import { Mark, Plugin, PluginKey } from '@tiptap/core'

export default class CustomMark extends Mark {
  get name() {
    return 'custom_mark'
  }

  get schema() {
    return {
      attrs: {
        class: {
          default: 'my-custom-mark',
        },
      },
      parseDOM: [
        {
          tag: '[data-custom-mark]',
        },
      ],
      toDOM: (node) => ['span', { 'data-custom-mark': '' }, 0],
    }
  }

  commands({ type }) {
    return () => toggleMark(type)
  }

  get plugins() {
    return [
      new Plugin({
        key: new PluginKey('customMark'),
        props: {
          handleClick: (view, pos, event) => {
            console.log('clicked!', event)
          },
        },
      }),
    ]
  }
}
```

在此示例中，我们创建了一个新的 Mark `CustomMark`，并覆写了它的 `name`，`schema`，`commands` 和 `plugins`。在 schema 中，我们定义了 Mark 的属性、解析和生成，让它适用于我们的需求。在 command 中，我们选择使用内置的 `toggleMark`，但是你也可以使用你自己的逻辑。在插件中，我们添加了一个 `handleClick` 方法，用于处理点击之后的事件。注意：默认情况下，Mark 不支持 Block 节点，这意味着它只能应用于文本节点中的一部分。如需使 Mark 支持 Block 节点，请查看 `/docs/guides/block-marks.md`。

## Custom Node

与创建自定义 Mark 相同，Tiptap 还支持创建自定义节点。以下是一个示例，它会创建一个自定义节点 `CustomNode` 并覆写了它的 `name`，`schema`，`commands` 和 `plugins`。

```js
import { Node, Plugin, PluginKey } from '@tiptap/core'

export default class CustomNode extends Node {
  get name() {
    return 'custom_node'
  }

  get schema() {
    return {
      content: 'inline*',
      group: 'block',
      defining: true,
      draggable: true,
      atom: true,
      attrs: {
        title: {
          default: null,
        },
        id: {
          default: null,
        },
      },
      parseDOM: [
        {
          tag: 'div[data-custom-node]',
          getAttrs: (node) => ({
            title: node.getAttribute('data-title'),
            id: node.getAttribute('data-id'),
          }),
        },
      ],
      toDOM: (node) => [
        'div',
        {
          'data-custom-node': '',
          'data-title': node.attrs.title,
          'data-id': node.attrs.id,
        },
        0,
      ],
    }
  }

  commands({ type }) {
    return () => toggleWrap(type)
  }

  get plugins() {
    return [
      new Plugin({
        key: new PluginKey('customNode'),
        props: {
          handleClick: (view, pos, event) => {
            console.log('clicked!', event)
          },
          handleDOMEvents: {
            click: (view, event) => {
              const { schema, selection } = view.state
              const attrs = { title: 'New Title', id: 'new-id' }
              const transaction = view.state.tr.setNodeMarkup(selection.$from.depth, null, attrs, [])
              view.dispatch(transaction)
              return true
            },
          },
        },
      }),
    ]
  }
}
```

在此示例中，我们定义了一个新的 Node `CustomNode`，并在 schema、command 和 plugin 中修改了它的行为。我们还定义了 `title` 和 `id` 属性，让 Node 中的内容更加自定义。在 plugin 中，我们向 Node 添加了点击事件和 DOM 事件处理程序，用于更新状态并实现拖放行为。由于 Node 可以包含其他节点和文本，我们在 schema 中定义了它的 `content` 属性。

## Conclusion

在 Tiptap 中，您可以轻松地覆写、扩展或修改默认扩展、命令、Mark 和 Node 的行为，并使其完全适合于您的编辑器需求。