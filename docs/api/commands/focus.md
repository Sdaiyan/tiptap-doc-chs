# focus

该命令将焦点重新定位到编辑器。

当用户点击编辑器外的按钮时，浏览器会将焦点设置在该按钮上。在大多数情况下，您都需要将焦点重新聚焦到编辑器上，这就是为什么您在这里看到的每个演示基本上都会这样做。

参见：[setTextSelection](/api/commands/set-text-selection), [blur](/api/commands/blur)

## 参数
`position: 'start' | 'end' | 'all' | number | boolean | null (false)`

默认情况下，它会恢复光标的位置（和文本选择）。将位置传递给它可以将光标移到该位置。

`options: { scrollIntoView: boolean }`

定义聚焦时是否滚动到光标位置。默认为`true`。

## 用法
```js
// 将焦点重新定位到编辑器
editor.commands.focus()

// 将光标设置为第一个位置
editor.commands.focus('start')

// 将光标设置为最后一个位置
editor.commands.focus('end')

// 选择整个文档
editor.commands.focus('all')

// 将光标设置为第10个位置
editor.commands.focus(10)
```