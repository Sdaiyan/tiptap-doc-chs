# 导出

## 简介

你可以将内容存储为 JSON 对象或 HTML 字符串。两者都可以正常工作。当然，你也可以将这两种格式都传递给编辑器以恢复内容。这里有一个交互式示例，当文档被更改时，它会将内容导出为 HTML 和 JSON 格式：

## 导出

### 选项 1: JSON

JSON 可能更容易循环遍历，例如查找提到的内容，而且它更接近于 Tiptap 底层使用的格式。无论如何，如果你想使用 JSON 存储内容，我们提供了一种将内容以 JSON 格式检索的方法：

```javascript
const json = editor.getJSON()
```

你可以将其存储在数据库中（或将其发送到 API），并像这样最初恢复文档：

```javascript
new Editor({
  content: {
    "type": "doc",
    "content": [
      // …
    ]
  },
})
```

或者，如果你需要等待某些操作完成，可以通过编辑器实例稍后完成：

```javascript
editor.commands.setContent({
  "type": "doc",
  "content": [
    // …
  ]
})
```

这里有一个交互式示例，你可以看到它的实际效果：

<iframe src="https://embed.tiptap.dev/preview/GuideContent/ExportJSON?inline=false&amp;hideSource=true" width="100%" height="0" frameborder="0" id="iFrameResizer0" scrolling="no" style="overflow: hidden; height: 486px;"></iframe>

### 选项2：HTML

HTML可以轻松地在其他地方进行渲染，例如在电子邮件中，并且广泛使用，因此在某些时候更换编辑器可能会更容易。无论如何，每个编辑器实例都提供了一种从当前文档获取HTML的方法：

```javascript
const html = editor.getHTML()
```

然后可以将其用于最初恢复文档：

```javascript
new Editor({
  content: `<p>Example Text</p>`,
})
```

或者如果您想稍后恢复内容（例如在API调用完成后），也可以这样做：

```javascript
editor.commands.setContent(`<p>Example Text</p>`)
```

使用此交互式示例进行调试：

<iframe src="https://embed.tiptap.dev/preview/GuideContent/ExportHTML?inline=false&amp;hideSource=true" width="100%" height="0" frameborder="0" id="iFrameResizer1" scrolling="no" style="overflow: hidden; height: 270px;"></iframe>

### [#](https://tiptap.dev/guide/output#option-3-yjs)选项3：Y.js

我们的编辑器对Y.js提供了一流的支持，这是添加实时协作、离线编辑或在设备之间同步等功能的绝佳选择。

在内部，Y.js存储了所有更改的历史记录。它可以在浏览器、服务器上、与其他连接的客户端同步，或者在USB存储设备上。但是，了解到Y.js需要这些存储的更改。一个简单的JSON文档并不足以合并更改。

当然，您可以导入现有的JSON文档以开始工作，并从Y.js获得JSON，但这更像是一种导入/导出格式。这不会成为您的单一来源。在添加Y.js以满足其中一种用例时，这一点很重要。

尽管如此，它仍然是非常棒的，并且我们将提供一个令人惊叹的后端，使所有这些变得轻而易举。

### [#](https://tiptap.dev/guide/output#not-an-option-markdown)不支持Markdown

不幸的是，**Tiptap不支持Markdown作为输入或输出格式**。我们曾考虑过添加支持，但以下是我们决定不这样做的原因：

- HTML和JSON都可以具有深层嵌套的结构，而Markdown是平面的。
- Markdown标准有所不同。
- Tiptap的优势是定制化，而这与Markdown不太搭配。
- 有足够的包可以将HTML转换为Markdown，反之亦然。

你应该真正考虑使用HTML或JSON来存储你的内容，它们在大多数用例中都非常好用。

如果你仍然认为你需要Markdown，ProseMirror有一个[处理Markdown的例子](https://prosemirror.net/examples/markdown/)，[Nextcloud Text](https://github.com/nextcloud/text)使用Tiptap 1来处理Markdown。也许你可以从中学习。或者如果你正在寻找一个真正好的Markdown编辑器，可以尝试[CodeMirror](https://codemirror.net/)。

话虽如此，Tiptap支持[Markdown快捷键](https://tiptap.dev/examples/markdown-shortcuts)来格式化你的内容。此外，你可以让你的内容看起来像Markdown，例如在CSS中在`<h1>`前加上`#`。

## [#](https://tiptap.dev/guide/output#listening-for-changes)监听更改

如果你想持续存储人们写作的更新内容，你可以[挂钩事件](https://tiptap.dev/api/events)。这是一个例子：

```javascript

const editor = new Editor({
  // intial content
  content: `<p>Example Content</p>`,

  // triggered on every change
  onUpdate: ({ editor }) => {
    const json = editor.getJSON()
    // send the content to an API here
  },
})
```

## [#](https://tiptap.dev/guide/output#rendering)渲染

### [#](https://tiptap.dev/guide/output#option-1-read-only-instance-of-tiptap)选项 1：只读模式下的 Tiptap 实例

要渲染保存的内容，请将编辑器设置为只读模式。这样就可以实现与编辑器中完全相同的渲染，而无需复制 CSS 和其他代码。

<iframe src="https://embed.tiptap.dev/preview/GuideContent/ReadOnly?inline=false&amp;hideSource=false" width="100%" height="0" frameborder="0" id="iFrameResizer2" scrolling="no" style="overflow: hidden; height: 809px;"></iframe>

### [#](https://tiptap.dev/guide/output#option-2-generate-html-from-prosemirror-json)选项 2：从 ProseMirror JSON 生成 HTML

如果您需要在服务器端呈现内容，例如为使用 Tiptap 编写的博客文章生成 HTML，则可能希望在没有实际编辑器实例的情况下完成此操作。

这就是 `generateHTML()` 的作用。它是一个辅助函数，可以在没有实际编辑器实例的情况下呈现 HTML。

<iframe src="https://embed.tiptap.dev/preview/GuideContent/GenerateHTML?inline=false&amp;hideSource=false" width="100%" height="0" frameborder="0" id="iFrameResizer4" scrolling="no" style="overflow: hidden; height: 809px;"></iframe>

顺便说一下，另一种方法也是可行的。以下示例显示了如何从 HTML 生成 JSON。

<iframe src="https://embed.tiptap.dev/preview/GuideContent/GenerateJSON?inline=false&amp;hideSource=false" width="100%" height="0" frameborder="0" id="iFrameResizer3" scrolling="no" style="overflow: hidden; height: 1065px;"></iframe>

## [#](https://tiptap.dev/guide/output#migration)迁移

如果要将现有内容迁移到 Tiptap，我们建议将现有输出转换为 HTML。这可能是将初始内容导入 Tiptap 的最佳格式，因为 ProseMirror 确保没有问题。即使有一些标记或属性不被允许（基于您的配置），Tiptap 也会安静地将它们丢弃。

我们即将介绍一些案例，以帮助您进行此操作，例如我们提供了一个 PHP 包，将 HTML 转换为兼容的 JSON 结构：[ueberdosis/prosemirror-to-html](https://github.com/ueberdosis/html-to-prosemirror)。

## [#](https://tiptap.dev/guide/output#security)安全性

出于安全方面的考虑，没有理由选择使用 JSON 还是 HTML。如果有人想要向您的服务器发送恶意内容，无论它是 JSON 还是 HTML，都没有关系。甚至您是否使用 Tiptap 都没有关系。您应该始终验证用户输入。