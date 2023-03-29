# 自定义文档

https://embed.tiptap.dev/preview/Examples/CustomDocument

## 介绍

使用 tiptap 时，您可以通过继承 `Document` 组件来自定义文档。这将使您能够完全控制文档中使用的节点和标记。

## 示例代码

在下面的示例中，我们创建了一个自定义文档，其中我们使用了一些自定义节点和标记：

```javascript
import { Document, Paragraph } from 'tiptap'
import { MyCustomNode, MyCustomMark } from './myCustomNodes'

export default class MyCustomDocument extends Document {
  get schema() {
    return {
      nodes: {
        doc: {
          content: 'paragraph+',
        },
        paragraph: {
          content: 'text*',
          toDOM: () => ['p', 0],
        },
        myCustomNode: MyCustomNode,
      },
      marks: {
        myCustomMark: MyCustomMark,
      },
    }
  }
}
```
上述代码中，我们创建了一个继承自 `Document` 的自定义类。我们指定了文档的架构，其中包含了 `Paragraph` 和 `MyCustomNode` 节点，以及 `MyCustomMark` 标记。

## 结论

由于我们已经继承了 `Document` 类，因此我们可以完全控制文档的结构。请确保您在使用此方法时了解 tiptap 的节点和标记系统，以及如何将它们集成到自定义文档中。