# clearNodes

`clearNodes` 命令将节点规范化为默认节点，其中默认节点默认情况下为段落。它甚至可以规范化各种类型的列表。对于高级用例，在应用新的节点类型之前使用此命令可能会很方便。

如果您想知道如何定义默认节点：它取决于您的 [`Document`](https://tiptap.dev/api/nodes/document) 的 `content` 属性中的内容，默认情况下为 `block+`（至少一个块节点），[`Paragraph`](https://tiptap.dev/api/nodes/paragraph) 节点具有最高优先级，因此它最先加载，因此是默认节点。

## 用法

```js
editor.commands.clearNodes()
```
