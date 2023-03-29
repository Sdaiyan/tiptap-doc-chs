# 简介

Tiptap 是 [ProseMirror](https://prosemirror.net/) 的友好封装。尽管 Tiptap 试图隐藏 ProseMirror 的大部分复杂性，但它是基于其 API 构建的，我们建议您阅读 [ProseMirror 指南](https://prosemirror.net/docs/guide/) 以获取高级用法。

### 结构

ProseMirror 使用严格的 [Schema](https://tiptap.dev/api/schema) 来定义文档的允许结构。一个文档是标题、段落和其他元素（称为节点）的树形结构。标记可以附加到一个节点上，例如强调其中的一部分。[命令](https://tiptap.dev/api/commands) 可以以编程方式更改文档。

### 内容

文档存储在状态中。所有更改都作为事务应用于状态。状态具有有关当前内容、光标位置和选择的详细信息。您可以挂钩到一些不同的 [事件](https://tiptap.dev/api/events)，例如在应用它们之前修改事务。

### 扩展

扩展将 [节点](https://tiptap.dev/api/nodes)、[标记](https://tiptap.dev/api/marks) 和/或 [功能](https://tiptap.dev/api/extensions) 添加到编辑器中。其中许多扩展将它们的命令绑定到常见的 [键盘快捷键](https://tiptap.dev/api/keyboard-shortcuts)。

## 词汇表

ProseMirror 有自己的词汇表，您会时常遇到这些单词。以下是我们在文档中使用的最常见单词的简要概述。

| 单词        | 描述                                   |
| ----------- | -------------------------------------- |
| Schema      | 配置内容可以具有的结构。               |
| Document    | 编辑器中的实际内容。                   |
| State       | 描述编辑器当前内容和选择的所有内容。   |
| Transaction | 对状态进行的更改（更新选择、内容等）。 |
| Extension   | 注册新功能。                           |
| Node        | 内容类型，例如标题或段落。             |
| Mark        | 可应用于节点的标记，例如用于内联格式。 |
| Command     | 在编辑器中执行更改状态的操作。         |
| Decoration  | 文档上方的样式，例如突出显示错误。     |
