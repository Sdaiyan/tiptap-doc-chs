# 示例

## 简介

节点视图可以让您完全自定义节点。我们在此收集了一些不同的示例。随意复制它们并开始构建。

请记住，这些只是示例，以帮助您入门，并非官方支持的扩展。我们没有为它们编写测试，并且不打算像官方扩展一样进行维护。

## [#](https://tiptap.dev/guide/node-views/examples#drag-handles)拖拽句柄

添加拖拽句柄并不容易。我们仍在寻找添加它们的最佳方式。官方支持将在某个时间点到来，但目前没有时间表。

<iframe src="https://embed.tiptap.dev/preview/GuideNodeViews/DragHandle?inline=false&amp;hideSource=false" width="100%" height="0" frameborder="0" id="iFrameResizer0" scrolling="no" style="overflow: hidden; height: 1009px;"></iframe>

## [#](https://tiptap.dev/guide/node-views/examples#table-of-contents)目录

此示例循环遍历编辑器内容，为所有标题赋予一个ID，并使用Vue呈现目录。

<iframe src="https://embed.tiptap.dev/preview/GuideNodeViews/TableOfContents?inline=false&amp;hideSource=false" width="100%" height="0" frameborder="0" id="iFrameResizer1" scrolling="no" style="overflow: hidden; height: 1065px;"></iframe>

## [#](https://tiptap.dev/guide/node-views/examples#drawing-in-the-editor)在编辑器中绘图

绘图示例显示了一个SVG，使您可以在编辑器中进行绘图。

<iframe src="https://embed.tiptap.dev/preview/Examples/Drawing?inline=false&amp;hideSource=false" width="100%" height="0" frameborder="0"></iframe>

它与Collaboration扩展不太兼容。它在每次更改时发送所有数据，这可能会导致Y.js非常庞大。如果您计划将这两个组合使用，则需要改进它或您的WebSocket后端将崩溃。