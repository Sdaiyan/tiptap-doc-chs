# insertContent
`insertContent` 命令将传入的值添加到文档中。

另请参见: [setContent](/api/commands/set-content), [clearContent](/api/commands/clear-content)

## 参数
`value: Content`

该命令非常灵活，可以接受纯文本、HTML，甚至是 JSON 作为值。

## 用法
```js
// 纯文本
editor.commands.insertContent('示例文字')

// HTML
editor.commands.insertContent('<h1>示例文字</h1>')

// HTML 并删除空白
editor.commands.insertContent('<h1>示例文字</h1>', 
{
  parseOptions: {
    preserveWhitespace: false,
  }
})

// JSON/节点
editor.commands.insertContent({
  type: 'heading',
  attrs: {
    level: 1,
  },
  content: [
    {
      type: 'text',
      text: '示例文字',
    },
  ],
})

// 一次添加多个节点
editor.commands.insertContent([
  {
    type: 'paragraph',
    content: [
      {
        type: 'text',
        text: '第一段',
      },
    ],
  },
  {
    type: 'paragraph',
    content: [
      {
        type: 'text',
        text: '第二段',
      },
    ],
  },
])
```