# 语法高亮

在 tiptap 中，您可以使用 CodeBlock 组件快速创建代码块并添加语法高亮。要在代码块中添加语法高亮，您需要使用第三方库 Prism.js。

在您的项目中安装 Prism.js 后，您可以将其导入到您的代码块中，如下所示：

```ts
import { CodeBlock } from 'tiptap'
import Prism from 'prismjs'
import 'prismjs/themes/prism.css'
import 'prismjs/components/prism-javascript'
// 导入您需要的其他语言
export default CodeBlock.extend({
  content: 'text*',
  code: '',
  language: '',
  parser: {
    parse: () => []
  },
  renderHTML({ HTMLAttributes }) {
    return ['pre', HTMLAttributes, ['code', { class: 'language-' + this.language }, this.code]]
  },
  commands: {
    updateLanguage(language) {
      return ({ attrs }) => {
        return { ...attrs, language }
      }
    },
    updateCode(code) {
      return ({ attrs }) => {
        return { ...attrs, code }
      }
    },
    setNodeAttrs(attrs) {
      return ({ attrs: oldAttrs }) => {
        return { ...oldAttrs, ...attrs }
      }
    }
  },
  addAttributes() {
    return {
      language: {
        default: null,
        parseHTML: element => ({
          language: element.getAttribute('data-language')
        }),
        renderHTML: attributes => {
          if (!attributes.language) {
            return {}
          }

          return {
            'data-language': attributes.language,
            class: 'language-' + attributes.language
          }
        },
        renderText: () => ''
      },
      code: {
        default: null,
        parseHTML: element => ({
          code: element.textContent
        }),
        renderHTML: attributes => {
          return {
            'data-language': attributes.language,
            class: 'language-' + attributes.language,
            style: 'white-space: pre-wrap;',
            textContent: attributes.code
          }
        },
        renderText: ({ node }) => node.attrs.code
      }
    }
  },
  addCommands() {
    return {
      setCodeBlockLanguage: language => ({ schema, commands }) => {
        const type = schema.nodes.code_block
        return commands.setNodeAttrs({
          language
        }, type)
      }
    }
  },
  onBeforeUpdate() {
    const grammar = Prism.languages[this.language]
    this.code = Prism.highlight(this.code, grammar, this.language)
  }
})
```

在上面的示例中，您可以看到我们如何导入 Prism.js，并将其添加到 `CodeBlock` 组件中。`onBeforeUpdate` 钩子在每次更新内容或语言时触发，会使用 Prism.js 来对代码块进行语法高亮。请注意，您需要导入所需的语言，并将其添加到 `Prism.languages` 对象中。

然后，您需要在渲染时将 `language` 和 `code` 设置为 JSX 属性，我们在上面的 `renderHTML` 方法中展示了这个过程。

除了默认的语言和代码属性之外，您还可以添加其他属性以对代码块进行进一步设置。在上面的代码中，我们使用了 `addAttributes` 方法，使 `language` 属性和 `code` 属性可用。这样，我们就可以在 `commands` 对象中使用这些属性来更新代码块。在上述代码中，我们为更新 `language` 和 `code` 添加了两个命令。

最后，我们使用 `setCodeBlockLanguage` 命令在 `CodeBlock` 组件中设置语言。在使用此命令时，您需要将其传递给命令库，并将其与 `schema` 和 `commands` 参数一起使用。