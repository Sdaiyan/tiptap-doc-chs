# setContent
`setContent` 命令会用新的文档替换当前文档。你可以传入 JSON 或 HTML，都可以正常工作。基本上与初始化时设置 `content` 属性的效果相同。

另请参考：[insertContent](/api/commands/insert-content), [clearContent](/api/commands/clear-content)

## 参数
`content: string`

把字符串（JSON 或 HTML）作为[内容](/guide/output)传递。编辑器将根据[模式](/api/schema)仅呈现允许的内容。

`emitUpdate?: Boolean (false)`

默认情况下，不会触发更新事件。传递 `true` 不会阻止触发更新事件。

`parseOptions?: Record<string, any>`

可以在初始化期间和/或使用 `setContent` 时传递配置解析的选项。详细了解 parseOptions，请参阅[ProseMirror文档](https://prosemirror.net/docs/ref/#model.ParseOptions)。

## 用法
```js
// HTML
editor.commands.setContent('<p>Example Text</p>')

// JSON
editor.commands.setContent({
  "type": "doc",
  "content": [
    {
      "type": "paragraph",
      "content": [
        {
          "type": "text",
          "text": "Example Text"
        }
      ]
    }
  ]
})
```