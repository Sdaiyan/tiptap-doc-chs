# 提示功能
[![版本](https://img.shields.io/npm/v/@tiptap/suggestion.svg?label=version)](https://www.npmjs.com/package/@tiptap/suggestion)
[![下载量](https://img.shields.io/npm/dm/@tiptap/suggestion.svg)](https://npmcharts.com/compare/@tiptap/suggestion?minimal=true)

此实用工具可帮助编辑器中的各种提示。 可查看 [`Mention`](/api/nodes/mention), [`Hashtag`](/api/nodes/hashtag) 或 [`Emoji`](/api/nodes/emoji) 节点，以查看其实际应用。

## 设置

### char 
触发自动完成弹出窗口的字符。

默认值：`'@'`

### pluginKey
ProseMirror PluginKey。

默认值：`SuggestionPluginKey`

### allowSpaces
允许或禁止提示项中的空格。

默认值：`false`

### allowedPrefixes 
可用于触发建议的前缀字符。设置为 `null` 可以允许任何前缀字符。

默认值：`[' ']`

### startOfLine
仅在行的开始处触发自动完成弹出窗口。

默认值：`false`

### decorationTag
应为提示所呈现的 HTML 标记。

默认值：`'span'`

### decorationClass
应添加到提示的 CSS 类。

默认值：`'suggestion'`

### command
选中建议时执行的命令。

默认值：`() => {}'`

### items
传递一个已过滤建议的数组，可以是异步的。

默认值：`({ editor, query }) => []`

### render
自动完成弹出窗口的渲染函数。

默认值：`() => ({})`


## 源代码
[packages/suggestion/](https://github.com/ueberdosis/tiptap/blob/main/packages/suggestion/)