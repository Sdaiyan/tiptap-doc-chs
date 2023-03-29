# 使用 React 实现 Node Views

## 介绍

如果你习惯于使用 React，那么使用纯 JavaScript 可能会让你感到复杂。好消息是：你也可以在 node views 中使用普通的 React 组件。只需要了解一点点，我们来一步一步学习。

## [#](https://tiptap.dev/guide/node-views/react#render-a-react-component)渲染 React 组件

下面是在编辑器内渲染 React 组件所需的步骤：

1. [创建一个 node 扩展](https://tiptap.dev/guide/custom-extensions)
2. 创建一个 React 组件
3. 将该组件传递给提供的 `ReactNodeViewRenderer`
4. 使用 `addNodeView()` 注册组件
5. [配置 Tiptap 使用你的新 node 扩展](https://tiptap.dev/guide/configuration)

这是你的 node 扩展应该看起来的样子：

```jsx
import { Node } from '@tiptap/core'
import { ReactNodeViewRenderer } from '@tiptap/react'
import Component from './Component.jsx'

export default Node.create({
  // 配置 ...

  addNodeView() {
    return ReactNodeViewRenderer(Component)
  },
})
```

这里需要一点点的魔法才能使其工作。但别担心，我们提供了一个包装组件，可以让你轻松入门。别忘了将其添加到你的自定义 React 组件中，如下所示：

```jsx
<NodeViewWrapper className="react-component">
  React 组件
</NodeViewWrapper>
```

理解了吗？我们来看看它是如何工作的。可以复制下面的示例开始尝试。

<iframe src="https://embed.tiptap.dev/preview/GuideNodeViews/ReactComponent?inline=false&amp;hideSource=false" width="100%" height="0" frameborder="0" id="iFrameResizer0" scrolling="no" style="overflow: hidden; height: 777px;"></iframe>

不过该组件还没有与编辑器交互。现在是时候将它们连接起来了。

## [#](https://tiptap.dev/guide/node-views/react#access-node-attributes)访问节点属性

你在节点扩展中使用的`ReactNodeViewRenderer`会向你的自定义 React 组件传递一些非常有用的属性。其中之一是 `node` 属性。假设你已经[向你的节点扩展添加了一个名为 `count` 的属性](https://tiptap.dev/guide/custom-extensions#attributes)（就像我们在上面的例子中所做的那样），你可以像这样访问它：

```jsx

props.node.attrs.count
```

## [#](https://tiptap.dev/guide/node-views/react#update-node-attributes)更新节点属性

你甚至可以使用传递给你的组件的 `updateAttributes` 属性从你的节点中更新节点属性。将带有更新后属性的对象传递给 `updateAttributes` 属性：

```jsx
export default props => {
  const increase = () => {
    props.updateAttributes({
      count: props.node.attrs.count + 1,
    })
  }

  // …
}
```

是的，所有这些也是响应式的。这是一种非常平滑的通信方式，不是吗？

## [#](https://tiptap.dev/guide/node-views/react#adding-a-content-editable)添加可编辑内容

还有另一个名为 `NodeViewContent` 的组件，它可以帮助你在节点视图中添加可编辑内容。这里是一个例子：

```jsx
import React from 'react'
import { NodeViewWrapper, NodeViewContent } from '@tiptap/react'

export default () => {
  return (
    <NodeViewWrapper className="react-component-with-content">
      <span className="label" contentEditable={false}>React 组件</span>

      <NodeViewContent className="content" />
    </NodeViewWrapper>
  )
}
```

你不需要添加这些 `className` 属性，随意删除它们或传递其他类名。在下面的例子中尝试一下：

<iframe src="https://embed.tiptap.dev/preview/GuideNodeViews/ReactComponentContent?inline=false&amp;hideSource=false" width="100%" height="0" frameborder="0" id="iFrameResizer1" scrolling="no" style="overflow: hidden; height: 777px;"></iframe>

请记住，这些内容是由 Tiptap 渲染的。这意味着你需要告诉 Tiptap 哪些类型的内容是允许的，例如在你的节点扩展中使用 `content: 'inline*'`（就像我们在上面的例子中所使用的那样）。

`NodeViewWrapper` 和 `NodeViewContent` 组件会呈现 `<div>` HTML 标记（对于行内节点为 `<span>`），但你可以更改它们。例如，`<NodeViewContent as="p">` 应该呈现一个段落。但有一个限制：这个标记在运行时不能改变。

## [#](https://tiptap.dev/guide/node-views/react#all-available-props)所有可用的属性

以下是您可以使用的所有属性列表：

### [#](https://tiptap.dev/guide/node-views/react#editor)editor

编辑器实例

### [#](https://tiptap.dev/guide/node-views/react#node)node

当前节点

### [#](https://tiptap.dev/guide/node-views/react#decorations)decorations

装饰数组

### [#](https://tiptap.dev/guide/node-views/react#selected)selected

当存在`NodeSelection`在当前节点视图时，为 `true`

### [#](https://tiptap.dev/guide/node-views/react#extension)extension

访问节点扩展，例如获取选项

### [#](https://tiptap.dev/guide/node-views/react#get-pos)getPos()

获取当前节点在文档中的位置

### [#](https://tiptap.dev/guide/node-views/react#update-attributes)updateAttributes()

更新当前节点的属性

### [#](https://tiptap.dev/guide/node-views/react#delete-node)deleteNode()

删除当前节点

## [#](https://tiptap.dev/guide/node-views/react#dragging)拖动

要使节点视图可拖动，请在扩展中设置`draggable: true`，并将 `data-drag-handle` 添加到应该作为拖动手柄的 DOM 元素中。